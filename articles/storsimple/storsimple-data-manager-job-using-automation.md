---
title: Gebruik Azure Automation om een taak te activeren | Microsoft Docs
description: Informatie over het gebruik van Azure Automation voor activering van StorSimple Data Manager-taken (afgeschermd voorbeeld)
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
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 9691408bcd80afb6eba534f26749b76dd3bfe315
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-automation-to-trigger-a-job-private-preview"></a><span data-ttu-id="3edb4-103">Gebruik Azure Automation voor het activeren van een taak (afgeschermd voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="3edb4-103">Use Azure Automation to trigger a job (Private Preview)</span></span>

<span data-ttu-id="3edb4-104">Dit artikel wordt beschreven hoe u Azure Automation gebruikt om een StorSimple Data Manager-taak te activeren.</span><span class="sxs-lookup"><span data-stu-id="3edb4-104">This articles describes how to use Azure Automation to trigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3edb4-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3edb4-105">Prerequisites</span></span>

<span data-ttu-id="3edb4-106">Zorg ervoor dat u hebt voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="3edb4-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="3edb4-107">Azure Powershell is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3edb4-107">Azure Powershell installed.</span></span> <span data-ttu-id="3edb4-108">[Download de Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="3edb4-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="3edb4-109">Configuratie-instellingen voor het initialiseren van de taak gegevenstransformatie (instructies voor het verkrijgen van deze instellingen zijn opgenomen hier).</span><span class="sxs-lookup"><span data-stu-id="3edb4-109">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="3edb4-110">De taakdefinitie van een die correct is geconfigureerd in een hybride Gegevensresource binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3edb4-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="3edb4-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) bestand van de github-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="3edb4-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from the github repository.</span></span>
*   <span data-ttu-id="3edb4-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) uit de github-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="3edb4-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from the github repository.</span></span>
*   <span data-ttu-id="3edb4-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) uit de github-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="3edb4-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="3edb4-114">Stapsgewijs</span><span class="sxs-lookup"><span data-stu-id="3edb4-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-the-automation-job-to-run-the-job-definition"></a><span data-ttu-id="3edb4-115">Azure Active Directory-machtigingen voor het uitvoeren van de taakdefinitie automation-taak ophalen</span><span class="sxs-lookup"><span data-stu-id="3edb4-115">Get Azure Active Directory permissions for the automation job to run the job definition</span></span>

1. <span data-ttu-id="3edb4-116">Voor het ophalen van de configuratieparameters voor Active Directory, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3edb4-116">To retrieve the configuration parameters for Active Directory, do the following steps:</span></span>

    1. <span data-ttu-id="3edb4-117">Open Windows PowerShell in uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="3edb4-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="3edb4-118">Zorg ervoor dat [Azure PowerShell](https://azure.microsoft.com/downloads/) is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3edb4-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="3edb4-119">Voer de `Get-ConfigurationParams.ps1` script (in de map die u hebt gedownload hierboven).</span><span class="sxs-lookup"><span data-stu-id="3edb4-119">Run the `Get-ConfigurationParams.ps1` script (in the folder you downloaded above).</span></span> <span data-ttu-id="3edb4-120">Typ de volgende opdracht in het venster PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3edb4-120">Type the following command in the PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="3edb4-121">De ActiveDirectoryKey is een wachtwoord dat u later gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3edb4-121">The ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="3edb4-122">Voer een wachtwoord van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="3edb4-122">Enter a password of your choice.</span></span> <span data-ttu-id="3edb4-123">AppName kan een willekeurige tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="3edb4-123">AppName can be any string.</span></span>

