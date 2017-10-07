---
title: aaaCreate taken tooprepare taken en volledige taken op rekenknooppunten - Azure Batch | Microsoft Docs
description: Gebruik op jobniveau voorbereiding taken toominimize gegevens overbrengen tooAzure Batch-rekenknooppunten en release van taken voor het opruimen van knooppunt bij Taakvoltooiing.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a>Taak uitvoeren voorbereidings- en jobvrijgevingstaken voor Batch-rekenknooppunten

 Een Azure Batch-taak is een vorm van setup vaak vereist voordat de bijbehorende taken worden uitgevoerd en onderhoud na taak wanneer de taken zijn voltooid. U mogelijk nodig toodownload algemene taak invoergegevens tooyour rekenknooppunten of taak uitvoer gegevens tooAzure opslag uploaden nadat het Hallo-taak is voltooid. U kunt **taak voorbereiding** en **taak release** taken tooperform deze bewerkingen.

## <a name="what-are-job-preparation-and-release-tasks"></a>Wat zijn taakvoorbereidingstaak en release van taken?
Voordat een job taken worden uitgevoerd, Hallo jobvoorbereidingstaak wordt uitgevoerd op alle compute knooppunten geplande toorun ten minste één taak. Zodra het Hallo-taak is voltooid, wordt Hallo jobvrijgevingstaak uitgevoerd op elk knooppunt in Hallo pool dat ten minste één taak uitgevoerd. Net als bij normale Batch-taken, kunt u een opdrachtregel toobe aangeroepen wanneer een taakvoorbereidingstaak of release-taak wordt uitgevoerd.

Jobvoorbereidingstaken en jobvrijgevingstaken taken bieden vertrouwde Batch taakfuncties zoals bestand downloaden ([bronbestanden][net_job_prep_resourcefiles]), verhoogde uitvoering, aangepaste omgevingsvariabelen, maximale uitvoering duur, probeer het opnieuw aantal en bewaartijd voor bestanden.

In de Hallo uit te voeren, leert u hoe toouse hello [JobPreparationTask] [ net_job_prep] en [JobReleaseTask] [ net_job_release] in Hallo klassen gevonden [Batch .NET] [ api_net] bibliotheek.

> [!TIP]
> Jobvoorbereidingstaken en jobvrijgevingstaken taken zijn vooral handig in omgevingen 'van toepassingen wordt gedeeld', waarop een pool van rekenknooppunten zich blijft voordoen tussen de taak wordt uitgevoerd en wordt gebruikt door veel taken.
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a>Wanneer toouse taak voorbereiding en release van taken
Taakvoorbereidings- en jobvrijgevingstaken zijn geschikt voor Hallo volgende situaties:

**Algemene taakgegevens downloaden**

Batchtaken is vaak een gemeenschappelijke set gegevens als invoer voor Hallo projecttaken vereist. In de dagelijkse risico analysis berekeningen is marktgegevens bijvoorbeeld specifieke nog algemene tooall taken in Hallo taak. Deze marktgegevens, grootte, vaak enkele gigabytes moet gedownloade tooeach rekenknooppunt slechts één keer zodat elke taak die wordt uitgevoerd op Hallo knooppunt kan worden gebruikt. Gebruik een **jobvoorbereidingstaak** toodownload dit gegevens tooeach knooppunt voordat de uitvoering van Hallo taak Hallo's andere taken.

**Verwijderen van de taak en uitvoer**

In een omgeving 'van toepassingen wordt gedeeld', waarbij een groep rekenknooppunten zich niet buiten gebruik gestelde tussen taken, moet u de taakgegevens toodelete tussen wordt uitgevoerd. Mogelijk moet u tooconserve vrije schijfruimte op Hallo knooppunten of voldoen aan het beveiligingsbeleid van uw organisatie. Gebruik een **jobvrijgevingstaak** toodelete gegevens die zijn gedownload door een jobvoorbereidingstaak of gegenereerd tijdens de uitvoering van de taak.

**Logboek bewaren**

