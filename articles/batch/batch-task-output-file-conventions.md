---
title: taak aaaPersist en uitvoer van tooAzure opslag met Hallo bestand Conventions-bibliotheek voor .NET - Azure Batch | Microsoft Docs
description: Meer informatie over hoe toouse bestand conventies van Azure Batch-bibliotheek voor .NET toopersist Batch-taak en de taak uitvoer tooAzure opslag en de weergave Hallo uitvoer in hello Azure-portal persistent.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a>Taak behouden en gegevens tooAzure opslag met Hallo Batch bestand Conventions-bibliotheek voor .NET toopersist taak 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Eenzijdige toopersist taakgegevens zijn toouse hello [bestand conventies van Azure Batch-bibliotheek voor .NET][nuget_package]. Hallo bestand conventies bibliotheek vereenvoudigt Hallo proces voor het opslaan van de uitvoer van de taak gegevens tooAzure opslag en het ophalen van het. Hallo bestand conventies bibliotheek in de taak en de client kunt u &mdash; taakcode voor persistent maken van bestanden en client toolist code en ze op te halen. Uw taakcode kunt ook Hallo bibliotheek tooretrieve Hallo uitvoer van de upstream-taken, zoals gebruiken in een [taakafhankelijkheden](batch-task-dependencies.md) scenario. 

tooretrieve uitvoerbestanden met Hallo bestand Conventions-bibliotheek, u kunt Hallo-bestanden voor een bepaalde taak of de taak vinden door deze door de ID en het doel. U hoeft niet tooknow Hallo namen of locaties van Hallo-bestanden. U kunt bijvoorbeeld Hallo bestand conventies bibliotheek toolist alle tussenliggende bestanden gebruiken voor een bepaalde taak of een preview-bestand voor een bepaalde taak ophalen.

> [!TIP]
> Hallo API van Batch-service ondersteunt persistent maken uitvoer gegevens tooAzure opslag voor taken en jobbeheertaken die worden uitgevoerd op de groepen die zijn gemaakt met de configuratie van de virtuele machine Hallo vanaf 2017-05-01-versie. Hallo API van Batch-service biedt een eenvoudige manier toopersist uitvoer van Hallo-code die een taak maakt en fungeert als een alternatieve toohello bestand Conventions-bibliotheek. U kunt uw Batch-client toepassingen toopersist uitvoer wijzigen zonder tooupdate Hallo toepassing die de taak wordt uitgevoerd. Zie voor meer informatie [taak gegevens tooAzure opslag Hello API van Batch-service behouden](batch-task-output-files.md).
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a>Wanneer kan ik Hallo bestand conventies bibliotheek toopersist-taakuitvoer gebruiken?

Azure Batch voorziet in meer dan een manier toopersist taakuitvoer. Hallo bestand conventies is aanbevolen geschikt toothese-scenario's:

- Hallo-code voor Hallo toepassing of de taak toopersist bestanden met behulp van Hallo bestand conventies bibliotheek wordt uitgevoerd, kunt u eenvoudig wijzigen.
- Gewenste toostream gegevens tooAzure opslag terwijl Hallo taak nog actief.
- Wilt u toopersist gegevens uit toepassingen die zijn gemaakt met Hallo cloud serviceconfiguratie of Hallo Virtuele-machineconfiguratie.
- Uw clienttoepassing of andere taken in Hallo van behoeften toolocate taken en downloaden van de taak uitvoerbestanden ID of met het doel. 
- Wilt u de taakuitvoer tooview in hello Azure-portal.

Als uw scenario van die verschilt hierboven zijn vermeld, moet u mogelijk een andere benadering tooconsider. Zie voor meer informatie over andere opties voor het persistent maken van de taakuitvoer [Persist taak en uitvoer tooAzure opslag](batch-task-output.md). 

## <a name="what-is-hello-batch-file-conventions-standard"></a>Wat is Hallo Batch bestand conventies standaard?

Hallo [Batch bestand conventies standaard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) biedt een schematische voor Hallo bestemming containers en blobs paden toowhich de uitvoerbestanden worden geschreven. Bestanden persistente tooAzure opslag die toohello bestand conventies standaard voldoen zijn automatisch beschikbaar voor weergave in hello Azure-portal. Hallo-portal is op de hoogte van de naamconventie Hallo en dus kan bestanden die tooit voldoen worden weergegeven.

Hallo bestand Conventions-bibliotheek voor .NET worden automatisch de uw storage-containers en uitvoerbestanden taak toohello bestand conventies standaard volgens naam. Hallo bestand Conventions-bibliotheek biedt ook methoden tooquery uitvoerbestanden in Azure Storage op basis van toojob-ID, taak-ID of doel.   

