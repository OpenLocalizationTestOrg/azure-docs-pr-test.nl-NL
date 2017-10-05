---
title: Taak en uitvoer naar Azure Storage met de bestand Conventions-bibliotheek voor .NET - Azure Batch behouden | Microsoft Docs
description: Informatie over het bestand conventies van Azure Batch-bibliotheek voor .NET gebruiken voor het behouden van de Batch-taak en de taak uitvoer naar Azure Storage en de persistente uitvoer weergeven in de Azure portal.
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
ms.openlocfilehash: a9de327c20463469bc91d9720aa17333a36f919e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="persist-job-and-task-data-to-azure-storage-with-the-batch-file-conventions-library-for-net-to-persist"></a><span data-ttu-id="bd878-103">Behouden van de taak en gegevens naar Azure Storage met de Batch-bestand Conventions-bibliotheek voor .NET voor het persistent maken</span><span class="sxs-lookup"><span data-stu-id="bd878-103">Persist job and task data to Azure Storage with the Batch File Conventions library for .NET to persist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="bd878-104">Een manier om taakgegevens is met de [bestand conventies van Azure Batch-bibliotheek voor .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="bd878-104">One way to persist task data is to use the [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="bd878-105">De bibliotheek bestand conventies vereenvoudigt het proces voor het opslaan van taak uitvoergegevens naar Azure Storage en het ophalen van het.</span><span class="sxs-lookup"><span data-stu-id="bd878-105">The File Conventions library simplifies the process of storing task output data to Azure Storage and retrieving it.</span></span> <span data-ttu-id="bd878-106">U kunt de bibliotheek bestanden in de taak en de client &mdash; in taakcode voor persistent maken van bestanden en in clientcode weergeven en ophalen van deze.</span><span class="sxs-lookup"><span data-stu-id="bd878-106">You can use the File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code to list and retrieve them.</span></span> <span data-ttu-id="bd878-107">Uw taakcode kunt ook de bibliotheek gebruiken voor het ophalen van de uitvoer van de upstream-taken, zoals een [taakafhankelijkheden](batch-task-dependencies.md) scenario.</span><span class="sxs-lookup"><span data-stu-id="bd878-107">Your task code can also use the library to retrieve the output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="bd878-108">Voor het ophalen van uitvoerbestanden met de bibliotheek bestand verdragen, kunt u de bestanden voor een bepaalde taak of de taak vinden door deze door de ID en het doel.</span><span class="sxs-lookup"><span data-stu-id="bd878-108">To retrieve output files with the File Conventions library, you can locate the files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="bd878-109">U hoeft niet te weten de namen of locaties van de bestanden.</span><span class="sxs-lookup"><span data-stu-id="bd878-109">You don't need to know the names or locations of the files.</span></span> <span data-ttu-id="bd878-110">U kunt bijvoorbeeld gebruikmaken van de tapewisselaar bestand conventies voor een lijst met alle tussenliggende bestanden voor een bepaalde taak of een preview-bestand voor een bepaalde taak ophalen.</span><span class="sxs-lookup"><span data-stu-id="bd878-110">For example, you can use the File Conventions library to list all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="bd878-111">Vanaf versie 2017-05-01 ondersteunt de Batch-service-API persistent maken uitvoergegevens naar Azure Storage voor taken en jobbeheertaken die worden uitgevoerd op de groepen die zijn gemaakt met de configuratie van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bd878-111">Starting with version 2017-05-01, the Batch service API supports persisting output data to Azure Storage for tasks and job manager tasks that run on pools created with the virtual machine configuration.</span></span> <span data-ttu-id="bd878-112">De API van Batch-service biedt een eenvoudige manier om vast te leggen van de uitvoer van de code die een taak maakt en fungeert als een alternatief voor het bestand Conventions-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="bd878-112">The Batch service API provides a simple way to persist output from within the code that creates a task and serves as an alternative to the File Conventions library.</span></span> <span data-ttu-id="bd878-113">Uw Batch-clienttoepassingen om vast te leggen uitvoer zonder bijwerken van de toepassing die de taak wordt uitgevoerd, kunt u wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bd878-113">You can modify your Batch client applications to persist output without needing to update the application that your task is running.</span></span> <span data-ttu-id="bd878-114">Zie voor meer informatie [Persist taakgegevens naar Azure Storage met de Batch-service API](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="bd878-114">For more information, see [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-the-file-conventions-library-to-persist-task-output"></a><span data-ttu-id="bd878-115">Wanneer gebruik de bibliotheek bestand verdragen om vast te leggen van de uitvoer van de taak?</span><span class="sxs-lookup"><span data-stu-id="bd878-115">When do I use the File Conventions library to persist task output?</span></span>

<span data-ttu-id="bd878-116">Azure Batch biedt meer dan één manier om vast te leggen van de uitvoer van de taak.</span><span class="sxs-lookup"><span data-stu-id="bd878-116">Azure Batch provides more than one way to persist task output.</span></span> <span data-ttu-id="bd878-117">De conventies bestand is het meest geschikt is voor deze scenario's:</span><span class="sxs-lookup"><span data-stu-id="bd878-117">The File Conventions is best suited to these scenarios:</span></span>

- <span data-ttu-id="bd878-118">U kunt de code voor de toepassing die de taak wordt uitgevoerd om te blijven behouden bestanden met behulp van de bibliotheek bestand conventies eenvoudig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bd878-118">You can easily modify the code for the application that your task is running to persist files using the File Conventions library.</span></span>
- <span data-ttu-id="bd878-119">Wilt u van stroomgegevens naar Azure Storage terwijl de taak nog actief.</span><span class="sxs-lookup"><span data-stu-id="bd878-119">You want to stream data to Azure Storage while the task is still running.</span></span>
- <span data-ttu-id="bd878-120">Wilt u gegevens uit toepassingen die zijn gemaakt met de configuratie van de cloud-service of de configuratie van de virtuele machine persistent maken.</span><span class="sxs-lookup"><span data-stu-id="bd878-120">You want to persist data from pools created with either the cloud service configuration or the virtual machine configuration.</span></span>
- <span data-ttu-id="bd878-121">Uw clienttoepassing of andere taken in de taak moet om te zoeken en downloaden van de taak uitvoerbestanden ID of met het doel.</span><span class="sxs-lookup"><span data-stu-id="bd878-121">Your client application or other tasks in the job needs to locate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="bd878-122">U wilt weergeven van uitvoer van de taak in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bd878-122">You want to view task output in the Azure portal.</span></span>

<span data-ttu-id="bd878-123">Als uw scenario van die verschilt hierboven zijn vermeld, moet u wellicht een andere benadering overwegen.</span><span class="sxs-lookup"><span data-stu-id="bd878-123">If your scenario differs from those listed above, you may need to consider a different approach.</span></span> <span data-ttu-id="bd878-124">Zie voor meer informatie over andere opties voor het persistent maken van de taakuitvoer [behouden van de taak en uitvoer naar Azure Storage](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="bd878-124">For more information on other options for persisting task output, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-the-batch-file-conventions-standard"></a><span data-ttu-id="bd878-125">Wat is de standaard Batch bestand conventies?</span><span class="sxs-lookup"><span data-stu-id="bd878-125">What is the Batch File Conventions standard?</span></span>

<span data-ttu-id="bd878-126">De [Batch bestand conventies standaard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) biedt een schematische naam voor de bestemming containers en blobs paden waarnaar de uitvoerbestanden worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="bd878-126">The [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for the destination containers and blob paths to which your output files are written.</span></span> <span data-ttu-id="bd878-127">Bestanden die zijn opgeslagen in Azure Storage die voldoen aan de bestanden standaard automatisch beschikbaar zijn voor weergave in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bd878-127">Files persisted to Azure Storage that adhere to the File Conventions standard are automatically available for viewing in the Azure portal.</span></span> <span data-ttu-id="bd878-128">De portal is op de hoogte van de naamconventie en dus kan bestanden die aan deze voldoen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bd878-128">The portal is aware of the naming convention and so can display files that adhere to it.</span></span>

<span data-ttu-id="bd878-129">Het bestand Conventions-bibliotheek voor .NET worden automatisch weergegeven in de naam van een uw storage-containers en uitvoerbestanden taak volgens de conventies bestand standaard.</span><span class="sxs-lookup"><span data-stu-id="bd878-129">The File Conventions library for .NET automatically names your storage containers and task output files according to the File Conventions standard.</span></span> <span data-ttu-id="bd878-130">De bibliotheek bestand conventies biedt ook methoden voor het opvragen van de uitvoerbestanden in Azure Storage volgens de taak-ID, taak-ID of doel.</span><span class="sxs-lookup"><span data-stu-id="bd878-130">The File Conventions library also provides methods to query output files in Azure Storage according to job ID, task ID, or purpose.</span></span>   

<span data-ttu-id="bd878-131">Als u met een andere taal dan .NET ontwikkelt, kunt u implementeren de bestanden standaard uzelf in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="bd878-131">If you are developing with a language other than .NET, you can implement the File Conventions standard yourself in your application.</span></span> <span data-ttu-id="bd878-132">Zie voor meer informatie [de conventies voor Batch-bestand standaard](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="bd878-132">For more information, see [About the Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-to-your-batch-account"></a><span data-ttu-id="bd878-133">Een Azure Storage-account koppelen aan uw Batch-account</span><span class="sxs-lookup"><span data-stu-id="bd878-133">Link an Azure Storage account to your Batch account</span></span>

<span data-ttu-id="bd878-134">Om te blijven behouden uitvoergegevens naar Azure Storage met behulp van het bestand Conventions-bibliotheek, moet u eerst een Azure Storage-account koppelen aan uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="bd878-134">To persist output data to Azure Storage using the File Conventions library, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="bd878-135">Als u dit nog niet hebt gedaan, koppelt u een opslagaccount aan uw Batch-account met behulp van de [Azure-portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="bd878-135">If you haven't done so already, link a Storage account to your Batch account by using the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="bd878-136">Ga in Azure Portal naar uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="bd878-136">Navigate to your Batch account in the Azure portal.</span></span> 
2. <span data-ttu-id="bd878-137">Onder **instellingen**, selecteer **Opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="bd878-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="bd878-138">Als u nog geen een opslagaccount die is gekoppeld aan uw Batch-account, klikt u op **Storage-Account (geen)**.</span><span class="sxs-lookup"><span data-stu-id="bd878-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="bd878-139">Selecteer een opslagaccount in de lijst voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="bd878-139">Select a Storage account from the list for your subscription.</span></span> <span data-ttu-id="bd878-140">Gebruik een Azure Storage-account dat zich in dezelfde regio bevinden als het Batch-account waarop uw taken worden uitgevoerd voor de beste prestaties.</span><span class="sxs-lookup"><span data-stu-id="bd878-140">For best performance, use an Azure Storage account that is in the same region as the Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="bd878-141">Uitvoergegevens behouden</span><span class="sxs-lookup"><span data-stu-id="bd878-141">Persist output data</span></span>

<span data-ttu-id="bd878-142">Om te blijven behouden taak en uitvoergegevens met de bibliotheek bestand verdragen, een container maken in Azure Storage en sla vervolgens de uitvoer naar de container.</span><span class="sxs-lookup"><span data-stu-id="bd878-142">To persist job and task output data with the File Conventions library, create a container in Azure Storage, then save the output to the container.</span></span> <span data-ttu-id="bd878-143">Gebruik de [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in uw taakcode voor het uploaden van de uitvoer van de taak voor de container.</span><span class="sxs-lookup"><span data-stu-id="bd878-143">Use the [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code to upload the task output to the container.</span></span> 

<span data-ttu-id="bd878-144">Zie voor meer informatie over het werken met containers en blobs in Azure Storage [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="bd878-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="bd878-145">Alle uitvoerwaarden van taak en persistent is gemaakt met het bestand conventies bibliotheek worden opgeslagen in dezelfde container.</span><span class="sxs-lookup"><span data-stu-id="bd878-145">All job and task outputs persisted with the File Conventions library are stored in the same container.</span></span> <span data-ttu-id="bd878-146">Als een groot aantal taken voor het persistent maken van bestanden op hetzelfde moment probeert [opslag beperking limieten](../storage/common/storage-performance-checklist.md#blobs) kan worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="bd878-146">If a large number of tasks try to persist files at the same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="bd878-147">Opslagcontainer maken</span><span class="sxs-lookup"><span data-stu-id="bd878-147">Create storage container</span></span>

<span data-ttu-id="bd878-148">Om te blijven behouden taakuitvoer naar Azure Storage, eerst een container maken door het aanroepen van [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="bd878-148">To persist task output to Azure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="bd878-149">Deze uitbreidingsmethode heeft een [CloudStorageAccount] [ net_cloudstorageaccount] -object als parameter.</span><span class="sxs-lookup"><span data-stu-id="bd878-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="bd878-150">Wordt gemaakt van een container met de naam volgens de standaard bestand verdragen, zodat de inhoud ervan kunnen gevonden door de Azure-portal worden en de ophalen-methoden die later in dit artikel wordt besproken.</span><span class="sxs-lookup"><span data-stu-id="bd878-150">It creates a container named according to the File Conventions standard,so that its contents are discoverable by the Azure portal and the retrieval methods discussed later in the article.</span></span>

<span data-ttu-id="bd878-151">U doorgaans de code voor het maken van een container in uw clienttoepassing plaatsen &mdash; de toepassing die wordt gemaakt van uw pools, jobs en taken.</span><span class="sxs-lookup"><span data-stu-id="bd878-151">You typically place the code to create a container in your client application &mdash; the application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference to the linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create the blob storage container for the outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="bd878-152">Taakuitvoer Store</span><span class="sxs-lookup"><span data-stu-id="bd878-152">Store task outputs</span></span>

<span data-ttu-id="bd878-153">Nu dat u een container in Azure Storage hebt voorbereid, taken uitvoer naar de container kunnen opslaan met behulp van de [TaskOutputStorage] [ net_taskoutputstorage] klasse gevonden in de bibliotheek bestand verdragen.</span><span class="sxs-lookup"><span data-stu-id="bd878-153">Now that you've prepared a container in Azure Storage, tasks can save output to the container by using the [TaskOutputStorage][net_taskoutputstorage] class found in the File Conventions library.</span></span>

<span data-ttu-id="bd878-154">In uw taakcode maakt u eerst een [TaskOutputStorage] [ net_taskoutputstorage] object wanneer de taak is voltooid zijn werk, en roep vervolgens de [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] methode voor het opslaan van de uitvoer naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="bd878-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when the task has completed its work, call the [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method to save its output to Azure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code to process data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="bd878-155">De `kind` parameter van de [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) methode categoriseert de persistente bestanden.</span><span class="sxs-lookup"><span data-stu-id="bd878-155">The `kind` parameter of the [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes the persisted files.</span></span> <span data-ttu-id="bd878-156">Er zijn vier vooraf gedefinieerde [TaskOutputKind] [ net_taskoutputkind] typen: `TaskOutput`, `TaskPreview`, `TaskLog`, en `TaskIntermediate.` ook kunt u aangepaste categorieën van uitvoer.</span><span class="sxs-lookup"><span data-stu-id="bd878-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="bd878-157">Deze uitvoer-typen kunnen u opgeven welk type uitvoer om weer te geven als u later Batch een query voor het persistent gemaakte uitvoerwaarden van een bepaalde taak.</span><span class="sxs-lookup"><span data-stu-id="bd878-157">These output types allow you to specify which type of outputs to list when you later query Batch for the persisted outputs of a given task.</span></span> <span data-ttu-id="bd878-158">Met andere woorden, wanneer u de uitvoer voor een taak wilt weergeven, kunt u de lijst op een van de typen uitvoer filteren.</span><span class="sxs-lookup"><span data-stu-id="bd878-158">In other words, when you list the outputs for a task, you can filter the list on one of the output types.</span></span> <span data-ttu-id="bd878-159">Bijvoorbeeld: ' Ik wil de *preview* uitvoer voor de taak *109*. "</span><span class="sxs-lookup"><span data-stu-id="bd878-159">For example, "Give me the *preview* output for task *109*."</span></span> <span data-ttu-id="bd878-160">Meer informatie over het weergeven en ophalen van de uitvoer wordt weergegeven in [uitvoer ophalen](#retrieve-output) verderop in het artikel.</span><span class="sxs-lookup"><span data-stu-id="bd878-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in the article.</span></span>

> [!TIP]
> <span data-ttu-id="bd878-161">Het type uitvoer bepaalt ook waar in de Azure portal een bepaald bestand wordt weergegeven: *TaskOutput*-gecategoriseerde bestanden worden weergegeven onder **taak uitvoerbestanden**, en *TaskLog* bestanden worden weergegeven onder **logboeken van de taak**.</span><span class="sxs-lookup"><span data-stu-id="bd878-161">The output kind also determines where in the Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="bd878-162">Opslaan van de taak uitvoer</span><span class="sxs-lookup"><span data-stu-id="bd878-162">Store job outputs</span></span>

<span data-ttu-id="bd878-163">Naast de uitvoer van de taak op te slaan, kunt u de uitvoer die zijn gekoppeld aan een volledige taak opslaan.</span><span class="sxs-lookup"><span data-stu-id="bd878-163">In addition to storing task outputs, you can store the outputs associated with an entire job.</span></span> <span data-ttu-id="bd878-164">In de taak samenvoegen van een taak van de rendering film, kunt u de volledig gerenderde film kan behouden als de taakuitvoer van een.</span><span class="sxs-lookup"><span data-stu-id="bd878-164">For example, in the merge task of a movie rendering job, you could persist the fully rendered movie as a job output.</span></span> <span data-ttu-id="bd878-165">Wanneer de taak is voltooid, uw clienttoepassing kunt weergeven en ophalen van de uitvoer voor de taak en heeft geen query uitvoeren op de afzonderlijke taken nodig.</span><span class="sxs-lookup"><span data-stu-id="bd878-165">When your job is completed, your client application can list and retrieve the outputs for the job, and does not need to query the individual tasks.</span></span>

<span data-ttu-id="bd878-166">Taakuitvoer slaan door het aanroepen van de [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] methode, en geef de [JobOutputKind] [ net_joboutputkind] en bestandsnaam:</span><span class="sxs-lookup"><span data-stu-id="bd878-166">Store job output by calling the [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify the [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="bd878-167">Net als bij de **TaskOutputKind** type voor de taak uitvoer, u de [JobOutputKind] [ net_joboutputkind] type om een taak te categoriseren de opgeslagen bestanden.</span><span class="sxs-lookup"><span data-stu-id="bd878-167">As with the **TaskOutputKind** type for task outputs, you use the [JobOutputKind][net_joboutputkind] type to categorize a job's persisted files.</span></span> <span data-ttu-id="bd878-168">Deze parameter kunt u later query voor (lijst) voor een specifiek type uitvoer.</span><span class="sxs-lookup"><span data-stu-id="bd878-168">This parameter allows you to later query for (list) a specific type of output.</span></span> <span data-ttu-id="bd878-169">De **JobOutputKind** type bevat zowel uitvoer als preview-categorieën en biedt ondersteuning voor het maken van aangepaste categorieën.</span><span class="sxs-lookup"><span data-stu-id="bd878-169">The **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="bd878-170">Taak logboeken worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="bd878-170">Store task logs</span></span>

<span data-ttu-id="bd878-171">Naast het behouden blijven van een bestand naar een duurzame opslag wanneer een taak of de taak is voltooid, moet u mogelijk persistent maken van bestanden die zijn bijgewerkt tijdens het uitvoeren van een taak &mdash; logboekbestanden of `stdout.txt` en `stderr.txt`, bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="bd878-171">In addition to persisting a file to durable storage when a task or job completes, you may need to persist files that are updated during the execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="bd878-172">Voor dit doel het bestand conventies van Azure Batch-bibliotheek biedt de [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] methode.</span><span class="sxs-lookup"><span data-stu-id="bd878-172">For this purpose, the Azure Batch File Conventions library provides the [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="bd878-173">Met [SaveTrackedAsync][net_savetrackedasync], kunt u updates naar een bestand op het knooppunt (met een interval dat u opgeeft) bijhouden en persistent maken die updates naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="bd878-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates to a file on the node (at an interval that you specify) and persist those updates to Azure Storage.</span></span>

<span data-ttu-id="bd878-174">In het volgende codefragment gebruiken we [SaveTrackedAsync] [ net_savetrackedasync] bijwerken `stdout.txt` in Azure Storage elke 15 seconden tijdens de uitvoering van de taak:</span><span class="sxs-lookup"><span data-stu-id="bd878-174">In the following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] to update `stdout.txt` in Azure Storage every 15 seconds during the execution of the task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// The primary task logic is wrapped in a using statement that sends updates to
// the stdout.txt blob in Storage every 15 seconds while the task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code to process data and produce output file(s) */

    // We are tracking the disk file to save our standard output, but the
    // node agent may take up to 3 seconds to flush the stdout stream to
    // disk. So give the file a moment to catch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="bd878-175">De sectie met opmerkingen `Code to process data and produce output file(s)` is een tijdelijke aanduiding voor de code die uw taak normaal kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bd878-175">The commented section `Code to process data and produce output file(s)` is a placeholder for the code that your task would normally perform.</span></span> <span data-ttu-id="bd878-176">Bijvoorbeeld wellicht code die gegevens uit Azure Storage downloadt en transformatie of berekening op deze uitvoert.</span><span class="sxs-lookup"><span data-stu-id="bd878-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="bd878-177">De belangrijk onderdeel van dit fragment is te demonstreren hoe u kunt laten teruglopen deze code in een `using` blok regelmatig bijwerken van een bestand met [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="bd878-177">The important part of this snippet is demonstrating how you can wrap such code in a `using` block to periodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="bd878-178">De knooppunt-agent is een programma dat wordt uitgevoerd op elk knooppunt in de groep en de opdracht en controle interface vormt tussen het knooppunt en de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="bd878-178">The node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="bd878-179">De `Task.Delay` aanroep is vereist bij het einde van dit `using` blok om ervoor te zorgen dat de agent knooppunt tijd de inhoud van de standard out naar het bestand stdout.txt op het knooppunt leegmaken.</span><span class="sxs-lookup"><span data-stu-id="bd878-179">The `Task.Delay` call is required at the end of this `using` block to ensure that the node agent has time to flush the contents of standard out to the stdout.txt file on the node.</span></span> <span data-ttu-id="bd878-180">Zonder deze vertraging is het mogelijk de laatste paar seconden van uitvoer mogen worden.</span><span class="sxs-lookup"><span data-stu-id="bd878-180">Without this delay, it is possible to miss the last few seconds of output.</span></span> <span data-ttu-id="bd878-181">Deze vertraging is mogelijk niet vereist voor alle bestanden.</span><span class="sxs-lookup"><span data-stu-id="bd878-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="bd878-182">Wanneer het inschakelen van bestand bijhouden met **SaveTrackedAsync**, alleen *voegt* naar het bestand bijgehouden zijn opgeslagen in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="bd878-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* to the tracked file are persisted to Azure Storage.</span></span> <span data-ttu-id="bd878-183">Gebruik deze methode alleen voor het bijhouden van de logboekbestanden niet draaien of andere bestanden die moeten worden toegevoegd met bewerkingen aan het einde van het bestand worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="bd878-183">Use this method only for tracking non-rotating log files or other files that are written to with append operations to the end of the file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="bd878-184">Uitvoergegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="bd878-184">Retrieve output data</span></span>

<span data-ttu-id="bd878-185">Wanneer u de persistente uitvoer met de Azure Batch-bestand conventies bibliotheek ophaalt, kunt u dat doen op een taak en taak-gericht manier.</span><span class="sxs-lookup"><span data-stu-id="bd878-185">When you retrieve your persisted output using the Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="bd878-186">U kunt de uitvoer van de aanvragen voor de gegeven taak of taak zonder te weten het pad in Azure Storage of zelfs de naam van het bestand.</span><span class="sxs-lookup"><span data-stu-id="bd878-186">You can request the output for given task or job without needing to know its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="bd878-187">U kunt in plaats daarvan uitvoerbestanden aanvragen door de taak of taak-ID.</span><span class="sxs-lookup"><span data-stu-id="bd878-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="bd878-188">Het volgende codefragment taken van een taak doorloopt, wordt bepaalde informatie over de uitvoerbestanden voor de taak afgedrukt en downloadt u de bestanden uit de opslag.</span><span class="sxs-lookup"><span data-stu-id="bd878-188">The following code snippet iterates through a job's tasks, prints some information about the output files for the task, and then downloads its files from Storage.</span></span>

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

## <a name="view-output-files-in-the-azure-portal"></a><span data-ttu-id="bd878-189">De uitvoerbestanden weergeven in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="bd878-189">View output files in the Azure portal</span></span>

<span data-ttu-id="bd878-190">De Azure-portal weergegeven taak uitvoerbestanden en logboeken die zijn opgeslagen in een gekoppelde Azure Storage-account met de [Batch bestand conventies standaard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="bd878-190">The Azure portal displays task output files and logs that are persisted to a linked Azure Storage account using the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="bd878-191">U kunt ook zelf deze conventies implementeren in de een taal van uw keuze of u kunt de bibliotheek bestanden in uw .NET-toepassingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bd878-191">You can implement these conventions yourself in the a language of your choice, or you can use the File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="bd878-192">Om de weergave van de uitvoerbestanden in de portal, moet u voldoen aan de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="bd878-192">To enable the display of your output files in the portal, you must satisfy the following requirements:</span></span>

1. <span data-ttu-id="bd878-193">[Een Azure Storage-account koppelen](#requirement-linked-storage-account) aan uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="bd878-193">[Link an Azure Storage account](#requirement-linked-storage-account) to your Batch account.</span></span>
2. <span data-ttu-id="bd878-194">Voldoen aan de vooraf gedefinieerde naamconventies voor Storage-containers en bestanden als uitvoer persistent maken.</span><span class="sxs-lookup"><span data-stu-id="bd878-194">Adhere to the predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="bd878-195">U kunt de definitie van deze overeenkomsten vinden in de bibliotheek bestand conventies [Leesmij][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="bd878-195">You can find the definition of these conventions in the File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="bd878-196">Als u de [Azure Batch-bestand conventies] [ nuget_package] bibliotheek om vast te leggen van de uitvoer uw bestanden blijven aanwezig op basis van de bestanden standaard.</span><span class="sxs-lookup"><span data-stu-id="bd878-196">If you use the [Azure Batch File Conventions][nuget_package] library to persist your output, your files are persisted according to the File Conventions standard.</span></span>

<span data-ttu-id="bd878-197">Als u wilt weergeven logboeken en uitvoerbestanden taak in de Azure portal, gaat u naar de taak waarvan de uitvoer u geïnteresseerd bent in, klik dan ofwel **opgeslagen uitvoerbestanden** of **opgeslagen logboeken**.</span><span class="sxs-lookup"><span data-stu-id="bd878-197">To view task output files and logs in the Azure portal, navigate to the task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="bd878-198">Deze afbeelding ziet u de **uitvoerbestanden opgeslagen** voor de taak met ID '007':</span><span class="sxs-lookup"><span data-stu-id="bd878-198">This image shows the **Saved output files** for the task with ID "007":</span></span>

<span data-ttu-id="bd878-199">![Taakuitvoer blade in de Azure portal][2]</span><span class="sxs-lookup"><span data-stu-id="bd878-199">![Task outputs blade in the Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="bd878-200">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="bd878-200">Code sample</span></span>

<span data-ttu-id="bd878-201">De [PersistOutputs] [ github_persistoutputs] voorbeeldproject is een van de [Azure Batch-codevoorbeelden] [ github_samples] op GitHub.</span><span class="sxs-lookup"><span data-stu-id="bd878-201">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="bd878-202">Deze Visual Studio-oplossing laat zien hoe de Azure Batch-bestand conventies-bibliotheek gebruiken om vast te leggen van de uitvoer van de taak naar duurzame opslag.</span><span class="sxs-lookup"><span data-stu-id="bd878-202">This Visual Studio solution demonstrates how to use the Azure Batch File Conventions library to persist task output to durable storage.</span></span> <span data-ttu-id="bd878-203">Als u wilt uitvoeren in het voorbeeld, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bd878-203">To run the sample, follow these steps:</span></span>

1. <span data-ttu-id="bd878-204">Open het project in **Visual Studio 2015 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="bd878-204">Open the project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="bd878-205">Toevoegen van uw Batch- en Storage **accountreferenties** naar **AccountSettings.settings** in het project Microsoft.Azure.Batch.Samples.Common.</span><span class="sxs-lookup"><span data-stu-id="bd878-205">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="bd878-206">**Bouwen** (maar niet worden uitgevoerd) de oplossing.</span><span class="sxs-lookup"><span data-stu-id="bd878-206">**Build** (but do not run) the solution.</span></span> <span data-ttu-id="bd878-207">Herstel alle NuGet-pakketten als daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="bd878-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="bd878-208">De Azure portal gebruiken voor het uploaden van een [toepassingspakket](batch-application-packages.md) voor **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="bd878-208">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="bd878-209">Bevatten de `PersistOutputsTask.exe` en afhankelijke assembly's in het ZIP-pakket, de toepassings-ID aan 'PersistOutputsTask' en de versie van het toepassingspakket naar "1.0".</span><span class="sxs-lookup"><span data-stu-id="bd878-209">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span></span>
5. <span data-ttu-id="bd878-210">**Start** (uitvoeren) de **PersistOutputs** project.</span><span class="sxs-lookup"><span data-stu-id="bd878-210">**Start** (run) the **PersistOutputs** project.</span></span>
6. <span data-ttu-id="bd878-211">Als u wordt gevraagd om te kiezen de persistentie-technologie gebruiken voor het uitvoeren van de steekproef, geeft u **1** om uit te voeren van het voorbeeld met de bibliotheek bestand verdragen om vast te leggen van de uitvoer van de taak.</span><span class="sxs-lookup"><span data-stu-id="bd878-211">When prompted to choose the persistence technology to use for running the sample, enter **1** to run the sample using the File Conventions library to persist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bd878-212">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bd878-212">Next steps</span></span>

### <a name="get-the-batch-file-conventions-library-for-net"></a><span data-ttu-id="bd878-213">Ophalen van de Batch-bestand Conventions-bibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="bd878-213">Get the Batch File Conventions library for .NET</span></span>

<span data-ttu-id="bd878-214">De Batch-bestand Conventions-bibliotheek voor .NET is beschikbaar op [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="bd878-214">The Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="bd878-215">De bibliotheek breidt de [CloudJob] [ net_cloudjob] en [CloudTask] [ net_cloudtask] klassen met nieuwe methoden.</span><span class="sxs-lookup"><span data-stu-id="bd878-215">The library extends the [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="bd878-216">Zie ook de [documentatie verwijst naar](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) voor de bibliotheek bestand verdragen.</span><span class="sxs-lookup"><span data-stu-id="bd878-216">Also see the [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for the File Conventions library.</span></span>

<span data-ttu-id="bd878-217">De [broncode] [ github_file_conventions] voor de conventies bestand bibliotheek is beschikbaar op GitHub in de Microsoft Azure SDK voor .NET-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="bd878-217">The [source code][github_file_conventions] for the File Conventions library is available on GitHub in the Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="bd878-218">Andere benaderingen voor persistent maken uitvoergegevens verkennen</span><span class="sxs-lookup"><span data-stu-id="bd878-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="bd878-219">Zie [behouden van de taak en uitvoer naar Azure Storage](batch-task-output.md) voor een overzicht van de persistente gegevens van de taak en taak.</span><span class="sxs-lookup"><span data-stu-id="bd878-219">See [Persist job and task output to Azure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="bd878-220">Zie [Persist taakgegevens naar Azure Storage met de Batch-service API](batch-task-output-files.md) voor informatie over het gebruik van de API van Batch-service om uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="bd878-220">See [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md) to learn how to use the Batch service API to persist output data.</span></span>

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
[2]: ./media/batch-task-output/task-output-02.png "Taakuitvoer blade in de Azure portal"