U kunt een kopie van de logboekbestanden die uw taken wordt gegenereerd of misschien crashdumpbestanden dat kunnen worden gegenereerd door de mislukte toepassingen tookeep. Gebruik een **jobvrijgevingstaak** in dergelijke gevallen toocompress en upload dit tooan gegevens [Azure Storage] [ azure_storage] account.

> [!TIP]
> Een andere manier toopersist logboeken en andere taak en uitvoer gegevens zijn toouse hello [Azure Batch-bestand conventies](batch-task-output.md) bibliotheek.
> 
> 

## <a name="job-preparation-task"></a>Jobvoorbereidingstaak
Batch: Hallo jobvoorbereidingstaak voordat de uitvoering van een job taken uitvoeren op elk rekenknooppunt die geplande toorun een taak. Standaard wacht Hallo Batch-service op Hallo taak voorbereiding taak toobe voltooid voordat de geplande taken-tooexecute Hallo op Hallo knooppunt uitgevoerd. U kunt echter Hallo-service niet toowait configureren. Als Hallo knooppunt opnieuw wordt opgestart, Hallo jobvoorbereidingstaak opnieuw wordt uitgevoerd, maar u kunt dit gedrag ook uitschakelen.

Hallo jobvoorbereidingstaak wordt alleen uitgevoerd op knooppunten die geplande toorun een taak. Dit voorkomt dat Hallo onnodige uitvoering van een jobvoorbereidingstaak als een knooppunt niet aan een taak toegewezen is. Dit kan gebeuren wanneer Hallo aantal taken voor een job minder dan het aantal knooppunten in een pool Hallo is. Dit geldt ook wanneer [uitvoering van gelijktijdige taken](batch-parallel-node-tasks.md) is ingeschakeld, waardoor sommige knooppunten inactief als het aantal van de taak Hallo is lager dan Hallo totale mogelijke gelijktijdige taken. Door de jobvoorbereidingstaak Hallo niet wordt uitgevoerd op niet-actieve knooppunten, kunt u minder geld besteden aan gegevensbelasting overdracht.

> [!NOTE]
> [JobPreparationTask] [ net_job_prep_cloudjob] verschilt van [CloudPool.StartTask] [ pool_starttask] in dat JobPreparationTask aan Hallo begin van elke taak wordt uitgevoerd terwijl StartTask voert alleen wanneer een rekenknooppunt eerst lid wordt van een groep of opnieuw wordt opgestart.
> 
> 

## <a name="job-release-task"></a>Jobvrijgevingstaak
Zodra een taak is gemarkeerd als voltooid, wordt Hallo jobvrijgevingstaak uitgevoerd op elk knooppunt in Hallo pool dat ten minste één taak uitgevoerd. U kunt een taak markeren als voltooid door uitgifte van een aanvraag beëindigen. Hallo Batch-service en vervolgens stelt Hallo taakstatus te*beëindigd*, die is gekoppeld aan taak Hallo actief of actieve taken beëindigd en Hallo jobvrijgevingstaak wordt uitgevoerd. Hallo taak gaat vervolgens toohello *voltooid* status.

> [!NOTE]
> Verwijderen van een taak worden ook Hallo jobvrijgevingstaak uitgevoerd. Echter als al een taak is beëindigd, is Hallo release taak niet uitgevoerd een tweede keer als Hallo-taak wordt later verwijderd.
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a>Taak prep en de vrijgave van taken met Batch .NET
toewijzen van een jobvoorbereidingstaak toouse een [JobPreparationTask] [ net_job_prep] object tooyour taak [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] eigenschap . Op deze manier initialiseren een [JobReleaseTask] [ net_job_release] en toewijzen van de taak tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] eigenschap tooset Hallo jobvrijgevingstaak.

In dit codefragment `myBatchClient` is een exemplaar van [BatchClient][net_batch_client], en `myPool` is een bestaande pool binnen Hallo Batch-account.

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