2. <span data-ttu-id="3edb4-124">Dit script levert de volgende waarden die moeten worden gebruikt tijdens de activering van de automation-runbook.</span><span class="sxs-lookup"><span data-stu-id="3edb4-124">This script outputs the following values that should be used while triggering the automation runbook.</span></span> <span data-ttu-id="3edb4-125">Noteer deze waarden.</span><span class="sxs-lookup"><span data-stu-id="3edb4-125">Make a note of these values.</span></span>

    - <span data-ttu-id="3edb4-126">Client-ID</span><span class="sxs-lookup"><span data-stu-id="3edb4-126">Client ID</span></span>
    - <span data-ttu-id="3edb4-127">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="3edb4-127">Tenant ID</span></span>
    - <span data-ttu-id="3edb4-128">Active Directory-sleutel (zelfde als een dat hierboven is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="3edb4-128">Active Directory key (same as the one entered above)</span></span>
    - <span data-ttu-id="3edb4-129">Abonnements-id</span><span class="sxs-lookup"><span data-stu-id="3edb4-129">Subscription ID</span></span>

### <a name="set-up-the-automation-account"></a><span data-ttu-id="3edb4-130">Het Automation-Account instellen</span><span class="sxs-lookup"><span data-stu-id="3edb4-130">Set up the Automation Account</span></span>

1. <span data-ttu-id="3edb4-131">Meld u aan bij Azure en open uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="3edb4-131">Log on to Azure and open your Automation account.</span></span>
2. <span data-ttu-id="3edb4-132">Klik op **activa** tegel om de lijst van assets te openen.</span><span class="sxs-lookup"><span data-stu-id="3edb4-132">Click **Assets** tile to open the list of assets.</span></span>
3. <span data-ttu-id="3edb4-133">Klik op **Modules** tegel te openen van de lijst met modules.</span><span class="sxs-lookup"><span data-stu-id="3edb4-133">Click **Modules** tile to open the list of modules.</span></span>
4. <span data-ttu-id="3edb4-134">Klik op **+ toevoegen van een module** knop en de blade van de module toevoegen wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="3edb4-134">Click **+ Add a module** button and the Add module blade is launched.</span></span>

    ![Instellingen voor Automation-account](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="3edb4-136">Nadat u hebt geselecteerd de `DataTransformationApp.zip` bestand vanaf uw lokale computer, klikt u op **OK** de module te importeren.</span><span class="sxs-lookup"><span data-stu-id="3edb4-136">After you have selected the `DataTransformationApp.zip` file from your local computer, click **OK** to import the module.</span></span>

   <span data-ttu-id="3edb4-137">Wanneer u een module Azure Automation importeert in uw account, pakt deze metagegevens over de module.</span><span class="sxs-lookup"><span data-stu-id="3edb4-137">When Azure Automation imports a module to your account, it extracts metadata about the module.</span></span> <span data-ttu-id="3edb4-138">Deze bewerking kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="3edb4-138">This operation may take a couple of minutes.</span></span>

   ![Instellingen voor Automation-account](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="3edb4-140">U ontvangt een melding dat de module wordt geïmplementeerd en nog een melding wanneer het proces voltooid is.</span><span class="sxs-lookup"><span data-stu-id="3edb4-140">You receive a notification that the module is being deployed and another notification when the process is complete.</span></span>  <span data-ttu-id="3edb4-141">U kunt ook de status controleren **Modules** tegel.</span><span class="sxs-lookup"><span data-stu-id="3edb4-141">You can also check the status in **Modules** tile.</span></span>

### <a name="to-import-the-runbook-that-triggers-the-job-definition"></a><span data-ttu-id="3edb4-142">Voor het importeren van het runbook waarmee de taakdefinitie wordt geactiveerd</span><span class="sxs-lookup"><span data-stu-id="3edb4-142">To import the runbook that triggers the job definition</span></span>

1. <span data-ttu-id="3edb4-143">Open uw Automation-account in Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3edb4-143">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="3edb4-144">Klik op **Runbooks** tegel om de lijst van runbooks te openen.</span><span class="sxs-lookup"><span data-stu-id="3edb4-144">Click **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="3edb4-145">Klik op **+ een runbook toevoegen** en vervolgens **een bestaand runbook importeren**.</span><span class="sxs-lookup"><span data-stu-id="3edb4-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Een bestaand runbook importeren](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="3edb4-147">Klik op **Runbook bestand** en selecteer de te importeren bestand `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="3edb4-147">Click **Runbook file** and select the file to import `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="3edb4-148">Klik op **maken** voor het importeren van het runbook.</span><span class="sxs-lookup"><span data-stu-id="3edb4-148">Click **Create** to import the runbook.</span></span> <span data-ttu-id="3edb4-149">Het nieuwe runbook wordt weergegeven in de lijst met runbooks voor het Automation-account.</span><span class="sxs-lookup"><span data-stu-id="3edb4-149">The new runbook appears in the list of runbooks for the Automation account.</span></span>
7. <span data-ttu-id="3edb4-150">Klik op **Trigger-DataTransformation-Job** runbook en klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="3edb4-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="3edb4-151">Klik op **publiceren** en vervolgens **Ja** wanneer u om bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="3edb4-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="to-run-the-runbook"></a><span data-ttu-id="3edb4-152">Het runbook uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3edb4-152">To run the runbook:</span></span>
1. <span data-ttu-id="3edb4-153">Open uw Automation-account in Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3edb4-153">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="3edb4-154">Klik op de tegel **Runbooks** om de lijst met runbooks te openen.</span><span class="sxs-lookup"><span data-stu-id="3edb4-154">Click the **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="3edb4-155">Klik op **Trigger-DataTransformation-Job**.</span><span class="sxs-lookup"><span data-stu-id="3edb4-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="3edb4-156">Klik op **Starten** om het runbook te starten.</span><span class="sxs-lookup"><span data-stu-id="3edb4-156">Click **Start** to start the runbook.</span></span>

   ![Runbook starten](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="3edb4-158">In de **runbook starten** blade alle parameters opgeven.</span><span class="sxs-lookup"><span data-stu-id="3edb4-158">In the **Start runbook** blade, enter all the parameters.</span></span> <span data-ttu-id="3edb4-159">Klik op **OK** de taak Gegevenstransformatie verzenden.</span><span class="sxs-lookup"><span data-stu-id="3edb4-159">Click **OK** to submit the Data Transformation job.</span></span>

   ![Runbook starten](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="3edb4-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3edb4-161">Next steps</span></span>

<span data-ttu-id="3edb4-162">[Gebruik StorSimple Data Manager UI om uw gegevens te transformeren](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="3edb4-162">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>