---
title: aaaUse .NET SDK voor Microsoft Azure StorSimple Data Manager-taken | Microsoft Docs
description: Meer informatie over hoe toouse .NET SDK toolaunch StorSimple Data Manager taken (afgeschermd voorbeeld)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b07fe64369574c994fd28d42786aa02dca435ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a><span data-ttu-id="1d30d-103">Gebruik de .net SDK Hallo tooinitiate gegevenstransformatie (afgeschermd voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="1d30d-103">Use hello .Net SDK tooinitiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="1d30d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1d30d-104">Overview</span></span>

<span data-ttu-id="1d30d-105">Dit artikel wordt uitgelegd hoe u Hallo functie voor transformatie van gegevens binnen Hallo StorSimple Data Manager service tootransform gegevens van de StorSimple-apparaat kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1d30d-105">This article explains how you can use hello data transformation feature within hello StorSimple Data Manager service tootransform StorSimple device data.</span></span> <span data-ttu-id="1d30d-106">Hallo wordt getransformeerde gegevens vervolgens geconsumeerd door andere Azure-services in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="1d30d-106">hello transformed data is then consumed by other Azure services in hello cloud.</span></span> <span data-ttu-id="1d30d-107">Hallo artikel heeft ook een overzicht toohelp een tooinitiate voorbeeld .NET-console-toepassing een transformatie-taak maken en te volgen voor de voltooiing.</span><span class="sxs-lookup"><span data-stu-id="1d30d-107">hello article also has a walkthrough toohelp create a sample .NET console application tooinitiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d30d-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1d30d-108">Prerequisites</span></span>

<span data-ttu-id="1d30d-109">Zorg ervoor dat u hebt voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="1d30d-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="1d30d-110">Een systeem met Visual Studio 2012, 2013 of 2015 2017 geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1d30d-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="1d30d-111">Azure Powershell is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1d30d-111">Azure Powershell installed.</span></span> <span data-ttu-id="1d30d-112">[Download de Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="1d30d-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="1d30d-113">Configuratie-instellingen tooinitialize Hallo gegevenstransformatie taak (instructies tooobtain deze instellingen zijn opgenomen hier).</span><span class="sxs-lookup"><span data-stu-id="1d30d-113">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="1d30d-114">De taakdefinitie van een die correct is geconfigureerd in een hybride Gegevensresource binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1d30d-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="1d30d-115">Alle Hallo vereist dll-bestanden.</span><span class="sxs-lookup"><span data-stu-id="1d30d-115">All hello required dlls.</span></span> <span data-ttu-id="1d30d-116">Deze DLL-bestanden downloaden van Hallo [GitHub-opslagplaats](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="1d30d-116">Download these dlls from hello [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="1d30d-117">`Get-ConfigurationParams.ps1`[script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) van Hallo github-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1d30d-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="1d30d-118">Stapsgewijs</span><span class="sxs-lookup"><span data-stu-id="1d30d-118">Step-by-step</span></span>

<span data-ttu-id="1d30d-119">Hallo te volgen stappen toouse .NET toolaunch een transformatie-taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1d30d-119">Perform hello following steps toouse .NET toolaunch a data transformation job.</span></span>

1. <span data-ttu-id="1d30d-120">tooretrieve hello configuratieparameters, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="1d30d-120">tooretrieve hello configuration parameters, do hello following steps:</span></span>
    1. <span data-ttu-id="1d30d-121">Hallo downloaden `Get-ConfigurationParams.ps1` van Hallo github-opslagplaats script in `C:\DataTransformation` locatie.</span><span class="sxs-lookup"><span data-stu-id="1d30d-121">Download hello `Get-ConfigurationParams.ps1` from hello github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="1d30d-122">Voer Hallo `Get-ConfigurationParams.ps1` script vanaf Hallo github-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1d30d-122">Run hello `Get-ConfigurationParams.ps1` script from hello github repository.</span></span> <span data-ttu-id="1d30d-123">Type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="1d30d-123">Type hello following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="1d30d-124">U kunt geen waarden voor Hallo doorgeven ActiveDirectoryKey en AppName.</span><span class="sxs-lookup"><span data-stu-id="1d30d-124">You can pass in any values for hello ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="1d30d-125">Dit script levert Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="1d30d-125">This script outputs hello following values:</span></span>
    * <span data-ttu-id="1d30d-126">Client-ID</span><span class="sxs-lookup"><span data-stu-id="1d30d-126">Client ID</span></span>
    * <span data-ttu-id="1d30d-127">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="1d30d-127">Tenant ID</span></span>
    * <span data-ttu-id="1d30d-128">Active Directory-sleutel (hetzelfde als Hallo een dat hierboven is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="1d30d-128">Active Directory key (same as hello one entered above)</span></span>
    * <span data-ttu-id="1d30d-129">Abonnements-id</span><span class="sxs-lookup"><span data-stu-id="1d30d-129">Subscription ID</span></span>

3. <span data-ttu-id="1d30d-130">Met behulp van Visual Studio 2012, 2013 of 2015, en maak een C# .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="1d30d-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="1d30d-131">Start **Visual Studio 2012-2013-2015**.</span><span class="sxs-lookup"><span data-stu-id="1d30d-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="1d30d-132">Klik op **bestand**, wijst u te**nieuw**, en klik op **Project**.</span><span class="sxs-lookup"><span data-stu-id="1d30d-132">Click **File**, point too**New**, and click **Project**.</span></span>
    2. <span data-ttu-id="1d30d-133">Vouw **Templates** uit en selecteer **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="1d30d-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="1d30d-134">Selecteer **consoletoepassing** uit de lijst Hallo van projecttypen op Hallo rechts.</span><span class="sxs-lookup"><span data-stu-id="1d30d-134">Select **Console Application** from hello list of project types on hello right.</span></span>
    4. <span data-ttu-id="1d30d-135">Voer **DataTransformationApp** voor Hallo **naam**.</span><span class="sxs-lookup"><span data-stu-id="1d30d-135">Enter **DataTransformationApp** for hello **Name**.</span></span>
    5. <span data-ttu-id="1d30d-136">Selecteer **C:\DataTransformation** voor Hallo **locatie**.</span><span class="sxs-lookup"><span data-stu-id="1d30d-136">Select **C:\DataTransformation** for hello **Location**.</span></span>
    6. <span data-ttu-id="1d30d-137">Klik op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="1d30d-137">Click **OK** toocreate hello project.</span></span>

4.  <span data-ttu-id="1d30d-138">Voeg nu alle dll's aanwezig zijn in Hallo [dll's](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) map als **verwijzingen** in Hallo-project dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1d30d-138">Now, add all DLLs present in hello [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in hello project that you created.</span></span> <span data-ttu-id="1d30d-139">toodownload hello dll-bestanden, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="1d30d-139">toodownload hello dll files, do hello following:</span></span>

    1. <span data-ttu-id="1d30d-140">In Visual Studio, ga te**weergave > Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="1d30d-140">In Visual Studio, go too**View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="1d30d-141">Klik op Hallo pijl toohello links van Data Transformation App-project.</span><span class="sxs-lookup"><span data-stu-id="1d30d-141">Click hello arrow toohello left of Data Transformation App project.</span></span> <span data-ttu-id="1d30d-142">Klik op **verwijzingen** en klik vervolgens met de rechtermuisknop te**verwijzing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1d30d-142">Click **References** and then right-click too**Add Reference**.</span></span>
    2. <span data-ttu-id="1d30d-143">Bladeren naar toohello locatie van de map voor hello-pakketten, alle Hallo dll selecteren en op **toevoegen**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d30d-143">Browse toohello location of hello packages folder, select all hello DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="1d30d-144">Voeg de volgende Hallo **met** instructies toohello bronbestand (Program.cs) in het Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="1d30d-144">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="1d30d-145">Hallo na code initialiseert Hallo data transformation taakexemplaar.</span><span class="sxs-lookup"><span data-stu-id="1d30d-145">hello following code initializes hello data transformation job instance.</span></span> <span data-ttu-id="1d30d-146">Voeg deze toe in Hallo **Main-methode**.</span><span class="sxs-lookup"><span data-stu-id="1d30d-146">Add this in hello **Main method**.</span></span> <span data-ttu-id="1d30d-147">Vervang de waarden Hallo configuratieparameters als u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="1d30d-147">Replace hello values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="1d30d-148">Hallo-waarden van invoegtoepassing **Resourcegroepnaam** en **hybride gegevens resourcenaam**.</span><span class="sxs-lookup"><span data-stu-id="1d30d-148">Plug in hello values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="1d30d-149">Hallo **Resourcegroepnaam** Hallo is een die als host fungeert voor Hallo hybride Gegevensresource op welke Hallo taakdefinitie is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1d30d-149">hello **Resource Group Name** is hello one that hosts hello Hybrid Data Resource on which hello job definition was configured.</span></span>

    ```
    // Setup hello configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize hello Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="1d30d-150">Geef Hallo parameters met welke Hallo taakdefinitie toobe moet worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="1d30d-150">Specify hello parameters with which hello job definition needs toobe run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="1d30d-151">(OR)</span><span class="sxs-lookup"><span data-stu-id="1d30d-151">(OR)</span></span>

    <span data-ttu-id="1d30d-152">Als u toochange Hallo taakparameters definitie tijdens runtime wilt, voegt u Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="1d30d-152">If you want toochange hello job definition parameters during run time, then add hello following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of hello volume on hello StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require hello latest existing backup toobe picked else use TakeNow tootrigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of hello StorSimple device.
        DeviceName = "device-name",
        // Name of hello container in Azure storage where hello files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) toobe applied on files under hello root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of hello volume on StorSimple device on which hello relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="1d30d-153">Toevoegen na de initialisatie van Hallo Hallo code tootrigger een transformatie-taak op Hallo taakdefinitie te volgen.</span><span class="sxs-lookup"><span data-stu-id="1d30d-153">After hello initialization, add hello following code tootrigger a data transformation job on hello job definition.</span></span> <span data-ttu-id="1d30d-154">Plug-in de juiste Hallo **definitie taaknaam**.</span><span class="sxs-lookup"><span data-stu-id="1d30d-154">Plug in hello appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="1d30d-155">Deze taak bestandsuploads Hallo-komt overeen met bestanden aanwezig zijn onder de hoofdmap Hallo op Hallo StorSimple volume toohello opgegeven container.</span><span class="sxs-lookup"><span data-stu-id="1d30d-155">This job uploads hello matched files present under hello root directory on hello StorSimple volume toohello specified container.</span></span> <span data-ttu-id="1d30d-156">Wanneer een bestand is geüpload, een bericht is verwijderd in de wachtrij hello (in Hallo hetzelfde opslagaccount als Hallo container) Hello dezelfde naam als de taakdefinitie Hallo.</span><span class="sxs-lookup"><span data-stu-id="1d30d-156">When a file is uploaded, a message is dropped in hello queue (in hello same storage account as hello container) with hello same name as hello job definition.</span></span> <span data-ttu-id="1d30d-157">Dit bericht kan worden gebruikt als een trigger tooinitiate verdere verwerking van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="1d30d-157">This message can be used as a trigger tooinitiate any further processing of hello file.</span></span>

10. <span data-ttu-id="1d30d-158">Zodra het Hallo-taak is geactiveerd, toevoegen Hallo code tootrack Hallo taak voor voltooiing te volgen.</span><span class="sxs-lookup"><span data-stu-id="1d30d-158">Once hello job has been triggered, add hello following code tootrack hello job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll hello job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for hello status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of hello job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // toohold hello console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="1d30d-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1d30d-159">Next steps</span></span>

<span data-ttu-id="1d30d-160">[Uw gegevens StorSimple Data Manager UI tootransform gebruiken](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="1d30d-160">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