Zoals eerder vermeld, worden de Hallo release taak wordt uitgevoerd wanneer een taak is beëindigd of is verwijderd. Beëindigen van een taak met [JobOperations.TerminateJobAsync][net_job_terminate]. Verwijderen van een taak met [JobOperations.DeleteJobAsync][net_job_delete]. U doorgaans beëindigen of verwijderen van een taak wanneer de taken zijn voltooid of wanneer een time-out die u hebt gedefinieerd is bereikt.

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a>Voorbeeld van code op GitHub
toosee jobvoorbereidingstaken en jobvrijgevingstaken taken in actie, bekijk Hallo [JobPrepRelease] [ job_prep_release_sample] voorbeeldproject op GitHub. Deze consoletoepassing Hallo te volgen:

1. Maakt een groep met twee knooppunten voor 'kleine'.
2. Maakt een taak met taak voorbereidings-, release- en standaardtaken.
3. Wordt uitgevoerd Hallo jobvoorbereidingstaak schrijft eerst tooa tekstbestand voor Hallo knooppunt-ID in van een knooppunt 'gedeeld' directory.
4. Een taak wordt uitgevoerd op elk knooppunt dat de taak-ID toohello schrijft dezelfde tekstbestand.
5. Hallo-inhoud van elk knooppunt tekst bestand toohello console afdrukken zodra alle taken zijn voltooid (of Hallo time-out is bereikt)
6. Wanneer Hallo-taak is voltooid, voert u Hallo taak release toodelete Hallo-bestand van het Hallo-knooppunt.
7. Afdrukken bestellen Hallo afsluitcodes van Hallo taakvoorbereidingstaak en release van taken voor elk knooppunt waarop ze worden uitgevoerd.
8. Onderbroken uitvoering tooallow bevestiging van de taak en/of de groep verwijderen.

De uitvoer van de voorbeeldtoepassing Hallo is vergelijkbaar toohello volgende:

```
Attempting toocreate pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> Vervaldatum toohello variabele maken en start het tijdstip knooppunten in een nieuwe pool (sommige knooppunten zijn gereed voor taken vóór andere), ziet u andere uitvoer. In het bijzonder omdat Hallo taken snel kunnen worden uitgevoerd, mogen een van de knooppunten van de pool Hallo uitvoeren alle taken van Hallo taak. Als dit gebeurt, ziet u dat Hallo prep taak en de vrijgave van taken bestaan niet voor Hallo-knooppunt dat geen taken uitgevoerd.
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a>Inspecteer de taakvoorbereidingstaak en release-taken in hello Azure-portal
Wanneer u de voorbeeldtoepassing Hallo uitvoert, kunt u Hallo [Azure-portal] [ portal] tooview Hallo eigenschappen van het Hallo-taak en de bijbehorende taken of zelfs Hallo gedeelde tekstbestand dat door Hallo projecttaken wordt gewijzigd te downloaden.

Hallo schermafbeelding hieronder ziet u Hallo **voorbereiding taken blade** in Hallo na een uitvoering van de voorbeeldtoepassing hello Azure-portal. Navigeer toohello *JobPrepReleaseSampleJob* eigenschappen nadat uw taken hebt voltooid (maar voordat de job en de pool wordt verwijderd) en klik op **systeemvoorbereidingstaken** of **takenRelease** tooview hun eigenschappen.

![Voorbereiding taakeigenschappen in Azure-portal][1]

## <a name="next-steps"></a>Volgende stappen
### <a name="application-packages"></a>Toepassingspakketten
In aanvulling toohello jobvoorbereidingstaak, kunt u ook hello gebruiken [toepassingspakketten](batch-application-packages.md) functie van Batch tooprepare rekenknooppunten voor uitvoering van de taak. Deze functie is vooral handig voor het implementeren van toepassingen die niet met een installatieprogramma, toepassingen die veel (100 en hoger) bestanden bevatten of toepassingen waarvoor strikte versiebeheer nodig hebt.

### <a name="installing-applications-and-staging-data"></a>Installeren van toepassingen en gegevens voor fasering
Dit bericht MSDN-forum biedt een overzicht van de verschillende methoden voor het voorbereiden van uw knooppunten om taken uit te voeren:

[Installeren van toepassingen en staging-gegevens op de Batch-rekenknooppunten][forum_post]

Geschreven door een van de Azure Batch-teamleden hello, besproken verschillende technieken waarmee u toodeploy toepassingen en gegevens toocompute knooppunten kunt.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

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

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