Als u met een andere taal dan .NET ontwikkelt, kunt u implementeren Hallo bestand conventies standaard uzelf in uw toepassing. Zie voor meer informatie [over Hallo Batch bestand conventies standaard](batch-task-output.md#about-the-batch-file-conventions-standard).

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a>Een Azure Storage-account tooyour Batch-account koppelen

toopersist uitvoer gegevens tooAzure opslag met behulp van Hallo bestand conventies bibliotheek, moet u eerst een Azure Storage-account tooyour Batch-account koppelen. Als u dit nog niet hebt gedaan, een opslag-account tooyour Batch-account koppelen via Hallo [Azure-portal](https://portal.azure.com):

1. Navigeer tooyour Batch-account in hello Azure-portal. 
2. Onder **instellingen**, selecteer **Opslagaccount**.
3. Als u nog geen een opslagaccount die is gekoppeld aan uw Batch-account, klikt u op **Storage-Account (geen)**.
4. Selecteer een opslagaccount in de lijst Hallo voor uw abonnement. Voor de beste prestaties gebruikt u een Azure Storage-account dat in Hallo dezelfde regio als Hallo Batch-account waarop uw taken worden uitgevoerd.

## <a name="persist-output-data"></a>Uitvoergegevens behouden

taak toopersist en uitvoergegevens met Hallo bestand Conventions-bibliotheek, een container maken in Azure Storage en Hallo uitvoer toohello container opslaan. Gebruik Hallo [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in uw taak code tooupload Hallo taak uitvoer toohello-container. 

Zie voor meer informatie over het werken met containers en blobs in Azure Storage [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

> [!WARNING]
> Alle uitvoerwaarden van taak en persistent is gemaakt met de Hallo bestand conventies bibliotheek worden opgeslagen in dezelfde container Hallo. Als een groot aantal taken probeert toopersist bestanden op Hallo dezelfde tijd [opslag beperking limieten](../storage/common/storage-performance-checklist.md#blobs) kan worden afgedwongen.
> 
> 

### <a name="create-storage-container"></a>Opslagcontainer maken

toopersist taak uitvoer tooAzure opslag, eerst een container maken door het aanroepen van [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync]. Deze uitbreidingsmethode heeft een [CloudStorageAccount] [ net_cloudstorageaccount] -object als parameter. Een container met de naam volgens toohello bestand conventies standaard zo in dat de inhoud ervan kunnen worden gedetecteerd door Azure portal en Hallo ophalen besproken methoden verderop in Hallo artikel Hallo wordt gemaakt.

U doorgaans Hallo code toocreate een container plaatsen in uw clienttoepassing &mdash; Hallo toepassing waarmee uw pools, jobs en taken worden gemaakt.

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a>Taakuitvoer Store

Nu dat u een container in Azure Storage hebt voorbereid, taken uitvoer toohello container kunnen opslaan met behulp van Hallo [TaskOutputStorage] [ net_taskoutputstorage] klasse gevonden in Hallo bestand Conventions-bibliotheek.

In uw taakcode maakt u eerst een [TaskOutputStorage] [ net_taskoutputstorage] object wanneer Hallo taak voltooid zijn werk, en roep vervolgens Hallo [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] methode toosave de uitvoer tooAzure opslag.

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

Hallo `kind` parameter Hallo [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) methode categoriseert Hallo persistent bestanden. Er zijn vier vooraf gedefinieerde [TaskOutputKind] [ net_taskoutputkind] typen: `TaskOutput`, `TaskPreview`, `TaskLog`, en `TaskIntermediate.` ook kunt u aangepaste categorieën van uitvoer.

Deze uitvoer-typen kunnen u toospecify welk type uitvoer toolist als u later Batch een query voor Hallo uitvoerwaarden van een bepaalde taak persistent. Wanneer u Hallo uitvoer voor een taak wilt weergeven, kunt u met andere woorden, Hallo-lijst op een van de Hallo uitvoer typen filteren. Bijvoorbeeld, "Geef me Hallo *preview* uitvoer voor de taak *109*." Meer informatie over het weergeven en ophalen van de uitvoer wordt weergegeven in [uitvoer ophalen](#retrieve-output) verderop in Hallo artikel.

> [!TIP]
> Hallo uitvoer soort bepaalt ook waar in hello Azure portal een bepaald bestand wordt weergegeven: *TaskOutput*-gecategoriseerde bestanden worden weergegeven onder **taak uitvoerbestanden**, en *TaskLog*-bestanden worden weergegeven onder **logboeken van de taak**.
> 
> 

### <a name="store-job-outputs"></a>Opslaan van de taak uitvoer

Bovendien toostoring taakuitvoer, kunt u opslaan Hallo-uitvoer die zijn gekoppeld aan een volledige-taak. In Hallo samenvoegen taak van een film rendering taak kunt u Hallo volledig gerenderde film kan behouden als de taakuitvoer van een. Als de taak is voltooid, kunt uw clienttoepassing lijst Hallo outputs voor Hallo-taak ophalen en is niet nodig tooquery Hallo afzonderlijke taken.

Taakuitvoer opslaan door de aanroepende Hallo [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] methode, en geef Hallo [JobOutputKind] [ net_joboutputkind] en bestandsnaam:

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

Net als bij Hallo **TaskOutputKind** type voor de taak uitvoer, u Hallo [JobOutputKind] [ net_joboutputkind] type toocategorize een taak de opgeslagen bestanden. Deze parameter kunt u de query toolater voor (lijst) voor een specifiek type uitvoer. Hallo **JobOutputKind** type bevat zowel uitvoer als preview-categorieën en biedt ondersteuning voor het maken van aangepaste categorieën.

### <a name="store-task-logs"></a>Taak logboeken worden opgeslagen

Bovendien toopersisting dat door een bestandsopslag toodurable wanneer een taak of de taak is voltooid, moet u mogelijk toopersist-bestanden die zijn bijgewerkt tijdens de uitvoering van een taak Hallo &mdash; logboekbestanden of `stdout.txt` en `stderr.txt`, bijvoorbeeld. Voor dit doel Hallo bestand conventies van Azure Batch-bibliotheek biedt een Hallo [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] methode. Met [SaveTrackedAsync][net_savetrackedasync], kunt u updates tooa bestand op Hallo-knooppunt (met een interval dat u opgeeft) bijhouden en persistent maken die updates tooAzure opslag.

In de Hallo codefragment te volgen, gebruiken we [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage elke 15 seconden tijdens het uitvoeren van taak Hallo Hallo:

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

Hallo opmerkingen sectie `Code tooprocess data and produce output file(s)` is een tijdelijke aanduiding voor Hallo-code die uw taak normaal kunt uitvoeren. Bijvoorbeeld wellicht code die gegevens uit Azure Storage downloadt en transformatie of berekening op deze uitvoert. Hallo belangrijk onderdeel van dit fragment is te demonstreren hoe u kunt laten teruglopen deze code in een `using` blok tooperiodically bijwerken van een bestand met [SaveTrackedAsync][net_savetrackedasync].

Hallo knooppunt agent is een programma dat wordt uitgevoerd op elk knooppunt in de pool Hallo en Hallo command en control interface vormt tussen Hallo-knooppunt en Hallo Batch-service. Hallo `Task.Delay` aanroep is vereist bij het einde van dit Hallo `using` blok tooensure dat knooppunt agent Hallo tijd tooflush Hallo inhoud van de standaard toohello stdout.txt bestand op Hallo knooppunt heeft. Zonder deze vertraging is het mogelijk toomiss Hallo laatste enkele seconden van uitvoer. Deze vertraging is mogelijk niet vereist voor alle bestanden.

> [!NOTE]
> Wanneer het inschakelen van bestand bijhouden met **SaveTrackedAsync**, alleen *voegt* toohello bijgehouden bestand persistente tooAzure opslag zijn. Deze methode alleen gebruiken voor het bijhouden van de logboekbestanden niet draaien of andere bestanden die zijn geschreven toowith operations toohello einde van Hallo-bestand toe te voegen.
> 
> 

## <a name="retrieve-output-data"></a>Uitvoergegevens ophalen

Wanneer u de persistente uitvoer met behulp van hello Azure Batch-bestand conventies bibliotheek ophaalt, kunt u dat doen op een taak en taak-gericht manier. U kunt aanvragen Hallo uitvoer voor de opgegeven taak zonder tooknow het pad in Azure Storage of zelfs de naam van het bestand. U kunt in plaats daarvan uitvoerbestanden aanvragen door de taak of taak-ID.

Hallo volgende codefragment doorlopen taken van een taak, wordt bepaalde informatie over de uitvoerbestanden Hallo voor Hallo taak afgedrukt, en vervolgens de bestanden uit Storage downloadt.

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a>De uitvoerbestanden weergeven in hello Azure-portal

Hello Azure-portal weergegeven taak uitvoerbestanden en logboeken die persistente tooa zijn gekoppelde Azure Storage-account met behulp van Hallo [Batch bestand conventies standaard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). U kunt ook zelf deze conventies implementeren in een taal van uw keuze Hallo of kunt u Hallo bestand conventies bibliotheek in uw .NET-toepassingen.

tooenable hello weergave van de uitvoerbestanden in Hallo-portal, moeten Hallo volgens de vereisten voldoen:

1. [Een Azure Storage-account koppelen](#requirement-linked-storage-account) tooyour Batch-account.
2. Vooraf gedefinieerde toohello naamgevingsregels voor Storage-containers en bestanden voldoen als uitvoer persistent maken. U vindt Hallo definitie van deze conventies in Hallo bestand conventies bibliotheek [Leesmij][github_file_conventions_readme]. Als u Hallo [Azure Batch-bestand conventies] [ nuget_package] bibliotheek toopersist uw uitvoer uw bestanden blijven aanwezig op basis van toohello bestand conventies standaard.

taakuitvoer tooview-bestanden en geregistreerd in hello Azure-portal, gaat u toohello taak waarvan de uitvoer u geïnteresseerd bent in, klik dan ofwel **opgeslagen uitvoerbestanden** of **opgeslagen logboeken**. Deze afbeelding ziet u Hallo **uitvoerbestanden opgeslagen** voor Hallo-taak met ID '007':

![Taakuitvoer blade in hello Azure-portal][2]

## <a name="code-sample"></a>Codevoorbeeld

Hallo [PersistOutputs] [ github_persistoutputs] voorbeeldproject is een van de Hallo [Azure Batch-codevoorbeelden] [ github_samples] op GitHub. Deze Visual Studio-oplossing laat zien hoe toouse hello Azure Batch-bestand conventies bibliotheek toopersist taak toodurable opslag uitvoer. toorun hello steekproef, als volgt te werk:

1. Open Hallo-project in **Visual Studio 2015 of hoger**.
2. Toevoegen van uw Batch- en Storage **accountreferenties** te**AccountSettings.settings** hello Microsoft.Azure.Batch.Samples.Common project.
3. **Bouwen** (maar niet worden uitgevoerd) Hallo oplossing. Herstel alle NuGet-pakketten als daarom wordt gevraagd.
4. Gebruik hello Azure portal tooupload een [toepassingspakket](batch-application-packages.md) voor **PersistOutputsTask**. Hallo omvatten `PersistOutputsTask.exe` en afhankelijke assembly's in Hallo ZIP-pakket, set Hallo toepassings-ID te 'PersistOutputsTask' en de toepassing hello Pakketversie te "1.0".
5. **Start** (uitvoeren) Hallo **PersistOutputs** project.
6. Wanneer de vraag toochoose Hallo persistentie technologie toouse voor actieve Hallo voorbeeld invoert **1** toorun Hallo voorbeeld met behulp van Hallo bestand conventies bibliotheek toopersist de taakuitvoer. 

## <a name="next-steps"></a>Volgende stappen

### <a name="get-hello-batch-file-conventions-library-for-net"></a>Hallo bestand conventies van Batch-bibliotheek voor .NET ophalen

Hallo bestand conventies van Batch-bibliotheek voor .NET is beschikbaar op [NuGet][nuget_package]. Hallo-bibliotheek breidt Hallo [CloudJob] [ net_cloudjob] en [CloudTask] [ net_cloudtask] klassen met nieuwe methoden. Zie ook Hallo [documentatie verwijst naar](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) voor Hallo bestand Conventions-bibliotheek.

Hallo [broncode] [ github_file_conventions] voor Hallo bestand conventies bibliotheek is beschikbaar op GitHub in Hallo Microsoft Azure SDK voor .NET-opslagplaats. 

### <a name="explore-other-approaches-for-persisting-output-data"></a>Andere benaderingen voor persistent maken uitvoergegevens verkennen

- Zie [Persist taak en uitvoer tooAzure opslag](batch-task-output.md) voor een overzicht van de persistente gegevens van de taak en taak.
- Zie [taak gegevens tooAzure opslag Hello API van Batch-service behouden](batch-task-output-files.md) toolearn hoe toouse Hallo API van Batch-service toopersist uitvoergegevens.

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "De uitvoerbestanden opgeslagen en opgeslagen logboeken selectoren in portal"
[2]: ./media/batch-task-output/task-output-02.png "Taakuitvoer blade in hello Azure-portal"
