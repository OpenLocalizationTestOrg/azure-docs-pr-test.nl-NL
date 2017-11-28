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
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a><span data-ttu-id="61b08-103">Taak behouden en gegevens tooAzure opslag met Hallo Batch bestand Conventions-bibliotheek voor .NET toopersist taak</span><span class="sxs-lookup"><span data-stu-id="61b08-103">Persist job and task data tooAzure Storage with hello Batch File Conventions library for .NET toopersist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="61b08-104">Eenzijdige toopersist taakgegevens zijn toouse hello [bestand conventies van Azure Batch-bibliotheek voor .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="61b08-104">One way toopersist task data is toouse hello [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="61b08-105">Hallo bestand conventies bibliotheek vereenvoudigt Hallo proces voor het opslaan van de uitvoer van de taak gegevens tooAzure opslag en het ophalen van het.</span><span class="sxs-lookup"><span data-stu-id="61b08-105">hello File Conventions library simplifies hello process of storing task output data tooAzure Storage and retrieving it.</span></span> <span data-ttu-id="61b08-106">Hallo bestand conventies bibliotheek in de taak en de client kunt u &mdash; taakcode voor persistent maken van bestanden en client toolist code en ze op te halen.</span><span class="sxs-lookup"><span data-stu-id="61b08-106">You can use hello File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code toolist and retrieve them.</span></span> <span data-ttu-id="61b08-107">Uw taakcode kunt ook Hallo bibliotheek tooretrieve Hallo uitvoer van de upstream-taken, zoals gebruiken in een [taakafhankelijkheden](batch-task-dependencies.md) scenario.</span><span class="sxs-lookup"><span data-stu-id="61b08-107">Your task code can also use hello library tooretrieve hello output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="61b08-108">tooretrieve uitvoerbestanden met Hallo bestand Conventions-bibliotheek, u kunt Hallo-bestanden voor een bepaalde taak of de taak vinden door deze door de ID en het doel.</span><span class="sxs-lookup"><span data-stu-id="61b08-108">tooretrieve output files with hello File Conventions library, you can locate hello files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="61b08-109">U hoeft niet tooknow Hallo namen of locaties van Hallo-bestanden.</span><span class="sxs-lookup"><span data-stu-id="61b08-109">You don't need tooknow hello names or locations of hello files.</span></span> <span data-ttu-id="61b08-110">U kunt bijvoorbeeld Hallo bestand conventies bibliotheek toolist alle tussenliggende bestanden gebruiken voor een bepaalde taak of een preview-bestand voor een bepaalde taak ophalen.</span><span class="sxs-lookup"><span data-stu-id="61b08-110">For example, you can use hello File Conventions library toolist all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="61b08-111">Hallo API van Batch-service ondersteunt persistent maken uitvoer gegevens tooAzure opslag voor taken en jobbeheertaken die worden uitgevoerd op de groepen die zijn gemaakt met de configuratie van de virtuele machine Hallo vanaf 2017-05-01-versie.</span><span class="sxs-lookup"><span data-stu-id="61b08-111">Starting with version 2017-05-01, hello Batch service API supports persisting output data tooAzure Storage for tasks and job manager tasks that run on pools created with hello virtual machine configuration.</span></span> <span data-ttu-id="61b08-112">Hallo API van Batch-service biedt een eenvoudige manier toopersist uitvoer van Hallo-code die een taak maakt en fungeert als een alternatieve toohello bestand Conventions-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="61b08-112">hello Batch service API provides a simple way toopersist output from within hello code that creates a task and serves as an alternative toohello File Conventions library.</span></span> <span data-ttu-id="61b08-113">U kunt uw Batch-client toepassingen toopersist uitvoer wijzigen zonder tooupdate Hallo toepassing die de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="61b08-113">You can modify your Batch client applications toopersist output without needing tooupdate hello application that your task is running.</span></span> <span data-ttu-id="61b08-114">Zie voor meer informatie [taak gegevens tooAzure opslag Hello API van Batch-service behouden](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="61b08-114">For more information, see [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a><span data-ttu-id="61b08-115">Wanneer kan ik Hallo bestand conventies bibliotheek toopersist-taakuitvoer gebruiken?</span><span class="sxs-lookup"><span data-stu-id="61b08-115">When do I use hello File Conventions library toopersist task output?</span></span>

<span data-ttu-id="61b08-116">Azure Batch voorziet in meer dan een manier toopersist taakuitvoer.</span><span class="sxs-lookup"><span data-stu-id="61b08-116">Azure Batch provides more than one way toopersist task output.</span></span> <span data-ttu-id="61b08-117">Hallo bestand conventies is aanbevolen geschikt toothese-scenario's:</span><span class="sxs-lookup"><span data-stu-id="61b08-117">hello File Conventions is best suited toothese scenarios:</span></span>

- <span data-ttu-id="61b08-118">Hallo-code voor Hallo toepassing of de taak toopersist bestanden met behulp van Hallo bestand conventies bibliotheek wordt uitgevoerd, kunt u eenvoudig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="61b08-118">You can easily modify hello code for hello application that your task is running toopersist files using hello File Conventions library.</span></span>
- <span data-ttu-id="61b08-119">Gewenste toostream gegevens tooAzure opslag terwijl Hallo taak nog actief.</span><span class="sxs-lookup"><span data-stu-id="61b08-119">You want toostream data tooAzure Storage while hello task is still running.</span></span>
- <span data-ttu-id="61b08-120">Wilt u toopersist gegevens uit toepassingen die zijn gemaakt met Hallo cloud serviceconfiguratie of Hallo Virtuele-machineconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="61b08-120">You want toopersist data from pools created with either hello cloud service configuration or hello virtual machine configuration.</span></span>
- <span data-ttu-id="61b08-121">Uw clienttoepassing of andere taken in Hallo van behoeften toolocate taken en downloaden van de taak uitvoerbestanden ID of met het doel.</span><span class="sxs-lookup"><span data-stu-id="61b08-121">Your client application or other tasks in hello job needs toolocate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="61b08-122">Wilt u de taakuitvoer tooview in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="61b08-122">You want tooview task output in hello Azure portal.</span></span>

<span data-ttu-id="61b08-123">Als uw scenario van die verschilt hierboven zijn vermeld, moet u mogelijk een andere benadering tooconsider.</span><span class="sxs-lookup"><span data-stu-id="61b08-123">If your scenario differs from those listed above, you may need tooconsider a different approach.</span></span> <span data-ttu-id="61b08-124">Zie voor meer informatie over andere opties voor het persistent maken van de taakuitvoer [Persist taak en uitvoer tooAzure opslag](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="61b08-124">For more information on other options for persisting task output, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-hello-batch-file-conventions-standard"></a><span data-ttu-id="61b08-125">Wat is Hallo Batch bestand conventies standaard?</span><span class="sxs-lookup"><span data-stu-id="61b08-125">What is hello Batch File Conventions standard?</span></span>

<span data-ttu-id="61b08-126">Hallo [Batch bestand conventies standaard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) biedt een schematische voor Hallo bestemming containers en blobs paden toowhich de uitvoerbestanden worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="61b08-126">hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for hello destination containers and blob paths toowhich your output files are written.</span></span> <span data-ttu-id="61b08-127">Bestanden persistente tooAzure opslag die toohello bestand conventies standaard voldoen zijn automatisch beschikbaar voor weergave in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="61b08-127">Files persisted tooAzure Storage that adhere toohello File Conventions standard are automatically available for viewing in hello Azure portal.</span></span> <span data-ttu-id="61b08-128">Hallo-portal is op de hoogte van de naamconventie Hallo en dus kan bestanden die tooit voldoen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="61b08-128">hello portal is aware of hello naming convention and so can display files that adhere tooit.</span></span>

<span data-ttu-id="61b08-129">Hallo bestand Conventions-bibliotheek voor .NET worden automatisch de uw storage-containers en uitvoerbestanden taak toohello bestand conventies standaard volgens naam.</span><span class="sxs-lookup"><span data-stu-id="61b08-129">hello File Conventions library for .NET automatically names your storage containers and task output files according toohello File Conventions standard.</span></span> <span data-ttu-id="61b08-130">Hallo bestand Conventions-bibliotheek biedt ook methoden tooquery uitvoerbestanden in Azure Storage op basis van toojob-ID, taak-ID of doel.</span><span class="sxs-lookup"><span data-stu-id="61b08-130">hello File Conventions library also provides methods tooquery output files in Azure Storage according toojob ID, task ID, or purpose.</span></span>   

<span data-ttu-id="61b08-131">Als u met een andere taal dan .NET ontwikkelt, kunt u implementeren Hallo bestand conventies standaard uzelf in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="61b08-131">If you are developing with a language other than .NET, you can implement hello File Conventions standard yourself in your application.</span></span> <span data-ttu-id="61b08-132">Zie voor meer informatie [over Hallo Batch bestand conventies standaard](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="61b08-132">For more information, see [About hello Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a><span data-ttu-id="61b08-133">Een Azure Storage-account tooyour Batch-account koppelen</span><span class="sxs-lookup"><span data-stu-id="61b08-133">Link an Azure Storage account tooyour Batch account</span></span>

<span data-ttu-id="61b08-134">toopersist uitvoer gegevens tooAzure opslag met behulp van Hallo bestand conventies bibliotheek, moet u eerst een Azure Storage-account tooyour Batch-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="61b08-134">toopersist output data tooAzure Storage using hello File Conventions library, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="61b08-135">Als u dit nog niet hebt gedaan, een opslag-account tooyour Batch-account koppelen via Hallo [Azure-portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="61b08-135">If you haven't done so already, link a Storage account tooyour Batch account by using hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="61b08-136">Navigeer tooyour Batch-account in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="61b08-136">Navigate tooyour Batch account in hello Azure portal.</span></span> 
2. <span data-ttu-id="61b08-137">Onder **instellingen**, selecteer **Opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="61b08-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="61b08-138">Als u nog geen een opslagaccount die is gekoppeld aan uw Batch-account, klikt u op **Storage-Account (geen)**.</span><span class="sxs-lookup"><span data-stu-id="61b08-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="61b08-139">Selecteer een opslagaccount in de lijst Hallo voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="61b08-139">Select a Storage account from hello list for your subscription.</span></span> <span data-ttu-id="61b08-140">Voor de beste prestaties gebruikt u een Azure Storage-account dat in Hallo dezelfde regio als Hallo Batch-account waarop uw taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="61b08-140">For best performance, use an Azure Storage account that is in hello same region as hello Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="61b08-141">Uitvoergegevens behouden</span><span class="sxs-lookup"><span data-stu-id="61b08-141">Persist output data</span></span>

<span data-ttu-id="61b08-142">taak toopersist en uitvoergegevens met Hallo bestand Conventions-bibliotheek, een container maken in Azure Storage en Hallo uitvoer toohello container opslaan.</span><span class="sxs-lookup"><span data-stu-id="61b08-142">toopersist job and task output data with hello File Conventions library, create a container in Azure Storage, then save hello output toohello container.</span></span> <span data-ttu-id="61b08-143">Gebruik Hallo [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in uw taak code tooupload Hallo taak uitvoer toohello-container.</span><span class="sxs-lookup"><span data-stu-id="61b08-143">Use hello [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code tooupload hello task output toohello container.</span></span> 

<span data-ttu-id="61b08-144">Zie voor meer informatie over het werken met containers en blobs in Azure Storage [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="61b08-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="61b08-145">Alle uitvoerwaarden van taak en persistent is gemaakt met de Hallo bestand conventies bibliotheek worden opgeslagen in dezelfde container Hallo.</span><span class="sxs-lookup"><span data-stu-id="61b08-145">All job and task outputs persisted with hello File Conventions library are stored in hello same container.</span></span> <span data-ttu-id="61b08-146">Als een groot aantal taken probeert toopersist bestanden op Hallo dezelfde tijd [opslag beperking limieten](../storage/common/storage-performance-checklist.md#blobs) kan worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="61b08-146">If a large number of tasks try toopersist files at hello same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="61b08-147">Opslagcontainer maken</span><span class="sxs-lookup"><span data-stu-id="61b08-147">Create storage container</span></span>

<span data-ttu-id="61b08-148">toopersist taak uitvoer tooAzure opslag, eerst een container maken door het aanroepen van [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="61b08-148">toopersist task output tooAzure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="61b08-149">Deze uitbreidingsmethode heeft een [CloudStorageAccount] [ net_cloudstorageaccount] -object als parameter.</span><span class="sxs-lookup"><span data-stu-id="61b08-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="61b08-150">Een container met de naam volgens toohello bestand conventies standaard zo in dat de inhoud ervan kunnen worden gedetecteerd door Azure portal en Hallo ophalen besproken methoden verderop in Hallo artikel Hallo wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="61b08-150">It creates a container named according toohello File Conventions standard,so that its contents are discoverable by hello Azure portal and hello retrieval methods discussed later in hello article.</span></span>

<span data-ttu-id="61b08-151">U doorgaans Hallo code toocreate een container plaatsen in uw clienttoepassing &mdash; Hallo toepassing waarmee uw pools, jobs en taken worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="61b08-151">You typically place hello code toocreate a container in your client application &mdash; hello application that creates your pools, jobs, and tasks.</span></span>

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

### <a name="store-task-outputs"></a><span data-ttu-id="61b08-152">Taakuitvoer Store</span><span class="sxs-lookup"><span data-stu-id="61b08-152">Store task outputs</span></span>

<span data-ttu-id="61b08-153">Nu dat u een container in Azure Storage hebt voorbereid, taken uitvoer toohello container kunnen opslaan met behulp van Hallo [TaskOutputStorage] [ net_taskoutputstorage] klasse gevonden in Hallo bestand Conventions-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="61b08-153">Now that you've prepared a container in Azure Storage, tasks can save output toohello container by using hello [TaskOutputStorage][net_taskoutputstorage] class found in hello File Conventions library.</span></span>

<span data-ttu-id="61b08-154">In uw taakcode maakt u eerst een [TaskOutputStorage] [ net_taskoutputstorage] object wanneer Hallo taak voltooid zijn werk, en roep vervolgens Hallo [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] methode toosave de uitvoer tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="61b08-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when hello task has completed its work, call hello [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method toosave its output tooAzure Storage.</span></span>

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

<span data-ttu-id="61b08-155">Hallo `kind` parameter Hallo [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) methode categoriseert Hallo persistent bestanden.</span><span class="sxs-lookup"><span data-stu-id="61b08-155">hello `kind` parameter of hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes hello persisted files.</span></span> <span data-ttu-id="61b08-156">Er zijn vier vooraf gedefinieerde [TaskOutputKind] [ net_taskoutputkind] typen: `TaskOutput`, `TaskPreview`, `TaskLog`, en `TaskIntermediate.` ook kunt u aangepaste categorieën van uitvoer.</span><span class="sxs-lookup"><span data-stu-id="61b08-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="61b08-157">Deze uitvoer-typen kunnen u toospecify welk type uitvoer toolist als u later Batch een query voor Hallo uitvoerwaarden van een bepaalde taak persistent.</span><span class="sxs-lookup"><span data-stu-id="61b08-157">These output types allow you toospecify which type of outputs toolist when you later query Batch for hello persisted outputs of a given task.</span></span> <span data-ttu-id="61b08-158">Wanneer u Hallo uitvoer voor een taak wilt weergeven, kunt u met andere woorden, Hallo-lijst op een van de Hallo uitvoer typen filteren.</span><span class="sxs-lookup"><span data-stu-id="61b08-158">In other words, when you list hello outputs for a task, you can filter hello list on one of hello output types.</span></span> <span data-ttu-id="61b08-159">Bijvoorbeeld, "Geef me Hallo *preview* uitvoer voor de taak *109*."</span><span class="sxs-lookup"><span data-stu-id="61b08-159">For example, "Give me hello *preview* output for task *109*."</span></span> <span data-ttu-id="61b08-160">Meer informatie over het weergeven en ophalen van de uitvoer wordt weergegeven in [uitvoer ophalen](#retrieve-output) verderop in Hallo artikel.</span><span class="sxs-lookup"><span data-stu-id="61b08-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in hello article.</span></span>

> [!TIP]
> <span data-ttu-id="61b08-161">Hallo uitvoer soort bepaalt ook waar in hello Azure portal een bepaald bestand wordt weergegeven: *TaskOutput*-gecategoriseerde bestanden worden weergegeven onder **taak uitvoerbestanden**, en *TaskLog*-bestanden worden weergegeven onder **logboeken van de taak**.</span><span class="sxs-lookup"><span data-stu-id="61b08-161">hello output kind also determines where in hello Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="61b08-162">Opslaan van de taak uitvoer</span><span class="sxs-lookup"><span data-stu-id="61b08-162">Store job outputs</span></span>

<span data-ttu-id="61b08-163">Bovendien toostoring taakuitvoer, kunt u opslaan Hallo-uitvoer die zijn gekoppeld aan een volledige-taak.</span><span class="sxs-lookup"><span data-stu-id="61b08-163">In addition toostoring task outputs, you can store hello outputs associated with an entire job.</span></span> <span data-ttu-id="61b08-164">In Hallo samenvoegen taak van een film rendering taak kunt u Hallo volledig gerenderde film kan behouden als de taakuitvoer van een.</span><span class="sxs-lookup"><span data-stu-id="61b08-164">For example, in hello merge task of a movie rendering job, you could persist hello fully rendered movie as a job output.</span></span> <span data-ttu-id="61b08-165">Als de taak is voltooid, kunt uw clienttoepassing lijst Hallo outputs voor Hallo-taak ophalen en is niet nodig tooquery Hallo afzonderlijke taken.</span><span class="sxs-lookup"><span data-stu-id="61b08-165">When your job is completed, your client application can list and retrieve hello outputs for hello job, and does not need tooquery hello individual tasks.</span></span>

<span data-ttu-id="61b08-166">Taakuitvoer opslaan door de aanroepende Hallo [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] methode, en geef Hallo [JobOutputKind] [ net_joboutputkind] en bestandsnaam:</span><span class="sxs-lookup"><span data-stu-id="61b08-166">Store job output by calling hello [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify hello [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="61b08-167">Net als bij Hallo **TaskOutputKind** type voor de taak uitvoer, u Hallo [JobOutputKind] [ net_joboutputkind] type toocategorize een taak de opgeslagen bestanden.</span><span class="sxs-lookup"><span data-stu-id="61b08-167">As with hello **TaskOutputKind** type for task outputs, you use hello [JobOutputKind][net_joboutputkind] type toocategorize a job's persisted files.</span></span> <span data-ttu-id="61b08-168">Deze parameter kunt u de query toolater voor (lijst) voor een specifiek type uitvoer.</span><span class="sxs-lookup"><span data-stu-id="61b08-168">This parameter allows you toolater query for (list) a specific type of output.</span></span> <span data-ttu-id="61b08-169">Hallo **JobOutputKind** type bevat zowel uitvoer als preview-categorieën en biedt ondersteuning voor het maken van aangepaste categorieën.</span><span class="sxs-lookup"><span data-stu-id="61b08-169">hello **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="61b08-170">Taak logboeken worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="61b08-170">Store task logs</span></span>

<span data-ttu-id="61b08-171">Bovendien toopersisting dat door een bestandsopslag toodurable wanneer een taak of de taak is voltooid, moet u mogelijk toopersist-bestanden die zijn bijgewerkt tijdens de uitvoering van een taak Hallo &mdash; logboekbestanden of `stdout.txt` en `stderr.txt`, bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="61b08-171">In addition toopersisting a file toodurable storage when a task or job completes, you may need toopersist files that are updated during hello execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="61b08-172">Voor dit doel Hallo bestand conventies van Azure Batch-bibliotheek biedt een Hallo [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] methode.</span><span class="sxs-lookup"><span data-stu-id="61b08-172">For this purpose, hello Azure Batch File Conventions library provides hello [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="61b08-173">Met [SaveTrackedAsync][net_savetrackedasync], kunt u updates tooa bestand op Hallo-knooppunt (met een interval dat u opgeeft) bijhouden en persistent maken die updates tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="61b08-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates tooa file on hello node (at an interval that you specify) and persist those updates tooAzure Storage.</span></span>

<span data-ttu-id="61b08-174">In de Hallo codefragment te volgen, gebruiken we [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage elke 15 seconden tijdens het uitvoeren van taak Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="61b08-174">In hello following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage every 15 seconds during hello execution of hello task:</span></span>

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

<span data-ttu-id="61b08-175">Hallo opmerkingen sectie `Code tooprocess data and produce output file(s)` is een tijdelijke aanduiding voor Hallo-code die uw taak normaal kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="61b08-175">hello commented section `Code tooprocess data and produce output file(s)` is a placeholder for hello code that your task would normally perform.</span></span> <span data-ttu-id="61b08-176">Bijvoorbeeld wellicht code die gegevens uit Azure Storage downloadt en transformatie of berekening op deze uitvoert.</span><span class="sxs-lookup"><span data-stu-id="61b08-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="61b08-177">Hallo belangrijk onderdeel van dit fragment is te demonstreren hoe u kunt laten teruglopen deze code in een `using` blok tooperiodically bijwerken van een bestand met [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="61b08-177">hello important part of this snippet is demonstrating how you can wrap such code in a `using` block tooperiodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="61b08-178">Hallo knooppunt agent is een programma dat wordt uitgevoerd op elk knooppunt in de pool Hallo en Hallo command en control interface vormt tussen Hallo-knooppunt en Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="61b08-178">hello node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="61b08-179">Hallo `Task.Delay` aanroep is vereist bij het einde van dit Hallo `using` blok tooensure dat knooppunt agent Hallo tijd tooflush Hallo inhoud van de standaard toohello stdout.txt bestand op Hallo knooppunt heeft.</span><span class="sxs-lookup"><span data-stu-id="61b08-179">hello `Task.Delay` call is required at hello end of this `using` block tooensure that hello node agent has time tooflush hello contents of standard out toohello stdout.txt file on hello node.</span></span> <span data-ttu-id="61b08-180">Zonder deze vertraging is het mogelijk toomiss Hallo laatste enkele seconden van uitvoer.</span><span class="sxs-lookup"><span data-stu-id="61b08-180">Without this delay, it is possible toomiss hello last few seconds of output.</span></span> <span data-ttu-id="61b08-181">Deze vertraging is mogelijk niet vereist voor alle bestanden.</span><span class="sxs-lookup"><span data-stu-id="61b08-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="61b08-182">Wanneer het inschakelen van bestand bijhouden met **SaveTrackedAsync**, alleen *voegt* toohello bijgehouden bestand persistente tooAzure opslag zijn.</span><span class="sxs-lookup"><span data-stu-id="61b08-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* toohello tracked file are persisted tooAzure Storage.</span></span> <span data-ttu-id="61b08-183">Deze methode alleen gebruiken voor het bijhouden van de logboekbestanden niet draaien of andere bestanden die zijn geschreven toowith operations toohello einde van Hallo-bestand toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="61b08-183">Use this method only for tracking non-rotating log files or other files that are written toowith append operations toohello end of hello file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="61b08-184">Uitvoergegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="61b08-184">Retrieve output data</span></span>

<span data-ttu-id="61b08-185">Wanneer u de persistente uitvoer met behulp van hello Azure Batch-bestand conventies bibliotheek ophaalt, kunt u dat doen op een taak en taak-gericht manier.</span><span class="sxs-lookup"><span data-stu-id="61b08-185">When you retrieve your persisted output using hello Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="61b08-186">U kunt aanvragen Hallo uitvoer voor de opgegeven taak zonder tooknow het pad in Azure Storage of zelfs de naam van het bestand.</span><span class="sxs-lookup"><span data-stu-id="61b08-186">You can request hello output for given task or job without needing tooknow its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="61b08-187">U kunt in plaats daarvan uitvoerbestanden aanvragen door de taak of taak-ID.</span><span class="sxs-lookup"><span data-stu-id="61b08-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="61b08-188">Hallo volgende codefragment doorlopen taken van een taak, wordt bepaalde informatie over de uitvoerbestanden Hallo voor Hallo taak afgedrukt, en vervolgens de bestanden uit Storage downloadt.</span><span class="sxs-lookup"><span data-stu-id="61b08-188">hello following code snippet iterates through a job's tasks, prints some information about hello output files for hello task, and then downloads its files from Storage.</span></span>

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

## <a name="view-output-files-in-hello-azure-portal"></a><span data-ttu-id="61b08-189">De uitvoerbestanden weergeven in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="61b08-189">View output files in hello Azure portal</span></span>

<span data-ttu-id="61b08-190">Hello Azure-portal weergegeven taak uitvoerbestanden en logboeken die persistente tooa zijn gekoppelde Azure Storage-account met behulp van Hallo [Batch bestand conventies standaard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="61b08-190">hello Azure portal displays task output files and logs that are persisted tooa linked Azure Storage account using hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="61b08-191">U kunt ook zelf deze conventies implementeren in een taal van uw keuze Hallo of kunt u Hallo bestand conventies bibliotheek in uw .NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="61b08-191">You can implement these conventions yourself in hello a language of your choice, or you can use hello File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="61b08-192">tooenable hello weergave van de uitvoerbestanden in Hallo-portal, moeten Hallo volgens de vereisten voldoen:</span><span class="sxs-lookup"><span data-stu-id="61b08-192">tooenable hello display of your output files in hello portal, you must satisfy hello following requirements:</span></span>

1. <span data-ttu-id="61b08-193">[Een Azure Storage-account koppelen](#requirement-linked-storage-account) tooyour Batch-account.</span><span class="sxs-lookup"><span data-stu-id="61b08-193">[Link an Azure Storage account](#requirement-linked-storage-account) tooyour Batch account.</span></span>
2. <span data-ttu-id="61b08-194">Vooraf gedefinieerde toohello naamgevingsregels voor Storage-containers en bestanden voldoen als uitvoer persistent maken.</span><span class="sxs-lookup"><span data-stu-id="61b08-194">Adhere toohello predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="61b08-195">U vindt Hallo definitie van deze conventies in Hallo bestand conventies bibliotheek [Leesmij][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="61b08-195">You can find hello definition of these conventions in hello File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="61b08-196">Als u Hallo [Azure Batch-bestand conventies] [ nuget_package] bibliotheek toopersist uw uitvoer uw bestanden blijven aanwezig op basis van toohello bestand conventies standaard.</span><span class="sxs-lookup"><span data-stu-id="61b08-196">If you use hello [Azure Batch File Conventions][nuget_package] library toopersist your output, your files are persisted according toohello File Conventions standard.</span></span>

<span data-ttu-id="61b08-197">taakuitvoer tooview-bestanden en geregistreerd in hello Azure-portal, gaat u toohello taak waarvan de uitvoer u geïnteresseerd bent in, klik dan ofwel **opgeslagen uitvoerbestanden** of **opgeslagen logboeken**.</span><span class="sxs-lookup"><span data-stu-id="61b08-197">tooview task output files and logs in hello Azure portal, navigate toohello task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="61b08-198">Deze afbeelding ziet u Hallo **uitvoerbestanden opgeslagen** voor Hallo-taak met ID '007':</span><span class="sxs-lookup"><span data-stu-id="61b08-198">This image shows hello **Saved output files** for hello task with ID "007":</span></span>

<span data-ttu-id="61b08-199">![Taakuitvoer blade in hello Azure-portal][2]</span><span class="sxs-lookup"><span data-stu-id="61b08-199">![Task outputs blade in hello Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="61b08-200">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="61b08-200">Code sample</span></span>

<span data-ttu-id="61b08-201">Hallo [PersistOutputs] [ github_persistoutputs] voorbeeldproject is een van de Hallo [Azure Batch-codevoorbeelden] [ github_samples] op GitHub.</span><span class="sxs-lookup"><span data-stu-id="61b08-201">hello [PersistOutputs][github_persistoutputs] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="61b08-202">Deze Visual Studio-oplossing laat zien hoe toouse hello Azure Batch-bestand conventies bibliotheek toopersist taak toodurable opslag uitvoer.</span><span class="sxs-lookup"><span data-stu-id="61b08-202">This Visual Studio solution demonstrates how toouse hello Azure Batch File Conventions library toopersist task output toodurable storage.</span></span> <span data-ttu-id="61b08-203">toorun hello steekproef, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="61b08-203">toorun hello sample, follow these steps:</span></span>

1. <span data-ttu-id="61b08-204">Open Hallo-project in **Visual Studio 2015 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="61b08-204">Open hello project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="61b08-205">Toevoegen van uw Batch- en Storage **accountreferenties** te**AccountSettings.settings** hello Microsoft.Azure.Batch.Samples.Common project.</span><span class="sxs-lookup"><span data-stu-id="61b08-205">Add your Batch and Storage **account credentials** too**AccountSettings.settings** in hello Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="61b08-206">**Bouwen** (maar niet worden uitgevoerd) Hallo oplossing.</span><span class="sxs-lookup"><span data-stu-id="61b08-206">**Build** (but do not run) hello solution.</span></span> <span data-ttu-id="61b08-207">Herstel alle NuGet-pakketten als daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="61b08-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="61b08-208">Gebruik hello Azure portal tooupload een [toepassingspakket](batch-application-packages.md) voor **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="61b08-208">Use hello Azure portal tooupload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="61b08-209">Hallo omvatten `PersistOutputsTask.exe` en afhankelijke assembly's in Hallo ZIP-pakket, set Hallo toepassings-ID te 'PersistOutputsTask' en de toepassing hello Pakketversie te "1.0".</span><span class="sxs-lookup"><span data-stu-id="61b08-209">Include hello `PersistOutputsTask.exe` and its dependent assemblies in hello .zip package, set hello application ID too"PersistOutputsTask", and hello application package version too"1.0".</span></span>
5. <span data-ttu-id="61b08-210">**Start** (uitvoeren) Hallo **PersistOutputs** project.</span><span class="sxs-lookup"><span data-stu-id="61b08-210">**Start** (run) hello **PersistOutputs** project.</span></span>
6. <span data-ttu-id="61b08-211">Wanneer de vraag toochoose Hallo persistentie technologie toouse voor actieve Hallo voorbeeld invoert **1** toorun Hallo voorbeeld met behulp van Hallo bestand conventies bibliotheek toopersist de taakuitvoer.</span><span class="sxs-lookup"><span data-stu-id="61b08-211">When prompted toochoose hello persistence technology toouse for running hello sample, enter **1** toorun hello sample using hello File Conventions library toopersist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="61b08-212">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="61b08-212">Next steps</span></span>

### <a name="get-hello-batch-file-conventions-library-for-net"></a><span data-ttu-id="61b08-213">Hallo bestand conventies van Batch-bibliotheek voor .NET ophalen</span><span class="sxs-lookup"><span data-stu-id="61b08-213">Get hello Batch File Conventions library for .NET</span></span>

<span data-ttu-id="61b08-214">Hallo bestand conventies van Batch-bibliotheek voor .NET is beschikbaar op [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="61b08-214">hello Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="61b08-215">Hallo-bibliotheek breidt Hallo [CloudJob] [ net_cloudjob] en [CloudTask] [ net_cloudtask] klassen met nieuwe methoden.</span><span class="sxs-lookup"><span data-stu-id="61b08-215">hello library extends hello [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="61b08-216">Zie ook Hallo [documentatie verwijst naar](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) voor Hallo bestand Conventions-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="61b08-216">Also see hello [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for hello File Conventions library.</span></span>

<span data-ttu-id="61b08-217">Hallo [broncode] [ github_file_conventions] voor Hallo bestand conventies bibliotheek is beschikbaar op GitHub in Hallo Microsoft Azure SDK voor .NET-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="61b08-217">hello [source code][github_file_conventions] for hello File Conventions library is available on GitHub in hello Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="61b08-218">Andere benaderingen voor persistent maken uitvoergegevens verkennen</span><span class="sxs-lookup"><span data-stu-id="61b08-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="61b08-219">Zie [Persist taak en uitvoer tooAzure opslag](batch-task-output.md) voor een overzicht van de persistente gegevens van de taak en taak.</span><span class="sxs-lookup"><span data-stu-id="61b08-219">See [Persist job and task output tooAzure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="61b08-220">Zie [taak gegevens tooAzure opslag Hello API van Batch-service behouden](batch-task-output-files.md) toolearn hoe toouse Hallo API van Batch-service toopersist uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="61b08-220">See [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md) toolearn how toouse hello Batch service API toopersist output data.</span></span>

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
