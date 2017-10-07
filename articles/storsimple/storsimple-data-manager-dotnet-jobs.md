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
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a>Gebruik de .net SDK Hallo tooinitiate gegevenstransformatie (afgeschermd voorbeeld)

## <a name="overview"></a>Overzicht

Dit artikel wordt uitgelegd hoe u Hallo functie voor transformatie van gegevens binnen Hallo StorSimple Data Manager service tootransform gegevens van de StorSimple-apparaat kunt gebruiken. Hallo wordt getransformeerde gegevens vervolgens geconsumeerd door andere Azure-services in de cloud Hallo. Hallo artikel heeft ook een overzicht toohelp een tooinitiate voorbeeld .NET-console-toepassing een transformatie-taak maken en te volgen voor de voltooiing.

## <a name="prerequisites"></a>Vereisten

Zorg ervoor dat u hebt voordat u begint:
*   Een systeem met Visual Studio 2012, 2013 of 2015 2017 geïnstalleerd.
*   Azure Powershell is geïnstalleerd. [Download de Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Configuratie-instellingen tooinitialize Hallo gegevenstransformatie taak (instructies tooobtain deze instellingen zijn opgenomen hier).
*   De taakdefinitie van een die correct is geconfigureerd in een hybride Gegevensresource binnen een resourcegroep.
*   Alle Hallo vereist dll-bestanden. Deze DLL-bestanden downloaden van Hallo [GitHub-opslagplaats](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).
*   `Get-ConfigurationParams.ps1`[script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) van Hallo github-opslagplaats.

## <a name="step-by-step"></a>Stapsgewijs

Hallo te volgen stappen toouse .NET toolaunch een transformatie-taak uitvoeren.

1. tooretrieve hello configuratieparameters, Hallo volgende stappen:
    1. Hallo downloaden `Get-ConfigurationParams.ps1` van Hallo github-opslagplaats script in `C:\DataTransformation` locatie.
    1. Voer Hallo `Get-ConfigurationParams.ps1` script vanaf Hallo github-opslagplaats. Type Hallo volgende opdracht:

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        U kunt geen waarden voor Hallo doorgeven ActiveDirectoryKey en AppName.


2. Dit script levert Hallo volgende waarden:
    * Client-ID
    * Tenant-id
    * Active Directory-sleutel (hetzelfde als Hallo een dat hierboven is opgegeven)
    * Abonnements-id

3. Met behulp van Visual Studio 2012, 2013 of 2015, en maak een C# .NET-consoletoepassing.

    1. Start **Visual Studio 2012-2013-2015**.
    1. Klik op **bestand**, wijst u te**nieuw**, en klik op **Project**.
    2. Vouw **Templates** uit en selecteer **Visual C#**.
    3. Selecteer **consoletoepassing** uit de lijst Hallo van projecttypen op Hallo rechts.
    4. Voer **DataTransformationApp** voor Hallo **naam**.
    5. Selecteer **C:\DataTransformation** voor Hallo **locatie**.
    6. Klik op **OK** toocreate Hallo project.

4.  Voeg nu alle dll's aanwezig zijn in Hallo [dll's](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) map als **verwijzingen** in Hallo-project dat u hebt gemaakt. toodownload hello dll-bestanden, Hallo te volgen:

    1. In Visual Studio, ga te**weergave > Solution Explorer**.
    1. Klik op Hallo pijl toohello links van Data Transformation App-project. Klik op **verwijzingen** en klik vervolgens met de rechtermuisknop te**verwijzing toevoegen**.
    2. Bladeren naar toohello locatie van de map voor hello-pakketten, alle Hallo dll selecteren en op **toevoegen**, en klik vervolgens op **OK**.

5. Voeg de volgende Hallo **met** instructies toohello bronbestand (Program.cs) in het Hallo-project.

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. Hallo na code initialiseert Hallo data transformation taakexemplaar. Voeg deze toe in Hallo **Main-methode**. Vervang de waarden Hallo configuratieparameters als u eerder hebt verkregen. Hallo-waarden van invoegtoepassing **Resourcegroepnaam** en **hybride gegevens resourcenaam**. Hallo **Resourcegroepnaam** Hallo is een die als host fungeert voor Hallo hybride Gegevensresource op welke Hallo taakdefinitie is geconfigureerd.

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

7. Geef Hallo parameters met welke Hallo taakdefinitie toobe moet worden uitgevoerd

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    (OR)

    Als u toochange Hallo taakparameters definitie tijdens runtime wilt, voegt u Hallo code te volgen:

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

8. Toevoegen na de initialisatie van Hallo Hallo code tootrigger een transformatie-taak op Hallo taakdefinitie te volgen. Plug-in de juiste Hallo **definitie taaknaam**.

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. Deze taak bestandsuploads Hallo-komt overeen met bestanden aanwezig zijn onder de hoofdmap Hallo op Hallo StorSimple volume toohello opgegeven container. Wanneer een bestand is geüpload, een bericht is verwijderd in de wachtrij hello (in Hallo hetzelfde opslagaccount als Hallo container) Hello dezelfde naam als de taakdefinitie Hallo. Dit bericht kan worden gebruikt als een trigger tooinitiate verdere verwerking van Hallo-bestand.

10. Zodra het Hallo-taak is geactiveerd, toevoegen Hallo code tootrack Hallo taak voor voltooiing te volgen.

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


## <a name="next-steps"></a>Volgende stappen

[Uw gegevens StorSimple Data Manager UI tootransform gebruiken](storsimple-data-manager-ui.md).
