---
title: Zelfstudie - De Azure Batch-clientbibliotheek voor .NET gebruiken | Microsoft Docs
description: Leer de basisconcepten van Azure Batch en bouw een eenvoudige oplossing met behulp van .NET.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf8fdca51a6a4ad1b7cd4fe6980543199f6b36e0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-building-solutions-with-the-batch-client-library-for-net"></a><span data-ttu-id="54695-103">Ga aan de slag met het bouwen van oplossingen met de Batch-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="54695-103">Get started building solutions with the Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="54695-104">.NET</span><span class="sxs-lookup"><span data-stu-id="54695-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="54695-105">Python</span><span class="sxs-lookup"><span data-stu-id="54695-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="54695-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="54695-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="54695-107">Ontdek in dit artikel de basisbeginselen van [Azure Batch][azure_batch] en de [Batch .NET][net_api]-bibliotheek aan de hand van een stapsgewijze C#-voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="54695-107">Learn the basics of [Azure Batch][azure_batch] and the [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="54695-108">U leert hier hoe de voorbeeldtoepassing gebruikmaakt van de Batch-service om een parallelle workload in de cloud te verwerken, en hoe deze samenwerkt met [Azure Storage](../storage/common/storage-introduction.md) voor het faseren en ophalen van bestanden.</span><span class="sxs-lookup"><span data-stu-id="54695-108">We look at how the sample application leverages the Batch service to process a parallel workload in the cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="54695-109">U maakt kennis met een gangbare werkstroom voor Batch-toepassingen en krijgt hier ook elementair inzicht in de belangrijkste onderdelen van Batch, zoals jobs, taken, pools en rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="54695-109">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="54695-110">![Werkstroom van de Batch-oplossing (basis)][11]</span><span class="sxs-lookup"><span data-stu-id="54695-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="54695-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="54695-111">Prerequisites</span></span>
<span data-ttu-id="54695-112">In dit artikel wordt ervan uitgegaan dat u praktische kennis hebt van C# en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54695-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="54695-113">Er wordt ook van uitgegaan dat u voldoet aan de vereisten voor het maken van een account die hieronder zijn opgegeven voor Azure en de Batch- en Storage-services.</span><span class="sxs-lookup"><span data-stu-id="54695-113">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="54695-114">Accounts</span><span class="sxs-lookup"><span data-stu-id="54695-114">Accounts</span></span>
* <span data-ttu-id="54695-115">**Azure-account**: als u nog geen Azure-abonnement hebt, [maakt u een gratis Azure-account][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="54695-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="54695-116">**Batch-account**: als u al een Azure-abonnement hebt, [maakt u een Azure Batch-account](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="54695-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="54695-117">**Opslagaccount**: zie [Een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [Over Azure-opslagaccounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="54695-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54695-118">Batch ondersteunt momenteel *alleen* het opslagaccounttype **Algemeen**, zoals beschreven in stap 5 [Een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [Over Azure-opslagaccounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="54695-118">Batch currently supports *only* the **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="54695-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="54695-119">Visual Studio</span></span>
<span data-ttu-id="54695-120">U moet beschikken over **Visual Studio 2015 of hoger** om het voorbeeldproject te kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="54695-120">You must have **Visual Studio 2015 or newer** to build the sample project.</span></span> <span data-ttu-id="54695-121">U vindt gratis en evaluatieversies van Visual Studio in het [overzicht van Visual Studio-producten][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="54695-121">You can find free and trial versions of Visual Studio in the [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="54695-122">*DotNetTutorial*-codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="54695-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="54695-123">Het [DotNetTutorial][github_dotnettutorial]-voorbeeld is een van de vele Batch-codevoorbeelden die u vindt in de opslagplaats [azure-batch-samples][github_samples] in GitHub.</span><span class="sxs-lookup"><span data-stu-id="54695-123">The [DotNetTutorial][github_dotnettutorial] sample is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="54695-124">U kunt alle voorbeelden downloaden door te klikken op **Clone or download > Download ZIP** (Klonen of downloaden > ZIP downloaden) op de introductiepagina van de opslagplaats of door te klikken op de koppeling van de directe download [azure batch-samples-master.zip][github_samples_zip].</span><span class="sxs-lookup"><span data-stu-id="54695-124">You can download all the samples by clicking  **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="54695-125">Nadat u de inhoud van het ZIP-bestand hebt uitgepakt, vindt u de oplossing in deze map:</span><span class="sxs-lookup"><span data-stu-id="54695-125">Once you've extracted the contents of the ZIP file, you can find the solution in the following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="54695-126">Azure Batch Explorer (optioneel)</span><span class="sxs-lookup"><span data-stu-id="54695-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="54695-127">[Azure Batch Explorer][github_batchexplorer] is een gratis hulpprogramma dat is opgenomen in de opslagplaats [azure-batch-samples][github_samples] in GitHub.</span><span class="sxs-lookup"><span data-stu-id="54695-127">The [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="54695-128">Hoewel het niet is vereist om deze zelfstudie te voltooien, kan het nuttig zijn bij de ontwikkeling en foutopsporing van uw Batch-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="54695-128">While not required to complete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="54695-129">Overzicht DotNetTutorial-voorbeeldproject</span><span class="sxs-lookup"><span data-stu-id="54695-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="54695-130">Het *DotNetTutorial*-codevoorbeeld is een Visual Studio-oplossing die uit twee projecten bestaat: **DotNetTutorial** en **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="54695-130">The *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="54695-131">**DotNetTutorial** is de clienttoepassing die met de Batch- en Storage-services communiceert voor het uitvoeren van een parallelle workload op rekenknooppunten (virtuele machines).</span><span class="sxs-lookup"><span data-stu-id="54695-131">**DotNetTutorial** is the client application that interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="54695-132">DotNetTutorial wordt uitgevoerd op uw lokale werkstation.</span><span class="sxs-lookup"><span data-stu-id="54695-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="54695-133">**TaskApplication** is het programma dat op rekenknooppunten in Azure wordt uitgevoerd om het echte werk te verrichten.</span><span class="sxs-lookup"><span data-stu-id="54695-133">**TaskApplication** is the program that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="54695-134">In het voorbeeld parseert `TaskApplication.exe` de tekst in een bestand dat van Azure Storage is gedownload (het invoerbestand).</span><span class="sxs-lookup"><span data-stu-id="54695-134">In the sample, `TaskApplication.exe` parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="54695-135">Daarna creëert het een tekstbestand (het uitvoerbestand) met daarin een lijst van de eerste drie woorden die het invoerbestand bevat.</span><span class="sxs-lookup"><span data-stu-id="54695-135">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="54695-136">Nadat TaskApplication het uitvoerbestand heeft gemaakt, wordt het bestand geüpload naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="54695-136">After it creates the output file, TaskApplication uploads the file to Azure Storage.</span></span> <span data-ttu-id="54695-137">Hierdoor is het voor de clienttoepassing beschikbaar als download.</span><span class="sxs-lookup"><span data-stu-id="54695-137">This makes it available to the client application for download.</span></span> <span data-ttu-id="54695-138">TaskApplication wordt parallel uitgevoerd op meerdere rekenknooppunten in de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="54695-138">TaskApplication runs in parallel on multiple compute nodes in the Batch service.</span></span>

<span data-ttu-id="54695-139">Het volgende diagram illustreert de primaire bewerkingen die worden uitgevoerd door de clienttoepassing *DotNetTutorial*, en de toepassing die wordt uitgevoerd door de taken, *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="54695-139">The following diagram illustrates the primary operations that are performed by the client application, *DotNetTutorial*, and the application that is executed by the tasks, *TaskApplication*.</span></span> <span data-ttu-id="54695-140">Deze basiswerkstroom is typerend voor vele rekenoplossingen die met Batch worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="54695-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="54695-141">Hoewel het niet elke functie beschikbaar in de Batch-service aantoont, omvat vrijwel elk Batch-scenario delen van deze werkstroom.</span><span class="sxs-lookup"><span data-stu-id="54695-141">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="54695-142">![Batch-voorbeeldwerkstroom][8]</span><span class="sxs-lookup"><span data-stu-id="54695-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="54695-143">**Stap 1.**</span><span class="sxs-lookup"><span data-stu-id="54695-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="54695-144">Maak **containers** in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="54695-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="54695-145">
[**Stap 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="54695-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="54695-146">Upload taaktoepassings- en invoerbestanden naar containers.</span><span class="sxs-lookup"><span data-stu-id="54695-146">Upload task application files and input files to containers.</span></span><br/><span data-ttu-id="54695-147">
[**Stap 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="54695-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="54695-148">Maak een Batch-**pool**.</span><span class="sxs-lookup"><span data-stu-id="54695-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="54695-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="54695-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="54695-150">De pool **Begintaak** downloadt de binaire bestanden van de taak (TaskApplication) naar knooppunten wanneer deze aan de pool worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="54695-150">The pool **StartTask** downloads the task binary files (TaskApplication) to nodes as they join the pool.</span></span><br/><span data-ttu-id="54695-151">
[**Stap 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="54695-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="54695-152">Maak een Batch-**job**.</span><span class="sxs-lookup"><span data-stu-id="54695-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="54695-153">
[**Stap 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="54695-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="54695-154">Voeg **taken** toe aan de job.</span><span class="sxs-lookup"><span data-stu-id="54695-154">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="54695-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="54695-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="54695-156">De taken worden gepland om op knooppunten te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54695-156">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="54695-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="54695-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="54695-158">Elke taak downloadt de bijbehorende invoergegevens uit Azure Storage en wordt daarna uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54695-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="54695-159">
[**Stap 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="54695-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="54695-160">Controleer taken.</span><span class="sxs-lookup"><span data-stu-id="54695-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="54695-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="54695-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="54695-162">Nadat taken zijn voltooid, uploaden zij hun uitvoergegevens naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="54695-162">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/><span data-ttu-id="54695-163">
[**Stap 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="54695-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="54695-164">Download taakuitvoer uit Storage.</span><span class="sxs-lookup"><span data-stu-id="54695-164">Download task output from Storage.</span></span>

<span data-ttu-id="54695-165">Zoals al is vermeld, voert niet elke Batch-oplossing exact deze stappen uit en kan een oplossing ook veel meer stappen bevatten. De voorbeeldtoepassing *DotNetTutorial* toont echter de algemene processen die u in een Batch-oplossing terugvindt.</span><span class="sxs-lookup"><span data-stu-id="54695-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but the *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-the-dotnettutorial-sample-project"></a><span data-ttu-id="54695-166">Het *DotNetTutorial*-voorbeeldproject maken</span><span class="sxs-lookup"><span data-stu-id="54695-166">Build the *DotNetTutorial* sample project</span></span>
<span data-ttu-id="54695-167">Voordat u het voorbeeld met succes kunt uitvoeren, moet u in het *DotNetTutorial*-project in het bestand `Program.cs` Batch- en Storage-accountreferenties opgeven.</span><span class="sxs-lookup"><span data-stu-id="54695-167">Before you can successfully run the sample, you must specify both Batch and Storage account credentials in the *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="54695-168">Als u dit nog niet hebt gedaan, opent u de oplossing in Visual Studio door te dubbelklikken op het oplossingsbestand `DotNetTutorial.sln`.</span><span class="sxs-lookup"><span data-stu-id="54695-168">If you have not done so already, open the solution in Visual Studio by double-clicking the `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="54695-169">U kunt de oplossing ook vanuit Visual Studio openen met het menu **Bestand > Openen > Project/Oplossing**.</span><span class="sxs-lookup"><span data-stu-id="54695-169">Or open it from within Visual Studio by using the **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="54695-170">Open `Program.cs` in het project *DotNetTutorial*.</span><span class="sxs-lookup"><span data-stu-id="54695-170">Open `Program.cs` within the *DotNetTutorial* project.</span></span> <span data-ttu-id="54695-171">Voeg daarna uw referenties toe zoals deze boven in het bestand zijn vermeld:</span><span class="sxs-lookup"><span data-stu-id="54695-171">Then add your credentials as specified near the top of the file:</span></span>

```csharp
// Update the Batch and Storage account credential strings below with the values
// unique to your accounts. These are used when constructing connection strings
// for the Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="54695-172">Zoals eerder vermeld, moet u in Azure Storage momenteel de referenties voor een opslagaccount voor **algemeen gebruik**t opgeven.</span><span class="sxs-lookup"><span data-stu-id="54695-172">As mentioned above, you must currently specify the credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="54695-173">Uw Batch-toepassingen gebruiken Blob Storage in het opslagaccount van het type **voor algemeen gebruik**.</span><span class="sxs-lookup"><span data-stu-id="54695-173">Your Batch applications use blob storage within the **general-purpose** storage account.</span></span> <span data-ttu-id="54695-174">Geef niet de referenties op voor een opslagaccount die is gemaakt door het accounttype *Blob Storage* te selecteren.</span><span class="sxs-lookup"><span data-stu-id="54695-174">Do not specify the credentials for a Storage account that was created by selecting the *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="54695-175">U vindt uw Batch- en Storage-accountreferenties op de accountblade van elke service in [Azure Portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="54695-175">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="54695-176">![Batch-referenties in de portal][9]
![Storage-referenties in de portal][10]</span><span class="sxs-lookup"><span data-stu-id="54695-176">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="54695-177">Nu dat u het project met uw referenties hebt bijgewerkt, klikt u met de rechtermuisknop op de oplossing in Solution Explorer en klikt u op **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="54695-177">Now that you've updated the project with your credentials, right-click the solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="54695-178">Bevestig het herstel van alle NuGet-pakketten als dit wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="54695-178">Confirm the restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="54695-179">Als de NuGet-pakketten niet automatisch worden hersteld of als in foutberichten wordt gemeld dat de pakketten niet kunnen worden hersteld, controleert u of [NuGet Package Manager][nuget_packagemgr] is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="54695-179">If the NuGet packages are not automatically restored, or if you see errors about a failure to restore the packages, ensure that you have the [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="54695-180">Schakel vervolgens het downloaden van ontbrekende pakketten in.</span><span class="sxs-lookup"><span data-stu-id="54695-180">Then enable the download of missing packages.</span></span> <span data-ttu-id="54695-181">Zie [Enabling Package Restore During Build][nuget_restore] (Herstellen van pakketten tijdens het bouwen inschakelen) om het downloaden van pakketten in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="54695-181">See [Enabling Package Restore During Build][nuget_restore] to enable package download.</span></span>
>
>

<span data-ttu-id="54695-182">In de volgende secties wordt de voorbeeldtoepassing uitgesplitst in de stappen die met de toepassing worden uitgevoerd om een workload in de Batch-service te verwerken en worden die stappen in detail besproken.</span><span class="sxs-lookup"><span data-stu-id="54695-182">In the following sections, we break down the sample application into the steps that it performs to process a workload in the Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="54695-183">Bij het lezen van de rest van dit artikel kunt u het best de geopende oplossing in Visual Studio raadplegen omdat niet elke regel in de code van het voorbeeld wordt besproken.</span><span class="sxs-lookup"><span data-stu-id="54695-183">We encourage you to refer to the open solution in Visual Studio while you work your way through the rest of this article, since not every line of code in the sample is discussed.</span></span>

<span data-ttu-id="54695-184">Navigeer naar de bovenkant van de methode `MainAsync` in het bestand `Program.cs` van het *DotNetTutorial*-project om bij stap 1 te starten.</span><span class="sxs-lookup"><span data-stu-id="54695-184">Navigate to the top of the `MainAsync` method in the *DotNetTutorial* project's `Program.cs` file to start with Step 1.</span></span> <span data-ttu-id="54695-185">Elke stap hieronder volgt min of meer de voortgang van de methodeaanroepen in `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="54695-185">Each step below then roughly follows the progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="54695-186">Stap 1: opslagcontainers maken</span><span class="sxs-lookup"><span data-stu-id="54695-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="54695-187">![Containers maken in Azure Storage][1]
</span><span class="sxs-lookup"><span data-stu-id="54695-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="54695-188">Batch bevat ingebouwde ondersteuning voor interactie met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="54695-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="54695-189">Containers in uw opslagaccount bevatten de bestanden die nodig zijn voor de taken die in uw Batch-account worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54695-189">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="54695-190">De containers bieden ook een plaats voor de opslag van de uitvoergegevens die de taken opleveren.</span><span class="sxs-lookup"><span data-stu-id="54695-190">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="54695-191">Het eerste wat de clienttoepassing *DotNetTutorial* doet, is drie containers maken in [Azure Blob Storage](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="54695-191">The first thing the *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="54695-192">**application**: in deze container worden de toepassing die door de taken wordt uitgevoerd, evenals alle afhankelijkheden hiervan, zoals DLL-bestanden, opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="54695-192">**application**: This container will store the application run by the tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="54695-193">**input**: taken downloaden de te verwerken gegevensbestanden uit de *invoer* container.</span><span class="sxs-lookup"><span data-stu-id="54695-193">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="54695-194">**output**: nadat taken de verwerking van invoerbestanden hebben voltooid, uploaden zij de resultaten naar de *uitvoer* container.</span><span class="sxs-lookup"><span data-stu-id="54695-194">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="54695-195">Om met een opslagaccount te communiceren en containers te maken, gebruiken we de [Azure Storage-clientbibliotheek voor .NET][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="54695-195">In order to interact with a Storage account and create containers, we use the [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="54695-196">We maken een verwijzing naar het account met [CloudStorageAccount][net_cloudstorageaccount] en van hieruit maken we een [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="54695-196">We create a reference to the account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct the Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve the storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create the blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="54695-197">We gebruiken in de toepassing de verwijzing `blobClient` en geven deze als een parameter door aan verschillende methoden.</span><span class="sxs-lookup"><span data-stu-id="54695-197">We use the `blobClient` reference throughout the application and pass it as a parameter to several methods.</span></span> <span data-ttu-id="54695-198">Een voorbeeld hiervan bevindt zich in het codeblok dat onmiddellijk na het bovenstaande blok volgt, waar we `CreateContainerIfNotExistAsync` aanroepen om de containers daadwerkelijk te maken.</span><span class="sxs-lookup"><span data-stu-id="54695-198">An example of this is in the code block that immediately follows the above, where we call `CreateContainerIfNotExistAsync` to actually create the containers.</span></span>

```csharp
// Use the blob client to create the containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

<span data-ttu-id="54695-199">Zodra de containers zijn gemaakt, kan de toepassing nu de bestanden uploaden die door de taken worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="54695-199">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> <span data-ttu-id="54695-200">[How to use Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) (Blob Storage gebruiken met .NET) biedt een goed overzicht van hoe u met Azure Storage-containers en -blobs werkt.</span><span class="sxs-lookup"><span data-stu-id="54695-200">[How to use Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="54695-201">Wanneer u met Batch begint te werken, moet dat artikel hoog in uw leeslijst zijn vermeld.</span><span class="sxs-lookup"><span data-stu-id="54695-201">It should be near the top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="54695-202">Stap 2: taaktoepassings- en gegevensbestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="54695-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="54695-203">![Taaktoepassings- en invoer(gegevens)bestanden uploaden naar containers][2]
</span><span class="sxs-lookup"><span data-stu-id="54695-203">![Upload task application and input (data) files to containers][2]
</span></span><br/>

<span data-ttu-id="54695-204">In de bewerking voor het uploaden van bestanden definieert *DotNetTutorial* eerst verzamelingen van bestandspaden naar **toepassing**sbestanden en **invoer**bestanden op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="54695-204">In the file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="54695-205">Daarna worden deze bestanden geüpload naar de containers die u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="54695-205">Then it uploads these files to the containers that you created in the previous step.</span></span>

```csharp
// Paths to the executable and its dependencies that will be executed by the tasks
List<string> applicationFilePaths = new List<string>
{
    // The DotNetTutorial project includes a project reference to TaskApplication,
    // allowing us to determine the path of the task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// The collection of data files that are to be processed by the tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload the application and its dependencies to Azure Storage. This is the
// application that will process the data files, and will be executed by each
// of the tasks on the compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload the data files. This is the data that will be processed by each of
// the tasks that are executed on the compute nodes within the pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="54695-206">Er zijn in `Program.cs` twee methoden die betrokken zijn bij het uploadproces:</span><span class="sxs-lookup"><span data-stu-id="54695-206">There are two methods in `Program.cs` that are involved in the upload process:</span></span>

* <span data-ttu-id="54695-207">`UploadFilesToContainerAsync`: deze methode retourneert een verzameling [ResourceFile][net_resourcefile]-objecten (zie hieronder) en roept intern `UploadFileToContainerAsync` aan om elk bestand te uploaden dat in de parameter *filePaths* wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="54695-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` to upload each file that is passed in the *filePaths* parameter.</span></span>
* <span data-ttu-id="54695-208">`UploadFileToContainerAsync`: dit is de methode die daadwerkelijk het bestand uploadt en de [ResourceFile][net_resourcefile]-objecten maakt.</span><span class="sxs-lookup"><span data-stu-id="54695-208">`UploadFileToContainerAsync`: This is the method that actually performs the file upload and creates the [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="54695-209">Nadat het bestand is geüpload, krijgt deze methode een Shared Access Signature (SAS) voor het bestand en retourneert deze een ResourceFile-object dat het bestand vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="54695-209">After uploading the file, it obtains a shared access signature (SAS) for the file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="54695-210">Ook Shared Access Signatures worden hieronder besproken.</span><span class="sxs-lookup"><span data-stu-id="54695-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} to container [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set the expiry time and permissions for the blob shared access signature.
        // In this case, no start time is specified, so the shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct the SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="54695-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="54695-211">ResourceFiles</span></span>
<span data-ttu-id="54695-212">[ResourceFile][net_resourcefile] levert aan taken in Batch de URL naar een bestand in Azure Storage dat naar een rekenknooppunt wordt gedownload voordat deze taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54695-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="54695-213">De eigenschap [ResourceFile.BlobSource][net_resourcefile_blobsource] geeft de volledige URL van het bestand zoals dit zich in Azure Storage bevindt.</span><span class="sxs-lookup"><span data-stu-id="54695-213">The [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="54695-214">De URL kan ook een Shared Access Signature (SAS) bevatten, die veilige toegang tot het bestand biedt.</span><span class="sxs-lookup"><span data-stu-id="54695-214">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="54695-215">De meeste typen taken in Batch .NET bevatten een eigenschap *ResourceFiles*, waaronder:</span><span class="sxs-lookup"><span data-stu-id="54695-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="54695-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="54695-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="54695-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="54695-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="54695-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="54695-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="54695-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="54695-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="54695-220">De DotNetTutorial-voorbeeldtoepassing gebruikt niet de taaktypen JobPreparationTask of JobReleaseTask. Meer informatie hierover vindt u in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md) (Jobvoorbereidings- en jobvoltooiingstaken uitvoeren op Azure Batch-rekenknooppunten).</span><span class="sxs-lookup"><span data-stu-id="54695-220">The DotNetTutorial sample application does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="54695-221">Shared Access Signature (SAS)</span><span class="sxs-lookup"><span data-stu-id="54695-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="54695-222">Shared Access Signatures zijn tekenreeksen die, wanneer ze deel uitmaken van een URL, beveiligde toegang bieden tot containers en blobs in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="54695-222">Shared access signatures are strings which—when included as part of a URL—provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="54695-223">De DotNetTutorial-toepassing maakt gebruik van Shared Access Signature-URL's voor blobs en containers en toont aan hoe u deze SAS-tekenreeksen van de Storage-service kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="54695-223">The DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="54695-224">**Shared Access Signatures voor blobs**: StartTask van de pool in DotNetTutorial maakt gebruik van Shared Access Signatures voor blobs wanneer het de binaire bestanden van toepassingen en invoergegevensbestanden uit Storage downloadt (zie stap 3 hieronder).</span><span class="sxs-lookup"><span data-stu-id="54695-224">**Blob shared access signatures**: The pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads the application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="54695-225">De methode `UploadFileToContainerAsync` in het bestand `Program.cs` van DotNetTutorial bevat de code die de Shared Access Signature van elke blob verkrijgt.</span><span class="sxs-lookup"><span data-stu-id="54695-225">The `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="54695-226">Dit gebeurt door het aanroepen van [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span><span class="sxs-lookup"><span data-stu-id="54695-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="54695-227">**Shared Access Signatures voor containers**: Nadat elke taak in het rekenknooppunt zijn werk heeft verricht, uploadt elke taak zijn uitvoerbestand naar de *uitvoer*container in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="54695-227">**Container shared access signatures**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="54695-228">Hiertoe maakt TaskApplication gebruik van een Shared Access Signature voor containers die schrijftoegang biedt tot de container als deel van het pad wanneer TaskApplication het bestand uploadt.</span><span class="sxs-lookup"><span data-stu-id="54695-228">To do so, TaskApplication uses a container shared access signature that provides write access to the container as part of the path when it uploads the file.</span></span> <span data-ttu-id="54695-229">De Shared Access Signature voor containers wordt op een vergelijkbare manier verkregen als de Shared Access Signature voor blobs.</span><span class="sxs-lookup"><span data-stu-id="54695-229">Obtaining the container shared access signature is done in a similar fashion as when obtaining the blob shared access signature.</span></span> <span data-ttu-id="54695-230">In DotNetTutorial zult u zien dat de Help-methode `GetContainerSasUrl` [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] aanroept om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="54695-230">In DotNetTutorial, you will find that the `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] to do so.</span></span> <span data-ttu-id="54695-231">Meer informatie over hoe TaskApplication de Shared Access Signature voor containers gebruikt, vindt u in 'Stap 6: taken controleren'.</span><span class="sxs-lookup"><span data-stu-id="54695-231">You'll read more about how TaskApplication uses the container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="54695-232">Bekijk de tweedelige reeks over Shared Access Signatures [Part 1: Understanding the shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (Deel 1: inzicht in het Shared Access Signature (SAS)-model) en [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) (Deel 2: Een Shared Access Signature (SAS) maken en gebruiken met Blob Storage), voor meer informatie over het verstrekken van beveiligde toegang tot gegevens in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="54695-232">Check out the two-part series on shared access signatures, [Part 1: Understanding the shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="54695-233">Stap 3: Batch-pool maken</span><span class="sxs-lookup"><span data-stu-id="54695-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="54695-234">![Een Batch-pool maken][3]
</span><span class="sxs-lookup"><span data-stu-id="54695-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="54695-235">Een Batch-**pool** is een verzameling rekenknooppunten (virtuele machines) waarop Batch de taken van een job uitvoert.</span><span class="sxs-lookup"><span data-stu-id="54695-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="54695-236">Zodra de toepassing en gegevensbestanden naar het Storage-account zijn geüpload met Azure Storage-API's, worden er door *DotNetTutorial* aanroepen naar de Batch-service gedaan met API's uit de Batch .NET-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="54695-236">After uploading the application and data files to the Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls to the Batch service with APIs provided by the Batch .NET library.</span></span> <span data-ttu-id="54695-237">De code maakt eerst een [BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="54695-237">The code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="54695-238">Daarna wordt in het voorbeeld met behulp van een aanroep naar `CreatePoolIfNotExistsAsync` een pool van rekenknooppunten in het Batch-account gemaakt.</span><span class="sxs-lookup"><span data-stu-id="54695-238">Next, the sample creates a pool of compute nodes in the Batch account with a call to `CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="54695-239">`CreatePoolIfNotExistsAsync` gebruikt de methode [BatchClient.PoolOperations.CreatePool][net_pool_create] om een nieuwe pool te maken in de Batch-service:</span><span class="sxs-lookup"><span data-stu-id="54695-239">`CreatePoolIfNotExistsAsync` uses the [BatchClient.PoolOperations.CreatePool][net_pool_create] method to create a new pool in the Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create the unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign the StartTask that will be executed when compute nodes join the pool.
        // In this case, we copy the StartTask's resource files (that will be automatically downloaded
        // to the node by the StartTask) into the shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for the StartTask that copies the task application files to the
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need to manually exit with a 0 for Batch to recognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow the specific error code PoolExists since that is expected if the pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("The pool {0} already existed when we tried to create it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="54695-240">Wanneer u een pool maakt met [CreatePool][net_pool_create], geeft u meerdere parameters op, zoals het aantal rekenknooppunten, de [grootte van de knooppunten](../cloud-services/cloud-services-sizes-specs.md) en het besturingssysteem van de knooppunten.</span><span class="sxs-lookup"><span data-stu-id="54695-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as the number of compute nodes, the [size of the nodes](../cloud-services/cloud-services-sizes-specs.md), and the nodes' operating system.</span></span> <span data-ttu-id="54695-241">In *DotNetTutorial* gebruiken we [CloudServiceConfiguration][net_cloudserviceconfiguration] om Windows Server 2012 R2 op te geven vanuit [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="54695-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] to specify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="54695-242">U kunt ook pools van rekenknooppunten maken die virtuele Azure-machines zijn door de [VirtualMachineConfiguration][net_virtualmachineconfiguration] op te geven voor uw pool.</span><span class="sxs-lookup"><span data-stu-id="54695-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying the [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="54695-243">U kunt een pool van VM-rekenknooppunten maken vanuit een Windows of [Linux-installatiekopie](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="54695-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="54695-244">De bron voor uw VM-installatiekopieën kan zijn:</span><span class="sxs-lookup"><span data-stu-id="54695-244">The source for your VM images can be either:</span></span>

- <span data-ttu-id="54695-245">De [Azure Virtual Machines Marketplace][vm_marketplace], die gebruiksklare Windows- en Linux-installatiekopieën biedt.</span><span class="sxs-lookup"><span data-stu-id="54695-245">The [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="54695-246">Een aangepaste installatiekopie die u voorbereidt en aanlevert.</span><span class="sxs-lookup"><span data-stu-id="54695-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="54695-247">Zie [Grootschalige parallelle rekenoplossingen ontwikkelen met Batch](batch-api-basics.md#pool) voor meer informatie over aangepaste installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="54695-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54695-248">De rekenresources in Batch worden in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="54695-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="54695-249">Om uw kosten te beperken, kunt u `targetDedicatedComputeNodes` verlagen naar 1 voordat u het voorbeeld uitvoert.</span><span class="sxs-lookup"><span data-stu-id="54695-249">To minimize costs, you can lower `targetDedicatedComputeNodes` to 1 before you run the sample.</span></span>
>
>

<span data-ttu-id="54695-250">Samen met deze fysieke knooppunteigenschappen kunt u ook [StartTask][net_pool_starttask] voor de pool opgeven.</span><span class="sxs-lookup"><span data-stu-id="54695-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for the pool.</span></span> <span data-ttu-id="54695-251">StartTask wordt in elk knooppunt uitgevoerd wanneer dat knooppunt aan de pool wordt toegevoegd en telkens wanneer dat knooppunt opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="54695-251">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="54695-252">StartTask is met name nuttig voor het installeren van toepassingen in rekenknooppunten voordat taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54695-252">The StartTask is especially useful for installing applications on compute nodes prior to the execution of tasks.</span></span> <span data-ttu-id="54695-253">Als bijvoorbeeld uw taken gegevens verwerken met behulp van Python-scripts, kunt u StartTask gebruiken om Python te installeren in de rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="54695-253">For example, if your tasks process data by using Python scripts, you could use a StartTask to install Python on the compute nodes.</span></span>

<span data-ttu-id="54695-254">In deze voorbeeldtoepassing kopieert StartTask de bestanden die het van Storage downloadt (die zijn opgegeven met behulp van de eigenschap [ResourceFiles][net_starttask_resourcefiles] van de [StartTask][net_starttask]) uit de StartTask-werkmap naar de gedeelde map waartoe *alle* taken die in het knooppunt worden uitgevoerd toegang hebben.</span><span class="sxs-lookup"><span data-stu-id="54695-254">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from the StartTask working directory to the shared directory that *all* tasks running on the node can access.</span></span> <span data-ttu-id="54695-255">In wezen worden hierdoor `TaskApplication.exe` en al de afhankelijkheden ervan gekopieerd naar de gedeelde map in elk knooppunt wanneer het knooppunt aan de pool wordt toegevoegd, zodat alle taken die in het knooppunt worden uitgevoerd er toegang toe hebben.</span><span class="sxs-lookup"><span data-stu-id="54695-255">Essentially, this copies `TaskApplication.exe` and its dependencies to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="54695-256">De functie voor **toepassingspakketten** van Azure Batch biedt een andere manier om uw toepassing in rekenknooppunten in een pool te krijgen.</span><span class="sxs-lookup"><span data-stu-id="54695-256">The **application packages** feature of Azure Batch provides another way to get your application onto the compute nodes in a pool.</span></span> <span data-ttu-id="54695-257">Zie [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md) (Toepassingen implementeren op rekenknooppunten met Batch-toepassingspakketten) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="54695-257">See [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="54695-258">Opmerkelijk in het bovenstaande codefragment is ook het gebruik van twee omgevingsvariabelen in de eigenschap *CommandLine* van StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` en `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="54695-258">Also notable in the code snippet above is the use of two environment variables in the *CommandLine* property of the StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="54695-259">Elk rekenknooppunt in een Batch-pool wordt automatisch geconfigureerd met meerdere omgevingsvariabelen die specifiek zijn voor Batch.</span><span class="sxs-lookup"><span data-stu-id="54695-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="54695-260">Elke proces dat door een taak wordt uitgevoerd, heeft toegang tot deze omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="54695-260">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="54695-261">Zie de secties [Omgevingsinstellingen voor taken](batch-api-basics.md#environment-settings-for-tasks) en [Bestanden en mappen](batch-api-basics.md#files-and-directories) in [Overzicht van Batch-functies voor ontwikkelaars](batch-api-basics.md) voor meer informatie over de omgevingsvariabelen die beschikbaar zijn in rekenknooppunten in een Batch-pool en voor meer informatie over taakwerkmappen.</span><span class="sxs-lookup"><span data-stu-id="54695-261">To find out more about the environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see the [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in the [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="54695-262">Stap 4: Batch-job maken</span><span class="sxs-lookup"><span data-stu-id="54695-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="54695-263">![Een Batch-job maken][4]</span><span class="sxs-lookup"><span data-stu-id="54695-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="54695-264">Een Batch-**job** is een verzameling taken en is gekoppeld aan een pool van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="54695-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="54695-265">De taken in een job worden uitgevoerd op de rekenknooppunten van de gekoppelde pool.</span><span class="sxs-lookup"><span data-stu-id="54695-265">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="54695-266">U kunt een job niet alleen gebruiken om taken in gerelateerde workloads te organiseren en te volgen, maar ook om bepaalde beperkingen op te leggen, zoals de maximale runtime voor de job (en, bij uitbreiding, dus ook voor de taken ervan) en de prioriteit van de job in verhouding tot andere jobs in de Batch-account.</span><span class="sxs-lookup"><span data-stu-id="54695-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) as well as job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="54695-267">In dit voorbeeld wordt de job echter alleen gekoppeld aan de pool die in stap 3 is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="54695-267">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="54695-268">Er worden geen aanvullende eigenschappen geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="54695-268">No additional properties are configured.</span></span>

<span data-ttu-id="54695-269">Alle Batch-jobs worden gekoppeld aan een specifieke pool.</span><span class="sxs-lookup"><span data-stu-id="54695-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="54695-270">Deze koppeling geeft aan op welke knooppunten de taken van de job worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54695-270">This association indicates which nodes the job's tasks will execute on.</span></span> <span data-ttu-id="54695-271">U geeft dit op met behulp van de eigenschap [CloudJob.PoolInformation][net_job_poolinfo], zoals in het onderstaande codefragment wordt getoond.</span><span class="sxs-lookup"><span data-stu-id="54695-271">You specify this by using the [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in the code snippet below.</span></span>

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

<span data-ttu-id="54695-272">Nu een job is gemaakt, worden er taken aan toegevoegd die het werk verrichten.</span><span class="sxs-lookup"><span data-stu-id="54695-272">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="54695-273">Stap 5: taken toevoegen aan job</span><span class="sxs-lookup"><span data-stu-id="54695-273">Step 5: Add tasks to job</span></span>
<span data-ttu-id="54695-274">![Taken toevoegen aan job][5]</span><span class="sxs-lookup"><span data-stu-id="54695-274">![Add tasks to job][5]</span></span><br/><span data-ttu-id="54695-275">
*(1) Taken worden toegevoegd aan de job, (2) de taken worden gepland om op knooppunten te worden uitgevoerd en (3) de taken downloaden de te verwerken gegevensbestanden*</span><span class="sxs-lookup"><span data-stu-id="54695-275">
*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="54695-276">Batch-**taken** zijn de afzonderlijke werkeenheden die op de rekenknooppunten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54695-276">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="54695-277">Een taak heeft een opdrachtregel en voert de scripts of uitvoerbare bestanden uit die u in die opdrachtregel opgeeft.</span><span class="sxs-lookup"><span data-stu-id="54695-277">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="54695-278">Om daadwerkelijk werk te verrichten, moeten de taken aan een job worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="54695-278">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="54695-279">Elke [CloudTask][net_task] wordt geconfigureerd met behulp van een opdrachtregeleigenschap en [ResourceFiles][net_task_resourcefiles] (net als bij StartTask van de pool) die de taak downloadt naar het knooppunt voordat de opdrachtregel ervan automatisch wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54695-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="54695-280">In het *DotNetTutorial*-voorbeeldproject verwerkt elke taak slechts één bestand.</span><span class="sxs-lookup"><span data-stu-id="54695-280">In the *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="54695-281">Hierdoor bevat de verzameling ResourceFiles één element.</span><span class="sxs-lookup"><span data-stu-id="54695-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks to job [{1}]...", inputFiles.Count, jobId);

    // Create a collection to hold the tasks that we'll be adding to the job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of the tasks. Because we copied the task application to the
    // node's shared directory with the pool's StartTask, we can access it via
    // the shared directory on the node that the task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add the tasks as a collection, as opposed to issuing a separate AddTask call
    // for each. Bulk task submission helps to ensure efficient underlying API calls
    // to the Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="54695-282">Wanneer ze toegang krijgen tot omgevingsvariabelen zoals `%AZ_BATCH_NODE_SHARED_DIR%` of een toepassing uitvoeren die niet op het `PATH` van het knooppunt wordt gevonden, moeten taakopdrachtregels het voorvoegsel `cmd /c` krijgen.</span><span class="sxs-lookup"><span data-stu-id="54695-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in the node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="54695-283">Hiermee wordt de opdrachtinterpreter expliciet uitgevoerd en krijgt deze de instructie om te beëindigen nadat uw opdracht is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54695-283">This will explicitly execute the command interpreter and instruct it to terminate after carrying out your command.</span></span> <span data-ttu-id="54695-284">Deze vereiste is niet nodig als uw taken een toepassing uitvoeren op het `PATH` van het knooppunt (zoals *robocopy.exe* of *powershell.exe*) en er geen omgevingsvariabelen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="54695-284">This requirement is unnecessary if your tasks execute an application in the node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="54695-285">In de `foreach`-lus in het bovenstaande codefragment kunt u zien dat de opdrachtregel voor de taak zodanig is opgesteld dat drie opdrachtregelargumenten worden doorgegeven aan *TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="54695-285">Within the `foreach` loop in the code snippet above, you can see that the command line for the task is constructed such that three command-line arguments are passed to *TaskApplication.exe*:</span></span>

1. <span data-ttu-id="54695-286">Het **eerste argument** is het pad van het te verwerken bestand.</span><span class="sxs-lookup"><span data-stu-id="54695-286">The **first argument** is the path of the file to process.</span></span> <span data-ttu-id="54695-287">Dit is het lokale pad naar het bestand, zoals zich dit op het knooppunt bevindt.</span><span class="sxs-lookup"><span data-stu-id="54695-287">This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="54695-288">Toen het ResourceFile-object `UploadFileToContainerAsync` voor het eerst werd gemaakt, werd de bestandsnaam voor deze eigenschap gebruikt (als een parameter voor de constructor ResourceFile).</span><span class="sxs-lookup"><span data-stu-id="54695-288">When the ResourceFile object in `UploadFileToContainerAsync` was first created above, the file name was used for this property (as a parameter to the ResourceFile constructor).</span></span> <span data-ttu-id="54695-289">Dit geeft aan dat het bestand kan worden gevonden in dezelfde map als *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="54695-289">This indicates that the file can be found in the same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="54695-290">Het **tweede argument** geeft aan dat de eerste *N* woorden naar het uitvoerbestand moeten worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="54695-290">The **second argument** specifies that the top *N* words should be written to the output file.</span></span> <span data-ttu-id="54695-291">In het voorbeeld is dit in code vastgelegd, zodat de eerste drie woorden naar het uitvoerbestand worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="54695-291">In the sample, this is hard-coded so that the top three words are written to the output file.</span></span>
3. <span data-ttu-id="54695-292">Het **derde argument** is de Shared Access Signature (SAS) die schrijftoegang tot de **uitvoer**container in Azure Storage biedt.</span><span class="sxs-lookup"><span data-stu-id="54695-292">The **third argument** is the shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="54695-293">*TaskApplication.exe* maakt gebruik van deze Shared Access Signature-URL wanneer het uitvoerbestand naar Azure Storage uploadt.</span><span class="sxs-lookup"><span data-stu-id="54695-293">*TaskApplication.exe* uses this shared access signature URL when it uploads the output file to Azure Storage.</span></span> <span data-ttu-id="54695-294">U vindt de code hiervoor in de methode `UploadFileToContainer` in het bestand `Program.cs` van het TaskApplication-project:</span><span class="sxs-lookup"><span data-stu-id="54695-294">You can find the code for this in the `UploadFileToContainer` method in the TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference to the container using the SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload the file (as a new blob) to the container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when the Batch service
                // sets the CloudTask.ExecutionInformation.ExitCode for the task that
                // executed this application, it properly indicates that there was a
                // problem with the task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="54695-295">Stap 6: taken controleren</span><span class="sxs-lookup"><span data-stu-id="54695-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="54695-296">![Taken controleren][6]</span><span class="sxs-lookup"><span data-stu-id="54695-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="54695-297">
*De clienttoepassing (1) controleert taken op de status Voltooid en Geslaagd en (2) de taken uploaden resultaatgegevens naar Azure Storage*</span><span class="sxs-lookup"><span data-stu-id="54695-297">
*The client application (1) monitors the tasks for completion and success status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="54695-298">Wanneer aan een job taken worden toegevoegd, worden deze automatisch in de wachtrij geplaatst en gepland voor uitvoering op rekenknooppunten binnen de pool die aan de job is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="54695-298">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="54695-299">Op basis van de instellingen die u opgeeft, zal Batch voor u alle taken in de wachtrij plaatsen, plannen en opnieuw proberen uit te voeren, evenals andere taakbeheerverrichtingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="54695-299">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="54695-300">Er zijn veel manieren om de uitvoering van taken te controleren.</span><span class="sxs-lookup"><span data-stu-id="54695-300">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="54695-301">DotNetTutorial toont een eenvoudig voorbeeld waarbij alleen wordt gerapporteerd bij voltooiing en wanneer de taak mislukt of slaagt.</span><span class="sxs-lookup"><span data-stu-id="54695-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="54695-302">Binnen de methode `MonitorTasks` in het DotNetTutorial-bestand `Program.cs` zijn er drie Batch .NET-concepten die discussies garanderen.</span><span class="sxs-lookup"><span data-stu-id="54695-302">Within the `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="54695-303">Ze worden hieronder weergegeven in de volgorde waarin ze voorkomen:</span><span class="sxs-lookup"><span data-stu-id="54695-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="54695-304">**ODATADetailLevel**: [ODATADetailLevel][net_odatadetaillevel] opgeven in lijstbewerkingen (zoals het verkrijgen van een lijst met taken van een job) is essentieel om Batch-toepassingen goed te laten presteren.</span><span class="sxs-lookup"><span data-stu-id="54695-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="54695-305">Voeg het artikel [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) (Efficiënt query's uitvoeren op de Azure Batch-service) toe aan uw leeslijst als u van plan bent een of andere vorm van statuscontrole uit te voeren in uw Batch-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="54695-305">Add [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) to your reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="54695-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] biedt Batch .NET-toepassingen met Help-hulpprogramma's voor het controleren van taakstatuswaarden.</span><span class="sxs-lookup"><span data-stu-id="54695-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="54695-307">In `MonitorTasks` wacht *DotNetTutorial* tot alle taken binnen een bepaalde tijd [TaskState.Completed][net_taskstate] hebben bereikt.</span><span class="sxs-lookup"><span data-stu-id="54695-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks to reach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="54695-308">Daarna wordt de job beëindigd.</span><span class="sxs-lookup"><span data-stu-id="54695-308">Then it terminates the job.</span></span>
3. <span data-ttu-id="54695-309">**TerminateJobAsync**: door een job te beëindigen met [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (of de blokkering JobOperations.TerminateJob), wordt deze job gemarkeerd als voltooid.</span><span class="sxs-lookup"><span data-stu-id="54695-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or the blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="54695-310">Het is essentieel om dit te doen als uw Batch-oplossing gebruikmaakt van een [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="54695-310">It is essential to do so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="54695-311">Dit is een speciaal type taak, dat wordt beschreven in [Job preparation and completion tasks](batch-job-prep-release.md) (Jobvoorbereidings- en jobvoltooiingstaken).</span><span class="sxs-lookup"><span data-stu-id="54695-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="54695-312">De methode `MonitorTasks` uit het *DotNetTutorial*-bestand `Program.cs` wordt hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="54695-312">The `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed to reach the Completed state within the timeout period.";

    // Obtain the collection of tasks currently managed by the job. Note that we use
    // a detail level to  specify that only the "id" property of each task should be
    // populated. Using a detail level for all list operations helps to lower
    // response time from the Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor to monitor the state of our tasks. In this case, we
    // will wait for all tasks to reach the Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached the "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property to ensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update the detail level to populate only the task id and executionInfo
    // properties. We refresh the tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate the task's properties with the latest info from the Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with the task. It is important to note that
            // the task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that the application executed by the task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within the specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="54695-313">Stap 7: taakuitvoer downloaden</span><span class="sxs-lookup"><span data-stu-id="54695-313">Step 7: Download task output</span></span>
<span data-ttu-id="54695-314">![Taakuitvoer downloaden uit Storage][7]</span><span class="sxs-lookup"><span data-stu-id="54695-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="54695-315">Nu de taak is voltooid, kan de uitvoer van de taken worden gedownload uit Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="54695-315">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="54695-316">Dat gebeurt met een aanroep van `DownloadBlobsFromContainerAsync` in het *DotNetTutorial*-bestand `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="54695-316">This is done with a call to `DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference to a previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all the block blobs in the specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference to the current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents to a file in the specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded to {0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="54695-317">De aanroep van `DownloadBlobsFromContainerAsync` in de *DotNetTutorial*-toepassing geeft aan dat de bestanden naar uw map `%TEMP%` moeten worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="54695-317">The call to `DownloadBlobsFromContainerAsync` in the *DotNetTutorial* application specifies that the files should be downloaded to your `%TEMP%` folder.</span></span> <span data-ttu-id="54695-318">U kunt eventueel deze uitvoerlocatie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="54695-318">Feel free to modify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="54695-319">Stap 8: containers verwijderen</span><span class="sxs-lookup"><span data-stu-id="54695-319">Step 8: Delete containers</span></span>
<span data-ttu-id="54695-320">Omdat gegevens die zich in Azure Storage bevinden, in rekening worden gebracht, doet u er altijd goed aan blobs te verwijderen die niet langer nodig zijn voor uw Batch-taken.</span><span class="sxs-lookup"><span data-stu-id="54695-320">Because you are charged for data that resides in Azure Storage, it's always a good idea to remove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="54695-321">In het DotNetTutorial-bestand `Program.cs` wordt dit gedaan met drie aanroepen naar de Help-methode `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="54695-321">In DotNetTutorial's `Program.cs`, this is done with three calls to the helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="54695-322">De methode zelf krijgt alleen een verwijzing naar de container en roept daarna [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete] aan:</span><span class="sxs-lookup"><span data-stu-id="54695-322">The method itself merely obtains a reference to the container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="54695-323">Stap 9: de job en de pool verwijderen</span><span class="sxs-lookup"><span data-stu-id="54695-323">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="54695-324">In de laatste stap wordt u gevraagd de job en de pool te verwijderen die door de DotNetTutorial-toepassing zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="54695-324">In the final step, you're prompted to delete the job and the pool that were created by the DotNetTutorial application.</span></span> <span data-ttu-id="54695-325">Hoewel jobs en taken zelf niet in rekening worden gebracht, worden rekenknooppunten *wel* in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="54695-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="54695-326">Daarom is het raadzaam om knooppunten alleen toe te wijzen als dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="54695-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="54695-327">Het verwijderen van ongebruikte pools kan een onderdeel zijn van uw onderhoudsprocedure.</span><span class="sxs-lookup"><span data-stu-id="54695-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="54695-328">[JobOperations][net_joboperations] en [PoolOperations][net_pooloperations] van BatchClient hebben beide overeenkomstige verwijderingsmethoden, die worden aangeroepen wanneer de gebruiker de verwijdering bevestigt:</span><span class="sxs-lookup"><span data-stu-id="54695-328">The BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if the user confirms deletion:</span></span>

```csharp
// Clean up the resources we've created in the Batch account if the user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> <span data-ttu-id="54695-329">Houd er rekening mee dat rekenresources in rekening worden gebracht. Door ongebruikte pools te verwijderen, beperkt u uw kosten tot een minimum.</span><span class="sxs-lookup"><span data-stu-id="54695-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="54695-330">Denk er ook aan dat een pool alle rekenknooppunten in die pool verwijdert en dat alle gegevens in de knooppunten onherstelbaar zijn nadat de pool wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="54695-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.</span></span>
>
>

## <a name="run-the-dotnettutorial-sample"></a><span data-ttu-id="54695-331">Het *DotNetTutorial*-voorbeeld uitvoeren</span><span class="sxs-lookup"><span data-stu-id="54695-331">Run the *DotNetTutorial* sample</span></span>
<span data-ttu-id="54695-332">Wanneer u de voorbeeldtoepassing uitvoert, lijkt de uitvoer van de console op die hieronder.</span><span class="sxs-lookup"><span data-stu-id="54695-332">When you run the sample application, the console output will be similar to the following.</span></span> <span data-ttu-id="54695-333">Bij het uitvoeren wordt bij `Awaiting task completion, timeout in 00:30:00...` gewacht wanneer de rekenknooppunten van de pool worden gestart.</span><span class="sxs-lookup"><span data-stu-id="54695-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while the pool's compute nodes are started.</span></span> <span data-ttu-id="54695-334">Gebruik [Azure Portal][azure_portal] om uw pool, rekenknooppunten, job en taken tijdens en na de uitvoering te controleren.</span><span class="sxs-lookup"><span data-stu-id="54695-334">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="54695-335">Gebruik [Azure Portal][azure_portal] of [Azure Opslagverkenner][storage_explorers] om de Storage-resources (containers en blobs) weer te geven die door de toepassing zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="54695-335">Use the [Azure portal][azure_portal] or the [Azure Storage Explorer][storage_explorers] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

<span data-ttu-id="54695-336">Wanneer u de toepassing uitvoert in de standaardconfiguratie, bedraagt de uitvoeringstijd doorgaans **ongeveer 5 minuten**.</span><span class="sxs-lookup"><span data-stu-id="54695-336">Typical execution time is **approximately 5 minutes** when you run the application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe to container [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll to container [application]...
Uploading file ..\..\taskdata1.txt to container [input]...
Uploading file ..\..\taskdata2.txt to container [input]...
Uploading file ..\..\taskdata3.txt to container [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks to job [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within the specified timeout period.
Downloading all files from container [output]...
All files downloaded to C:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="54695-337">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="54695-337">Next steps</span></span>
<span data-ttu-id="54695-338">Breng gerust wijzigingen aan in *DotNetTutorial* en *TaskApplication* om met verschillende rekenscenario's te experimenteren.</span><span class="sxs-lookup"><span data-stu-id="54695-338">Feel free to make changes to *DotNetTutorial* and *TaskApplication* to experiment with different compute scenarios.</span></span> <span data-ttu-id="54695-339">Probeer bijvoorbeeld een uitvoeringsvertraging toe te voegen aan *TaskApplication*, bijvoorbeeld met [Thread.Sleep][net_thread_sleep], om langlopende taken te simuleren en ze in de portal te controleren.</span><span class="sxs-lookup"><span data-stu-id="54695-339">For example, try adding an execution delay to *TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="54695-340">Probeer meer taken toe te voegen of het aantal rekenknooppunten aan te passen.</span><span class="sxs-lookup"><span data-stu-id="54695-340">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="54695-341">Voeg logica toe om te controleren op een bestaande pool en het gebruik ervan toe te staan om de uitvoeringssnelheid te verhogen (*hint*: bekijk het bestand `ArticleHelpers.cs` in het project [Microsoft.Azure.Batch.Samples.Common][github_samples_common] in [azure-batch-samples][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="54695-341">Add logic to check for and allow the use of an existing pool to speed execution time (*hint*: check out `ArticleHelpers.cs` in the [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="54695-342">Nu u vertrouwd bent met de basiswerkstroom van een Batch-oplossing, is het tijd om kennis te maken met de aanvullende functies van de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="54695-342">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="54695-343">Lees het artikel [Overzicht van Azure Batch-functies](batch-api-basics.md). Dit is raadzaam als u niet vertrouwd bent met de service.</span><span class="sxs-lookup"><span data-stu-id="54695-343">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="54695-344">Lees ook de andere artikelen over Batch-ontwikkeling die vermeld zijn onder **Ontwikkeling nader bekeken** in het [Batch-leertraject][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="54695-344">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="54695-345">Bekijk een andere implementatie van de verwerking van de workload 'eerste N woorden' met behulp van Batch in het voorbeeld [TopNWords][github_topnwords].</span><span class="sxs-lookup"><span data-stu-id="54695-345">Check out a different implementation of processing the "top N words" workload by using Batch in the [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="54695-346">Bekijk de [opmerkingen bij de release](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) van Batch .NET voor de meest recente wijzigingen in de bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="54695-346">Review the Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for the latest changes in the library.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Containers maken in Azure Storage"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Taaktoepassings- en invoer(gegevens)bestanden uploaden naar containers"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Batch-pool maken"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Batch-job maken"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Taken toevoegen aan job"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Taken controleren"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Taakuitvoer downloaden uit Storage"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Werkstroom van de Batch-oplossing (volledige diagram)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Batch-referenties in Portal"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Storage-referenties in Portal"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Werkstroom van de Batch-oplossing (minimaal diagram)"
