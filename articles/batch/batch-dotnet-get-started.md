---
title: aaaTutorial - gebruik hello Azure Batch-clientbibliotheek voor .NET | Microsoft Docs
description: Leer de basisconcepten Hallo van Azure Batch en bouwen van een eenvoudige oplossing met behulp van .NET.
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
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a><span data-ttu-id="8433b-103">Aan de slag bouwen van oplossingen met Hallo Batch-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="8433b-103">Get started building solutions with hello Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8433b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8433b-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="8433b-105">Python</span><span class="sxs-lookup"><span data-stu-id="8433b-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="8433b-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="8433b-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="8433b-107">Leer de basisbeginselen Hallo van [Azure Batch] [ azure_batch] en Hallo [Batch .NET] [ net_api] bibliotheek in dit artikel als bespreken we een C#-voorbeeld stap toepassing door stap.</span><span class="sxs-lookup"><span data-stu-id="8433b-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="8433b-108">Kijken we hoe Hallo Batch-service tooprocess in Hallo-voorbeeldtoepassing gebruikmaakt van een parallelle workload in Hallo cloud en hoe deze samenwerkt met [Azure Storage](../storage/common/storage-introduction.md) voor Faseren en ophalen.</span><span class="sxs-lookup"><span data-stu-id="8433b-108">We look at how hello sample application leverages hello Batch service tooprocess a parallel workload in hello cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="8433b-109">U hebt meer informatie over een algemene werkstroom voor Batch-toepassing en een elementair inzicht in Hallo belangrijkste onderdelen van Batch zoals jobs, taken, pools en rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="8433b-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="8433b-110">![Werkstroom van de Batch-oplossing (basis)][11]</span><span class="sxs-lookup"><span data-stu-id="8433b-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="8433b-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8433b-111">Prerequisites</span></span>
<span data-ttu-id="8433b-112">In dit artikel wordt ervan uitgegaan dat u praktische kennis hebt van C# en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8433b-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="8433b-113">Ook wordt ervan uitgegaan dat u kunnen toosatisfy Hallo-account maken vereisten die bent hieronder zijn opgegeven voor de Azure- en hello Batch- en opslagservices.</span><span class="sxs-lookup"><span data-stu-id="8433b-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="8433b-114">Accounts</span><span class="sxs-lookup"><span data-stu-id="8433b-114">Accounts</span></span>
* <span data-ttu-id="8433b-115">**Azure-account**: als u nog geen Azure-abonnement hebt, [maakt u een gratis Azure-account][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="8433b-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="8433b-116">**Batch-account**: als u al een Azure-abonnement hebt, [maakt u een Azure Batch-account](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8433b-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="8433b-117">**Opslagaccount**: zie [Een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [Over Azure-opslagaccounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8433b-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8433b-118">Batch ondersteunt momenteel *alleen* hello **algemeen** opslagaccounttype, zoals beschreven in stap &#5; [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [over Azure Storage-accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8433b-118">Batch currently supports *only* hello **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="8433b-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8433b-119">Visual Studio</span></span>
<span data-ttu-id="8433b-120">U moet hebben **Visual Studio 2015 of hoger** toobuild Hallo-voorbeeldproject.</span><span class="sxs-lookup"><span data-stu-id="8433b-120">You must have **Visual Studio 2015 or newer** toobuild hello sample project.</span></span> <span data-ttu-id="8433b-121">U vindt gratis en evaluatieversies van Visual Studio in Hallo [overzicht van Visual Studio-producten][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="8433b-121">You can find free and trial versions of Visual Studio in hello [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="8433b-122">*DotNetTutorial*-codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="8433b-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="8433b-123">Hallo [DotNetTutorial] [ github_dotnettutorial] voorbeeld is een van de vele Batch-codevoorbeelden in Hallo gevonden Hallo [azure-batch-samples] [ github_samples] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="8433b-123">hello [DotNetTutorial][github_dotnettutorial] sample is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="8433b-124">U kunt alle Hallo voorbeelden downloaden door te klikken op **klonen of downloaden > ZIP downloaden** op de startpagina Hallo-opslagplaats of door te klikken op Hallo [azure-batch-samples-master.zip] [ github_samples_zip]directe downloadkoppeling.</span><span class="sxs-lookup"><span data-stu-id="8433b-124">You can download all hello samples by clicking  **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="8433b-125">Nadat u de inhoud van het ZIP-bestand Hallo Hallo hebt uitgepakt, vindt u Hallo oplossing in Hallo volgende map:</span><span class="sxs-lookup"><span data-stu-id="8433b-125">Once you've extracted hello contents of hello ZIP file, you can find hello solution in hello following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="8433b-126">Azure Batch Explorer (optioneel)</span><span class="sxs-lookup"><span data-stu-id="8433b-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="8433b-127">Hallo [Azure Batch Explorer] [ github_batchexplorer] is een gratis hulpprogramma dat is opgenomen in Hallo [azure-batch-samples] [ github_samples] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="8433b-127">hello [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="8433b-128">Tijdens het niet vereist toocomplete in deze zelfstudie, dit kan nuttig zijn bij de ontwikkeling en foutopsporing van uw Batch-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="8433b-128">While not required toocomplete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="8433b-129">Overzicht DotNetTutorial-voorbeeldproject</span><span class="sxs-lookup"><span data-stu-id="8433b-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="8433b-130">Hallo *DotNetTutorial* codevoorbeeld is een Visual Studio-oplossing die uit twee projecten bestaat: **DotNetTutorial** en **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="8433b-130">hello *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="8433b-131">**DotNetTutorial** is Hallo-clienttoepassing die met de Hallo Batch- en Storage services tooexecute een parallelle workload op rekenknooppunten (virtuele machines communiceert).</span><span class="sxs-lookup"><span data-stu-id="8433b-131">**DotNetTutorial** is hello client application that interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="8433b-132">DotNetTutorial wordt uitgevoerd op uw lokale werkstation.</span><span class="sxs-lookup"><span data-stu-id="8433b-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="8433b-133">**TaskApplication** is Hallo programma dat wordt uitgevoerd op rekenknooppunten in Azure tooperform Hallo echte werk.</span><span class="sxs-lookup"><span data-stu-id="8433b-133">**TaskApplication** is hello program that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="8433b-134">In voorbeeld Hallo `TaskApplication.exe` parseert Hallo tekst in een bestand gedownload van Azure Storage (Hallo-invoerbestand).</span><span class="sxs-lookup"><span data-stu-id="8433b-134">In hello sample, `TaskApplication.exe` parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="8433b-135">En vervolgens het genereert een tekstbestand (Hallo uitvoerbestand) die een lijst van Hallo eerste drie woorden die worden weergegeven in het invoerbestand Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="8433b-135">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="8433b-136">Nadat het Hallo-uitvoerbestand heeft gemaakt, uploadt TaskApplication Hallo bestand tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="8433b-136">After it creates hello output file, TaskApplication uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="8433b-137">Hierdoor kunt u de clienttoepassing beschikbaar toohello downloaden.</span><span class="sxs-lookup"><span data-stu-id="8433b-137">This makes it available toohello client application for download.</span></span> <span data-ttu-id="8433b-138">TaskApplication wordt parallel uitgevoerd op meerdere rekenknooppunten in Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="8433b-138">TaskApplication runs in parallel on multiple compute nodes in hello Batch service.</span></span>

<span data-ttu-id="8433b-139">Hallo volgende diagram illustreert Hallo primaire bewerkingen die worden uitgevoerd door de clienttoepassing Hallo *DotNetTutorial*, en het Hallo-toepassing die wordt uitgevoerd door Hallo-taken *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="8433b-139">hello following diagram illustrates hello primary operations that are performed by hello client application, *DotNetTutorial*, and hello application that is executed by hello tasks, *TaskApplication*.</span></span> <span data-ttu-id="8433b-140">Deze basiswerkstroom is typerend voor vele rekenoplossingen die met Batch worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8433b-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="8433b-141">Hoewel hierin niet elke beschikbare functie in Hallo Batch-service, omvat vrijwel elk Batch-scenario gedeelten van deze werkstroom.</span><span class="sxs-lookup"><span data-stu-id="8433b-141">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="8433b-142">![Batch-voorbeeldwerkstroom][8]</span><span class="sxs-lookup"><span data-stu-id="8433b-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="8433b-143">**Stap 1.**</span><span class="sxs-lookup"><span data-stu-id="8433b-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="8433b-144">Maak **containers** in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="8433b-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="8433b-145">
[**Stap 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="8433b-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="8433b-146">Upload taaktoepassings- en invoerbestanden toocontainers.</span><span class="sxs-lookup"><span data-stu-id="8433b-146">Upload task application files and input files toocontainers.</span></span><br/><span data-ttu-id="8433b-147">
[**Stap 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="8433b-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="8433b-148">Maak een Batch-**pool**.</span><span class="sxs-lookup"><span data-stu-id="8433b-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="8433b-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="8433b-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="8433b-150">Hallo groep **StartTask** downloads Hallo taak binaire bestanden (TaskApplication) toonodes wanneer ze aan Hallo groep worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="8433b-150">hello pool **StartTask** downloads hello task binary files (TaskApplication) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="8433b-151">
[**Stap 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="8433b-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="8433b-152">Maak een Batch-**job**.</span><span class="sxs-lookup"><span data-stu-id="8433b-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="8433b-153">
[**Stap 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="8433b-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="8433b-154">Voeg **taken** toohello taak.</span><span class="sxs-lookup"><span data-stu-id="8433b-154">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="8433b-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="8433b-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="8433b-156">Hallo-taken zijn gepland tooexecute op knooppunten.</span><span class="sxs-lookup"><span data-stu-id="8433b-156">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="8433b-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="8433b-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="8433b-158">Elke taak downloadt de bijbehorende invoergegevens uit Azure Storage en wordt daarna uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8433b-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="8433b-159">
[**Stap 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="8433b-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="8433b-160">Controleer taken.</span><span class="sxs-lookup"><span data-stu-id="8433b-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="8433b-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="8433b-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="8433b-162">Nadat taken zijn voltooid, uploaden zij hun uitvoer gegevens tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="8433b-162">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="8433b-163">
[**Stap 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="8433b-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="8433b-164">Download taakuitvoer uit Storage.</span><span class="sxs-lookup"><span data-stu-id="8433b-164">Download task output from Storage.</span></span>

<span data-ttu-id="8433b-165">Zoals gezegd, niet elke Batch-oplossing deze exacte stappen worden uitgevoerd en kan nog veel meer bevatten, maar Hallo *DotNetTutorial* voorbeeldtoepassing toont de algemene processen die in een Batch-oplossing.</span><span class="sxs-lookup"><span data-stu-id="8433b-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but hello *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-hello-dotnettutorial-sample-project"></a><span data-ttu-id="8433b-166">Hallo bouwen *DotNetTutorial* voorbeeldproject</span><span class="sxs-lookup"><span data-stu-id="8433b-166">Build hello *DotNetTutorial* sample project</span></span>
<span data-ttu-id="8433b-167">Voordat u Hallo voorbeeld met succes uitvoeren kunt, moet u de Batch- en Storage-accountreferenties opgeven in Hallo *DotNetTutorial* van het project `Program.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="8433b-167">Before you can successfully run hello sample, you must specify both Batch and Storage account credentials in hello *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="8433b-168">Als u dit nog niet hebt gedaan, opent u Hallo oplossing in Visual Studio door te dubbelklikken op Hallo `DotNetTutorial.sln` oplossingsbestand.</span><span class="sxs-lookup"><span data-stu-id="8433b-168">If you have not done so already, open hello solution in Visual Studio by double-clicking hello `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="8433b-169">Openen in Visual Studio met behulp van Hallo **bestand > openen > Project/oplossing** menu.</span><span class="sxs-lookup"><span data-stu-id="8433b-169">Or open it from within Visual Studio by using hello **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="8433b-170">Open `Program.cs` binnen Hallo *DotNetTutorial* project.</span><span class="sxs-lookup"><span data-stu-id="8433b-170">Open `Program.cs` within hello *DotNetTutorial* project.</span></span> <span data-ttu-id="8433b-171">Voeg vervolgens uw referenties toe zoals opgegeven in de buurt Hallo bovenaan Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="8433b-171">Then add your credentials as specified near hello top of hello file:</span></span>

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="8433b-172">Zoals eerder vermeld, moet u momenteel opgeven Hallo referenties voor een **algemeen** storage-account in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8433b-172">As mentioned above, you must currently specify hello credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="8433b-173">Uw Batch-toepassingen gebruiken blob storage in Hallo **algemeen** storage-account.</span><span class="sxs-lookup"><span data-stu-id="8433b-173">Your Batch applications use blob storage within hello **general-purpose** storage account.</span></span> <span data-ttu-id="8433b-174">Geef geen referenties voor een opslagaccount dat is gemaakt door het selecteren van Hallo Hallo *Blob storage* accounttype.</span><span class="sxs-lookup"><span data-stu-id="8433b-174">Do not specify hello credentials for a Storage account that was created by selecting hello *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="8433b-175">U vindt uw Batch- en Storage-accountreferenties op Hallo accountblade van elke service op Hallo [Azure-portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="8433b-175">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="8433b-176">![Batch-referenties in portal Hallo][9]
![Storage-referenties in portal Hallo][10]</span><span class="sxs-lookup"><span data-stu-id="8433b-176">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="8433b-177">Nu dat u Hallo-project met uw referenties hebt bijgewerkt, met de rechtermuisknop op het Hallo-oplossing in Solution Explorer en klikt u op **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="8433b-177">Now that you've updated hello project with your credentials, right-click hello solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="8433b-178">Bevestig Hallo herstel van alle NuGet-pakketten als u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="8433b-178">Confirm hello restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="8433b-179">Zorg ervoor dat er Hallo als Hallo NuGet-pakketten niet automatisch worden hersteld of als er fouten over een mislukte toorestore hello-pakketten, [NuGet Package Manager] [ nuget_packagemgr] geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8433b-179">If hello NuGet packages are not automatically restored, or if you see errors about a failure toorestore hello packages, ensure that you have hello [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="8433b-180">Schakel vervolgens Hallo downloaden van ontbrekende pakketten.</span><span class="sxs-lookup"><span data-stu-id="8433b-180">Then enable hello download of missing packages.</span></span> <span data-ttu-id="8433b-181">Zie [inschakelen pakket herstellen tijdens bouwen] [ nuget_restore] tooenable pakket downloaden.</span><span class="sxs-lookup"><span data-stu-id="8433b-181">See [Enabling Package Restore During Build][nuget_restore] tooenable package download.</span></span>
>
>

<span data-ttu-id="8433b-182">In Hallo uit te voeren, we Hallo voorbeeldtoepassing uitgesplitst in Hallo stappen die het tooprocess uitvoert een workload in Hallo Batch-service en worden die stappen in detail.</span><span class="sxs-lookup"><span data-stu-id="8433b-182">In hello following sections, we break down hello sample application into hello steps that it performs tooprocess a workload in hello Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="8433b-183">We raden u toorefer toohello geopende oplossing in Visual Studio terwijl u zich door de rest van dit artikel Hallo werkt, omdat niet elke regel code in Hallo voorbeeld wordt besproken.</span><span class="sxs-lookup"><span data-stu-id="8433b-183">We encourage you toorefer toohello open solution in Visual Studio while you work your way through hello rest of this article, since not every line of code in hello sample is discussed.</span></span>

<span data-ttu-id="8433b-184">Navigeer toohello bovenaan Hallo `MainAsync` methode in Hallo *DotNetTutorial* van het project `Program.cs` bestand toostart bij stap 1.</span><span class="sxs-lookup"><span data-stu-id="8433b-184">Navigate toohello top of hello `MainAsync` method in hello *DotNetTutorial* project's `Program.cs` file toostart with Step 1.</span></span> <span data-ttu-id="8433b-185">Elke stap hieronder vervolgens ongeveer volgt Hallo voortgang van de methode aanroept `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="8433b-185">Each step below then roughly follows hello progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="8433b-186">Stap 1: opslagcontainers maken</span><span class="sxs-lookup"><span data-stu-id="8433b-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="8433b-187">![Containers maken in Azure Storage][1]
</span><span class="sxs-lookup"><span data-stu-id="8433b-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="8433b-188">Batch bevat ingebouwde ondersteuning voor interactie met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8433b-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="8433b-189">Containers in uw opslagaccount biedt Hallo-bestanden die nodig zijn door Hallo-taken die worden uitgevoerd in uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="8433b-189">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="8433b-190">Hallo containers bieden ook een uitvoergegevens van plaats toostore Hallo die Hallo taken opleveren.</span><span class="sxs-lookup"><span data-stu-id="8433b-190">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="8433b-191">Hallo eerst te beginnen Hallo *DotNetTutorial* clienttoepassing biedt is drie containers maken in [Azure Blob Storage](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="8433b-191">hello first thing hello *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="8433b-192">**toepassing**: deze container slaat Hallo toepassing hello taken, evenals alle afhankelijkheden hiervan, zoals dll's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8433b-192">**application**: This container will store hello application run by hello tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="8433b-193">**invoer**: taken downloaden de Hallo gegevens bestanden tooprocess vanaf Hallo *invoer* container.</span><span class="sxs-lookup"><span data-stu-id="8433b-193">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="8433b-194">**uitvoer**: bij de verwerking van invoerbestanden taken hebt voltooid, uploaden zij Hallo resultaten toohello *uitvoer* container.</span><span class="sxs-lookup"><span data-stu-id="8433b-194">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="8433b-195">In de volgorde toointeract met een Storage-account in en containers, maken we hello gebruiken [Azure Storage-clientbibliotheek voor .NET][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="8433b-195">In order toointeract with a Storage account and create containers, we use hello [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="8433b-196">We maken een verwijzing toohello-account met [CloudStorageAccount][net_cloudstorageaccount], en van hieruit maken een [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="8433b-196">We create a reference toohello account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="8433b-197">We gebruiken Hallo `blobClient` verwijzing in de toepassing hello en tooseveral methoden doorgegeven als parameter.</span><span class="sxs-lookup"><span data-stu-id="8433b-197">We use hello `blobClient` reference throughout hello application and pass it as a parameter tooseveral methods.</span></span> <span data-ttu-id="8433b-198">Een voorbeeld hiervan is in Hallo codeblok dat onmiddellijk volgt Hallo bovenstaande waar we noemen `CreateContainerIfNotExistAsync` tooactually Hallo containers te maken.</span><span class="sxs-lookup"><span data-stu-id="8433b-198">An example of this is in hello code block that immediately follows hello above, where we call `CreateContainerIfNotExistAsync` tooactually create hello containers.</span></span>

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
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

<span data-ttu-id="8433b-199">Zodra het Hallo-containers zijn gemaakt, Hallo toepassing kan nu Hallo bestanden uploaden die wordt gebruikt door Hallo taken.</span><span class="sxs-lookup"><span data-stu-id="8433b-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="8433b-200">[Hoe toouse Blob Storage in .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) biedt een goed overzicht van het werken met Azure Storage-containers en blobs.</span><span class="sxs-lookup"><span data-stu-id="8433b-200">[How toouse Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="8433b-201">Deze moet aan de bovenkant Hallo van uw leeslijst als u met Batch begint te werken.</span><span class="sxs-lookup"><span data-stu-id="8433b-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="8433b-202">Stap 2: taaktoepassings- en gegevensbestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="8433b-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="8433b-203">![Het uploaden van taak toepassing en invoer (gegevens) bestanden toocontainers][2]
</span><span class="sxs-lookup"><span data-stu-id="8433b-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="8433b-204">In Hallo uploaden bewerking *DotNetTutorial* definieert eerst verzamelingen van **toepassing** en **invoer** bestandspaden die op de lokale machine Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="8433b-204">In hello file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="8433b-205">Vervolgens wordt deze bestanden toohello containers die u hebt gemaakt in de vorige stap Hallo geüpload.</span><span class="sxs-lookup"><span data-stu-id="8433b-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="8433b-206">Er zijn twee methoden in `Program.cs` die betrokken zijn bij het uploadproces Hallo:</span><span class="sxs-lookup"><span data-stu-id="8433b-206">There are two methods in `Program.cs` that are involved in hello upload process:</span></span>

* <span data-ttu-id="8433b-207">`UploadFilesToContainerAsync`: Deze methode retourneert een verzameling [ResourceFile] [ net_resourcefile] objecten (Zie hieronder) en roept intern `UploadFileToContainerAsync` tooupload elk bestand dat wordt doorgegeven in Hallo *filePaths* parameter.</span><span class="sxs-lookup"><span data-stu-id="8433b-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` tooupload each file that is passed in hello *filePaths* parameter.</span></span>
* <span data-ttu-id="8433b-208">`UploadFileToContainerAsync`: Dit is Hallo-methode die daadwerkelijk Hallo-bestand uploaden uitvoert en maakt Hallo [ResourceFile] [ net_resourcefile] objecten.</span><span class="sxs-lookup"><span data-stu-id="8433b-208">`UploadFileToContainerAsync`: This is hello method that actually performs hello file upload and creates hello [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="8433b-209">Na het Hallo-bestand uploadt, het verkrijgt een shared access signature (SAS) voor het Hallo-bestand en retourneert een ResourceFile-object dat vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="8433b-209">After uploading hello file, it obtains a shared access signature (SAS) for hello file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="8433b-210">Ook Shared Access Signatures worden hieronder besproken.</span><span class="sxs-lookup"><span data-stu-id="8433b-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="8433b-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="8433b-211">ResourceFiles</span></span>
<span data-ttu-id="8433b-212">Een [ResourceFile] [ net_resourcefile] biedt taken in Batch met Hallo URL tooa bestand in Azure Storage dat is gedownload tooa rekenknooppunt voordat deze taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8433b-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="8433b-213">Hallo [ResourceFile.BlobSource] [ net_resourcefile_blobsource] eigenschap geeft u de volledige URL Hallo van Hallo-bestand zoals dit zich in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8433b-213">hello [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="8433b-214">Hallo-URL kan ook een shared access signature (SAS) waarmee u veilige toegang tot toohello bestand bevatten.</span><span class="sxs-lookup"><span data-stu-id="8433b-214">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="8433b-215">De meeste typen taken in Batch .NET bevatten een eigenschap *ResourceFiles*, waaronder:</span><span class="sxs-lookup"><span data-stu-id="8433b-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="8433b-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="8433b-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="8433b-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="8433b-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="8433b-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="8433b-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="8433b-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="8433b-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="8433b-220">Hallo DotNetTutorial-voorbeeldtoepassing gebruikt niet Hallo JobPreparationTask of JobReleaseTask taaktypen maar vindt u meer informatie hierover in [uitvoeren jobvoorbereidingstaken en jobvrijgevingstaken taken op Azure Batch-rekenknooppunten](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="8433b-220">hello DotNetTutorial sample application does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="8433b-221">Shared Access Signature (SAS)</span><span class="sxs-lookup"><span data-stu-id="8433b-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="8433b-222">Shared access signatures zijn tekenreeksen die, wanneer ze deel uitmaken van een URL, bieden veilige toegang toocontainers en blobs in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8433b-222">Shared access signatures are strings which—when included as part of a URL—provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="8433b-223">Hallo DotNetTutorial-toepassing gebruikt blobs en container shared access signature-URL en laat zien hoe deze gedeelde tooobtain vanaf toegang tot tekenreeksen Hallo Storage-service.</span><span class="sxs-lookup"><span data-stu-id="8433b-223">hello DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="8433b-224">**Shared access signatures voor blobs**: StartTask van Hallo pool in DotNetTutorial maakt gebruik van handtekeningen voor gedeelde blob-toegang wanneer het Hallo binaire bestanden van toepassingen en invoergegevensbestanden uit Storage downloadt (Zie stap 3 hieronder).</span><span class="sxs-lookup"><span data-stu-id="8433b-224">**Blob shared access signatures**: hello pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads hello application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="8433b-225">Hallo `UploadFileToContainerAsync` methode in het DotNetTutorial `Program.cs` bevat Hallo-code die shared access signature van elke blob verkrijgt.</span><span class="sxs-lookup"><span data-stu-id="8433b-225">hello `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="8433b-226">Dit gebeurt door het aanroepen van [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span><span class="sxs-lookup"><span data-stu-id="8433b-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="8433b-227">**Container shared access signatures**: als elke taak zijn werk heeft verricht op Hallo rekenknooppunt, uploadt het bestand uitvoer toohello *uitvoer* container in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8433b-227">**Container shared access signatures**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="8433b-228">toodo dus maakt TaskApplication gebruik van een shared access signature voor containers die schrijftoegang toohello container als onderdeel van Hallo pad biedt, wanneer het Hallo-bestand wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="8433b-228">toodo so, TaskApplication uses a container shared access signature that provides write access toohello container as part of hello path when it uploads hello file.</span></span> <span data-ttu-id="8433b-229">Shared access signature voor het ophalen van Hallo container wordt uitgevoerd op een vergelijkbare manier als wanneer het verkrijgen van Hallo blob toegangshandtekening gedeeld.</span><span class="sxs-lookup"><span data-stu-id="8433b-229">Obtaining hello container shared access signature is done in a similar fashion as when obtaining hello blob shared access signature.</span></span> <span data-ttu-id="8433b-230">In DotNetTutorial zult u die Hallo `GetContainerSasUrl` helper methodeaanroepen [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo zodat.</span><span class="sxs-lookup"><span data-stu-id="8433b-230">In DotNetTutorial, you will find that hello `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] toodo so.</span></span> <span data-ttu-id="8433b-231">U moet lees meer over hoe TaskApplication Hallo container gebruikt gedeelde-toegangshandtekening in ' stap 6: taken controleren. '</span><span class="sxs-lookup"><span data-stu-id="8433b-231">You'll read more about how TaskApplication uses hello container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="8433b-232">Uitchecken Hallo tweedelige reeks over handtekeningen voor gedeelde toegang [deel 1: Understanding Hallo shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) en [deel 2: maken en een shared access signature (SAS) gebruiken met Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn meer over het opgeven van beveiligde toegang toodata in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8433b-232">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="8433b-233">Stap 3: Batch-pool maken</span><span class="sxs-lookup"><span data-stu-id="8433b-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="8433b-234">![Een Batch-pool maken][3]
</span><span class="sxs-lookup"><span data-stu-id="8433b-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="8433b-235">Een Batch-**pool** is een verzameling rekenknooppunten (virtuele machines) waarop Batch de taken van een job uitvoert.</span><span class="sxs-lookup"><span data-stu-id="8433b-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="8433b-236">Na het uploaden van de toepassing hello en gegevens bestanden toohello Storage-account met Azure Storage-API's *DotNetTutorial* begonnen met het aanbrengen van aanroepen toohello Batch-service met API's die worden geleverd door Hallo Batch .NET-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="8433b-236">After uploading hello application and data files toohello Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls toohello Batch service with APIs provided by hello Batch .NET library.</span></span> <span data-ttu-id="8433b-237">Hallo code maakt eerst een [BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="8433b-237">hello code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="8433b-238">Vervolgens Hallo voorbeeld maakt u een pool van rekenknooppunten in Hallo Batch-account met een aanroep te`CreatePoolIfNotExistsAsync`.</span><span class="sxs-lookup"><span data-stu-id="8433b-238">Next, hello sample creates a pool of compute nodes in hello Batch account with a call too`CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="8433b-239">`CreatePoolIfNotExistsAsync`maakt gebruik van Hallo [BatchClient.PoolOperations.CreatePool] [ net_pool_create] methode toocreate een nieuwe groep in Hallo Batch-service:</span><span class="sxs-lookup"><span data-stu-id="8433b-239">`CreatePoolIfNotExistsAsync` uses hello [BatchClient.PoolOperations.CreatePool][net_pool_create] method toocreate a new pool in hello Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="8433b-240">Wanneer u een pool maakt met [CreatePool][net_pool_create], u verschillende parameters zoals het aantal rekenknooppunten, Hallo Hallo [grootte van de knooppunten Hallo](../cloud-services/cloud-services-sizes-specs.md), en Hallo knooppunten besturingssysteem systeem.</span><span class="sxs-lookup"><span data-stu-id="8433b-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as hello number of compute nodes, hello [size of hello nodes](../cloud-services/cloud-services-sizes-specs.md), and hello nodes' operating system.</span></span> <span data-ttu-id="8433b-241">In *DotNetTutorial*, gebruiken we [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 van [Cloudservices](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="8433b-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="8433b-242">U kunt ook pools van rekenknooppunten die Azure Virtual Machines (VM's zijn) maken door op te geven Hallo [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8433b-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying hello [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="8433b-243">U kunt een pool van VM-rekenknooppunten maken vanuit een Windows of [Linux-installatiekopie](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="8433b-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="8433b-244">Hallo-bron voor VM-installatiekopieën kan zijn:</span><span class="sxs-lookup"><span data-stu-id="8433b-244">hello source for your VM images can be either:</span></span>

- <span data-ttu-id="8433b-245">Hallo [Azure Virtual Machines Marketplace][vm_marketplace], waarmee u Windows- en Linux-installatiekopieën die kant-en-klare zijn.</span><span class="sxs-lookup"><span data-stu-id="8433b-245">hello [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="8433b-246">Een aangepaste installatiekopie die u voorbereidt en aanlevert.</span><span class="sxs-lookup"><span data-stu-id="8433b-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="8433b-247">Zie [Grootschalige parallelle rekenoplossingen ontwikkelen met Batch](batch-api-basics.md#pool) voor meer informatie over aangepaste installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="8433b-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8433b-248">De rekenresources in Batch worden in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="8433b-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="8433b-249">toominimize kosten, kunt u het verlagen `targetDedicatedComputeNodes` too1 voordat u Hallo voorbeeld uitvoert.</span><span class="sxs-lookup"><span data-stu-id="8433b-249">toominimize costs, you can lower `targetDedicatedComputeNodes` too1 before you run hello sample.</span></span>
>
>

<span data-ttu-id="8433b-250">Samen met deze fysieke knooppunteigenschappen, kunt u ook opgeven een [StartTask] [ net_pool_starttask] voor Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8433b-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for hello pool.</span></span> <span data-ttu-id="8433b-251">Hallo StartTask wordt uitgevoerd op elk knooppunt, zoals u dat knooppunt aan Hallo-pool wordt toegevoegd en telkens wanneer een knooppunt opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="8433b-251">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="8433b-252">Hallo StartTask is vooral nuttig voor het installeren van toepassingen op compute knooppunten voorafgaande toohello uitvoering van taken.</span><span class="sxs-lookup"><span data-stu-id="8433b-252">hello StartTask is especially useful for installing applications on compute nodes prior toohello execution of tasks.</span></span> <span data-ttu-id="8433b-253">Bijvoorbeeld, als uw taken gegevens verwerken met behulp van Python-scripts, kunt u een StartTask tooinstall Python op Hallo rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="8433b-253">For example, if your tasks process data by using Python scripts, you could use a StartTask tooinstall Python on hello compute nodes.</span></span>

<span data-ttu-id="8433b-254">In deze voorbeeldtoepassing kopieert StartTask Hallo Hallo-bestanden die het van Storage downloadt (die zijn opgegeven met behulp van Hallo [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] eigenschap) vanuit Hallo StartTask directory toohello gedeelde werkmap die *alle* taken op Hallo knooppunt uitgevoerd toegang hebben.</span><span class="sxs-lookup"><span data-stu-id="8433b-254">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from hello StartTask working directory toohello shared directory that *all* tasks running on hello node can access.</span></span> <span data-ttu-id="8433b-255">In wezen Hiermee kopieert u `TaskApplication.exe` en de afhankelijkheden toohello gedeelde map in elk knooppunt zoals Hallo knooppunt lid van groep Hallo, zodat alle taken die worden uitgevoerd op Hallo-knooppunt toegang deze tot.</span><span class="sxs-lookup"><span data-stu-id="8433b-255">Essentially, this copies `TaskApplication.exe` and its dependencies toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="8433b-256">Hallo **toepassingspakketten** functie van Azure Batch biedt een andere manier tooget uw toepassing op Hallo van rekenknooppunten in een pool.</span><span class="sxs-lookup"><span data-stu-id="8433b-256">hello **application packages** feature of Azure Batch provides another way tooget your application onto hello compute nodes in a pool.</span></span> <span data-ttu-id="8433b-257">Zie [implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten](batch-application-packages.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8433b-257">See [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="8433b-258">Opmerkelijk in bovenstaande Hallo codefragment is ook gebruik van twee omgevingsvariabelen in Hallo Hallo *CommandLine* eigenschap Hallo StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` en `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="8433b-258">Also notable in hello code snippet above is hello use of two environment variables in hello *CommandLine* property of hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="8433b-259">Elk rekenknooppunt in een Batch-pool wordt automatisch geconfigureerd met meerdere omgevingsvariabelen die specifiek tooBatch zijn.</span><span class="sxs-lookup"><span data-stu-id="8433b-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="8433b-260">Een proces dat wordt uitgevoerd door een taak heeft toegang tot toothese omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="8433b-260">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="8433b-261">toofind voor meer informatie over Hallo omgevingsvariabelen die beschikbaar op rekenknooppunten in een Batch-pool en informatie over taakwerkmappen zijn, Zie Hallo [omgevingsinstellingen voor taken](batch-api-basics.md#environment-settings-for-tasks) en [bestanden en mappen ](batch-api-basics.md#files-and-directories) secties in Hallo [overzicht van de Batch-functies voor ontwikkelaars](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="8433b-261">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see hello [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in hello [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="8433b-262">Stap 4: Batch-job maken</span><span class="sxs-lookup"><span data-stu-id="8433b-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="8433b-263">![Een Batch-job maken][4]</span><span class="sxs-lookup"><span data-stu-id="8433b-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="8433b-264">Een Batch-**job** is een verzameling taken en is gekoppeld aan een pool van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="8433b-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="8433b-265">Hallo-taken in een taak uitgevoerd op de rekenknooppunten van de pool Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8433b-265">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="8433b-266">U kunt een job niet alleen voor het organiseren en te volgen taken in gerelateerde workloads, maar ook voor de toepassing van bepaalde beperkingen--zoals Hallo maximale runtime voor Hallo job (en bij uitbreiding, de taken ervan) en de taakprioriteit van de in de relatie tooother taken in Batch Hallo account.</span><span class="sxs-lookup"><span data-stu-id="8433b-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) as well as job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="8433b-267">In dit voorbeeld is Hallo-taak echter alleen gekoppeld aan Hallo-groep die is gemaakt in stap #3.</span><span class="sxs-lookup"><span data-stu-id="8433b-267">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="8433b-268">Er worden geen aanvullende eigenschappen geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8433b-268">No additional properties are configured.</span></span>

<span data-ttu-id="8433b-269">Alle Batch-jobs worden gekoppeld aan een specifieke pool.</span><span class="sxs-lookup"><span data-stu-id="8433b-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="8433b-270">Deze koppeling geeft aan welke knooppunten Hallo taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8433b-270">This association indicates which nodes hello job's tasks will execute on.</span></span> <span data-ttu-id="8433b-271">U geeft dit met behulp van Hallo [CloudJob.PoolInformation] [ net_job_poolinfo] eigenschap, zoals wordt weergegeven in onderstaande Hallo codefragment.</span><span class="sxs-lookup"><span data-stu-id="8433b-271">You specify this by using hello [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in hello code snippet below.</span></span>

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

<span data-ttu-id="8433b-272">Nu dat een taak is gemaakt, worden taken tooperform Hallo werk toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="8433b-272">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="8433b-273">Stap 5: Taken toojob toevoegen</span><span class="sxs-lookup"><span data-stu-id="8433b-273">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="8433b-274">![Taken toojob toevoegen][5]</span><span class="sxs-lookup"><span data-stu-id="8433b-274">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="8433b-275">
*(1) taken toohello taak worden toegevoegd, (2) Hallo taken zijn gepland toorun op knooppunten en (3) Hallo taken Hallo gegevens bestanden tooprocess downloaden*</span><span class="sxs-lookup"><span data-stu-id="8433b-275">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="8433b-276">Batch **taken** zijn Hallo afzonderlijke werkeenheden die worden uitgevoerd op Hallo van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="8433b-276">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="8433b-277">Een taak heeft een opdrachtregel en voert Hallo scripts of uitvoerbare bestanden die u in die opdrachtregel opgeeft.</span><span class="sxs-lookup"><span data-stu-id="8433b-277">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="8433b-278">tooactually werk verrichten en taken tooa taak moeten worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="8433b-278">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="8433b-279">Elke [CloudTask] [ net_task] wordt geconfigureerd met behulp van een opdrachtregeleigenschap en [ResourceFiles] [ net_task_resourcefiles] (net als bij StartTask van Hallo pool) die Hallo taak downloadt toohello knooppunt voordat de opdrachtregel ervan automatisch wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8433b-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="8433b-280">In Hallo *DotNetTutorial* voorbeeldproject, elke taak slechts één bestand wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="8433b-280">In hello *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="8433b-281">Hierdoor bevat de verzameling ResourceFiles één element.</span><span class="sxs-lookup"><span data-stu-id="8433b-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
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

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="8433b-282">Wanneer ze toegang krijgen tot omgevingsvariabelen zoals `%AZ_BATCH_NODE_SHARED_DIR%` of een toepassing niet gevonden in het Hallo-knooppunt uitvoeren `PATH`, opdrachtregels taak moet worden voorafgegaan door `cmd /c`.</span><span class="sxs-lookup"><span data-stu-id="8433b-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in hello node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="8433b-283">Hiermee wordt expliciet Hallo opdrachtinterpreter uitgevoerd en krijgt deze de instructie tooterminate nadat uw opdracht is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8433b-283">This will explicitly execute hello command interpreter and instruct it tooterminate after carrying out your command.</span></span> <span data-ttu-id="8433b-284">Deze vereiste is niet nodig als uw taken een toepassing in Hallo-knooppunt uitvoeren `PATH` (zoals *robocopy.exe* of *powershell.exe*) en er geen omgevingsvariabelen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8433b-284">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="8433b-285">Binnen Hallo `foreach` lus in bovenstaande Hallo codefragment, kunt u zien dat Hallo vanaf de opdrachtregel voor Hallo taak zodanig is opgesteld dat drie opdrachtregelargumenten te worden doorgegeven*TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="8433b-285">Within hello `foreach` loop in hello code snippet above, you can see that hello command line for hello task is constructed such that three command-line arguments are passed too*TaskApplication.exe*:</span></span>

1. <span data-ttu-id="8433b-286">Hallo **eerste argument** Hallo Hallo bestand tooprocess pad is.</span><span class="sxs-lookup"><span data-stu-id="8433b-286">hello **first argument** is hello path of hello file tooprocess.</span></span> <span data-ttu-id="8433b-287">Dit is Hallo lokaal pad toohello bestand zoals dit zich op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="8433b-287">This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="8433b-288">Wanneer Hallo ResourceFile-object in `UploadFileToContainerAsync` is gemaakt, Hallo bestandsnaam voor deze eigenschap is gebruikt (als een parameter constructor ResourceFile toohello).</span><span class="sxs-lookup"><span data-stu-id="8433b-288">When hello ResourceFile object in `UploadFileToContainerAsync` was first created above, hello file name was used for this property (as a parameter toohello ResourceFile constructor).</span></span> <span data-ttu-id="8433b-289">Dit geeft aan dat Hallo-bestand kan worden gevonden in Hallo dezelfde map als *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="8433b-289">This indicates that hello file can be found in hello same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="8433b-290">Hallo **tweede argument** die boven Hallo *N* woorden moeten toohello uitvoerbestand worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="8433b-290">hello **second argument** specifies that hello top *N* words should be written toohello output file.</span></span> <span data-ttu-id="8433b-291">In de steekproef hello, dit in code vastgelegd zodat de eerste drie woorden Hallo toohello uitvoerbestand worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="8433b-291">In hello sample, this is hard-coded so that hello top three words are written toohello output file.</span></span>
3. <span data-ttu-id="8433b-292">Hallo **derde argument** is Hallo shared access signature (SAS) die schrijftoegang toohello biedt **uitvoer** container in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8433b-292">hello **third argument** is hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="8433b-293">*TaskApplication.exe* gebruikt deze shared access signature-URL wanneer het Hallo uitvoer bestand tooAzure Storage uploadt.</span><span class="sxs-lookup"><span data-stu-id="8433b-293">*TaskApplication.exe* uses this shared access signature URL when it uploads hello output file tooAzure Storage.</span></span> <span data-ttu-id="8433b-294">U vindt Hallo code voor deze in Hallo `UploadFileToContainer` methode in Hallo TaskApplication project `Program.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="8433b-294">You can find hello code for this in hello `UploadFileToContainer` method in hello TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
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

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="8433b-295">Stap 6: taken controleren</span><span class="sxs-lookup"><span data-stu-id="8433b-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="8433b-296">![Taken controleren][6]</span><span class="sxs-lookup"><span data-stu-id="8433b-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="8433b-297">
*Hallo client-toepassing (1) monitors Hallo taken voor de status voltooid en geslaagd en (2) Hallo taken uploaden resultaat gegevens tooAzure opslag*</span><span class="sxs-lookup"><span data-stu-id="8433b-297">
*hello client application (1) monitors hello tasks for completion and success status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="8433b-298">Wanneer taken zijn tooa taak toegevoegd, worden ze automatisch in de wachtrij geplaatst en gepland voor uitvoering op rekenknooppunten in die zijn gekoppeld aan taak Hallo Hallo-pool.</span><span class="sxs-lookup"><span data-stu-id="8433b-298">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="8433b-299">Batch verwerkt op basis van het Hallo-instellingen die u opgeeft, alle taak queuing, planning, opnieuw uit te voeren en andere taakbeheerverrichtingen voor u.</span><span class="sxs-lookup"><span data-stu-id="8433b-299">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="8433b-300">Er zijn veel manieren toomonitoring uitvoering van de taak.</span><span class="sxs-lookup"><span data-stu-id="8433b-300">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="8433b-301">DotNetTutorial toont een eenvoudig voorbeeld waarbij alleen wordt gerapporteerd bij voltooiing en wanneer de taak mislukt of slaagt.</span><span class="sxs-lookup"><span data-stu-id="8433b-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="8433b-302">Binnen Hallo `MonitorTasks` methode in het DotNetTutorial `Program.cs`, zijn er drie Batch .NET-concepten die discussies garanderen.</span><span class="sxs-lookup"><span data-stu-id="8433b-302">Within hello `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="8433b-303">Ze worden hieronder weergegeven in de volgorde waarin ze voorkomen:</span><span class="sxs-lookup"><span data-stu-id="8433b-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="8433b-304">**ODATADetailLevel**: [ODATADetailLevel][net_odatadetaillevel] opgeven in lijstbewerkingen (zoals het verkrijgen van een lijst met taken van een job) is essentieel om Batch-toepassingen goed te laten presteren.</span><span class="sxs-lookup"><span data-stu-id="8433b-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="8433b-305">Voeg [hello Azure Batch-service efficiënt Query](batch-efficient-list-queries.md) tooyour leeslijst als u van plan bent een of andere vorm van controle van de status binnen uw Batch-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8433b-305">Add [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md) tooyour reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="8433b-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] biedt Batch .NET-toepassingen met Help-hulpprogramma's voor het controleren van taakstatuswaarden.</span><span class="sxs-lookup"><span data-stu-id="8433b-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="8433b-307">In `MonitorTasks`, *DotNetTutorial* wacht tot alle taken tooreach [TaskState.Completed] [ net_taskstate] binnen een tijdslimiet.</span><span class="sxs-lookup"><span data-stu-id="8433b-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks tooreach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="8433b-308">Vervolgens wordt de taak Hallo beëindigd.</span><span class="sxs-lookup"><span data-stu-id="8433b-308">Then it terminates hello job.</span></span>
3. <span data-ttu-id="8433b-309">**TerminateJobAsync**: een taak met beëindigd [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (of Hallo blokkering JobOperations.TerminateJob) die taak wordt gemarkeerd als voltooid.</span><span class="sxs-lookup"><span data-stu-id="8433b-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or hello blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="8433b-310">Het is essentieel toodo dus als uw Batch-oplossing maakt gebruik van een [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="8433b-310">It is essential toodo so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="8433b-311">Dit is een speciaal type taak, dat wordt beschreven in [Job preparation and completion tasks](batch-job-prep-release.md) (Jobvoorbereidings- en jobvoltooiingstaken).</span><span class="sxs-lookup"><span data-stu-id="8433b-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="8433b-312">Hallo `MonitorTasks` methode van *DotNetTutorial*van `Program.cs` wordt hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="8433b-312">hello `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
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

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="8433b-313">Stap 7: taakuitvoer downloaden</span><span class="sxs-lookup"><span data-stu-id="8433b-313">Step 7: Download task output</span></span>
<span data-ttu-id="8433b-314">![Taakuitvoer downloaden uit Storage][7]</span><span class="sxs-lookup"><span data-stu-id="8433b-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="8433b-315">Nu dat hello taak is voltooid, kan Hallo-uitvoer van Hallo taken worden gedownload uit Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8433b-315">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="8433b-316">Hierbij wordt een aanroep te`DownloadBlobsFromContainerAsync` in *DotNetTutorial*van `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="8433b-316">This is done with a call too`DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="8433b-317">Hallo aanroep te`DownloadBlobsFromContainerAsync` in Hallo *DotNetTutorial* toepassing geeft aan dat Hallo-bestanden gedownloade tooyour moeten `%TEMP%` map.</span><span class="sxs-lookup"><span data-stu-id="8433b-317">hello call too`DownloadBlobsFromContainerAsync` in hello *DotNetTutorial* application specifies that hello files should be downloaded tooyour `%TEMP%` folder.</span></span> <span data-ttu-id="8433b-318">Gratis toomodify van mening bent dat dit locatie uitvoer.</span><span class="sxs-lookup"><span data-stu-id="8433b-318">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="8433b-319">Stap 8: containers verwijderen</span><span class="sxs-lookup"><span data-stu-id="8433b-319">Step 8: Delete containers</span></span>
<span data-ttu-id="8433b-320">Omdat u in rekening voor gegevens die zich in Azure Storage bevindt gebracht, maar het is altijd een goed idee tooremove blobs die niet langer nodig zijn voor uw Batch-taken.</span><span class="sxs-lookup"><span data-stu-id="8433b-320">Because you are charged for data that resides in Azure Storage, it's always a good idea tooremove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="8433b-321">In het DotNetTutorial `Program.cs`, dit wordt gedaan met drie aanroepen toohello Help-methode `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="8433b-321">In DotNetTutorial's `Program.cs`, this is done with three calls toohello helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="8433b-322">Hallo-methode zelf krijgt alleen een verwijzing toohello-container en roept vervolgens [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="8433b-322">hello method itself merely obtains a reference toohello container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

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

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="8433b-323">Stap 9: Hallo job en Hallo pool verwijderen</span><span class="sxs-lookup"><span data-stu-id="8433b-323">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="8433b-324">In de laatste stap hello bent u na vragen aan gebruiker toodelete Hallo taak en Hallo van toepassingen die zijn gemaakt door de DotNetTutorial-toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="8433b-324">In hello final step, you're prompted toodelete hello job and hello pool that were created by hello DotNetTutorial application.</span></span> <span data-ttu-id="8433b-325">Hoewel jobs en taken zelf niet in rekening worden gebracht, worden rekenknooppunten *wel* in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="8433b-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="8433b-326">Daarom is het raadzaam om knooppunten alleen toe te wijzen als dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="8433b-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="8433b-327">Het verwijderen van ongebruikte pools kan een onderdeel zijn van uw onderhoudsprocedure.</span><span class="sxs-lookup"><span data-stu-id="8433b-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="8433b-328">Hallo BatchClient van [JobOperations] [ net_joboperations] en [PoolOperations] [ net_pooloperations] hebben beide overeenkomstige verwijderingsmethoden, die worden aangeroepen wanneer Hallo gebruiker de verwijdering bevestigt:</span><span class="sxs-lookup"><span data-stu-id="8433b-328">hello BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if hello user confirms deletion:</span></span>

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
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
> <span data-ttu-id="8433b-329">Houd er rekening mee dat rekenresources in rekening worden gebracht. Door ongebruikte pools te verwijderen, beperkt u uw kosten tot een minimum.</span><span class="sxs-lookup"><span data-stu-id="8433b-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="8433b-330">Let op dat een pool verwijdert alle rekenknooppunten in die groep en dat alle gegevens op Hallo knooppunten kunnen niet worden teruggezet nadat het Hallo-pool wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8433b-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-dotnettutorial-sample"></a><span data-ttu-id="8433b-331">Voer Hallo *DotNetTutorial* voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8433b-331">Run hello *DotNetTutorial* sample</span></span>
<span data-ttu-id="8433b-332">Wanneer u de voorbeeldtoepassing Hallo uitvoert, worden Hallo console-uitvoer vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="8433b-332">When you run hello sample application, hello console output will be similar toohello following.</span></span> <span data-ttu-id="8433b-333">Tijdens het uitvoeren, wordt er op een pauze `Awaiting task completion, timeout in 00:30:00...` terwijl de rekenknooppunten van Hallo pool worden gestart.</span><span class="sxs-lookup"><span data-stu-id="8433b-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while hello pool's compute nodes are started.</span></span> <span data-ttu-id="8433b-334">Gebruik Hallo [Azure-portal] [ azure_portal] toomonitor uw pool, rekenknooppunten, job en taken tijdens en na de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="8433b-334">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="8433b-335">Gebruik Hallo [Azure-portal] [ azure_portal] of Hallo [Azure Opslagverkenner] [ storage_explorers] tooview Hallo Storage-resources (containers en blobs) die zijn gemaakt door de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="8433b-335">Use hello [Azure portal][azure_portal] or hello [Azure Storage Explorer][storage_explorers] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

<span data-ttu-id="8433b-336">Uitvoeringstijd doorgaans **ongeveer 5 minuten** wanneer u Hallo toepassing uitvoert in de standaardconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="8433b-336">Typical execution time is **approximately 5 minutes** when you run hello application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="8433b-337">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8433b-337">Next steps</span></span>
<span data-ttu-id="8433b-338">Gratis toomake wijzigingen te denken*DotNetTutorial* en *TaskApplication* tooexperiment met andere compute-scenario's.</span><span class="sxs-lookup"><span data-stu-id="8433b-338">Feel free toomake changes too*DotNetTutorial* and *TaskApplication* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="8433b-339">Probeer bijvoorbeeld een uitvoeringsvertraging te toevoegen*TaskApplication*, bijvoorbeeld net als bij [Thread.Sleep][net_thread_sleep], toosimulate langlopende taken en deze in de portal Hallo controleren.</span><span class="sxs-lookup"><span data-stu-id="8433b-339">For example, try adding an execution delay too*TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="8433b-340">Probeer meer taken toe te voegen of Hallo aantal rekenknooppunten aan te passen.</span><span class="sxs-lookup"><span data-stu-id="8433b-340">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="8433b-341">Voeg logica toocheck voor en Hallo gebruik van een bestaande groep toospeed uitvoeringstijd toestaan (*hint*: Bekijk `ArticleHelpers.cs` in Hallo [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] project in [azure-batch-samples][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="8433b-341">Add logic toocheck for and allow hello use of an existing pool toospeed execution time (*hint*: check out `ArticleHelpers.cs` in hello [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="8433b-342">Nu u bekend bent met de basiswerkstroom Hallo van een Batch-oplossing, is het tijd toodig in toohello aanvullende functies van Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="8433b-342">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="8433b-343">Bekijk Hallo [overzicht van Azure Batch-functies](batch-api-basics.md) artikel, waarin het is raadzaam als je nieuwe toohello-service.</span><span class="sxs-lookup"><span data-stu-id="8433b-343">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="8433b-344">Start op de andere artikelen Batch-ontwikkeling onder Hallo **Development in-depth** in Hallo [Batch-leertraject][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="8433b-344">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="8433b-345">Bekijk een andere implementatie van de verwerking van de workload Hallo 'eerste N woorden' met behulp van Batch in Hallo [TopNWords] [ github_topnwords] voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8433b-345">Check out a different implementation of processing hello "top N words" workload by using Batch in hello [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="8433b-346">Bekijk Hallo Batch .NET [release-opmerkingen](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) voor de meest recente wijzigingen in de bibliotheek Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8433b-346">Review hello Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for hello latest changes in hello library.</span></span>

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
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Het uploaden van taak toepassing en invoer (gegevens) bestanden toocontainers"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Batch-pool maken"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Batch-job maken"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Taken toojob toevoegen"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Taken controleren"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Taakuitvoer downloaden uit Storage"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Werkstroom van de Batch-oplossing (volledige diagram)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Batch-referenties in Portal"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Storage-referenties in Portal"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Werkstroom van de Batch-oplossing (minimaal diagram)"
