---
title: aaaUse Azure Automation tootrigger een taak | Microsoft Docs
description: Meer informatie over hoe Azure Automation toouse voor activering van StorSimple Data Manager-taken (afgeschermd voorbeeld)
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
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a><span data-ttu-id="331df-103">Gebruik Azure Automation tootrigger een taak (afgeschermd voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="331df-103">Use Azure Automation tootrigger a job (Private Preview)</span></span>

<span data-ttu-id="331df-104">Dit artikel wordt beschreven hoe toouse Azure Automation tootrigger een taak StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="331df-104">This articles describes how toouse Azure Automation tootrigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="331df-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="331df-105">Prerequisites</span></span>

<span data-ttu-id="331df-106">Zorg ervoor dat u hebt voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="331df-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="331df-107">Azure Powershell is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="331df-107">Azure Powershell installed.</span></span> <span data-ttu-id="331df-108">[Download de Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="331df-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="331df-109">Configuratie-instellingen tooinitialize Hallo gegevenstransformatie taak (instructies tooobtain deze instellingen zijn opgenomen hier).</span><span class="sxs-lookup"><span data-stu-id="331df-109">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="331df-110">De taakdefinitie van een die correct is geconfigureerd in een hybride Gegevensresource binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="331df-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="331df-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) bestand van Hallo github-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="331df-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from hello github repository.</span></span>
*   <span data-ttu-id="331df-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) van Hallo github-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="331df-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from hello github repository.</span></span>
*   <span data-ttu-id="331df-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) van Hallo github-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="331df-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="331df-114">Stapsgewijs</span><span class="sxs-lookup"><span data-stu-id="331df-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a><span data-ttu-id="331df-115">Azure Active Directory-machtigingen voor de taakdefinitie Hallo automation-taak toorun Hallo ophalen</span><span class="sxs-lookup"><span data-stu-id="331df-115">Get Azure Active Directory permissions for hello automation job toorun hello job definition</span></span>

1. <span data-ttu-id="331df-116">tooretrieve Hallo-configuratieparameters voor Active Directory, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="331df-116">tooretrieve hello configuration parameters for Active Directory, do hello following steps:</span></span>

    1. <span data-ttu-id="331df-117">Open Windows PowerShell in uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="331df-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="331df-118">Zorg ervoor dat [Azure PowerShell](https://azure.microsoft.com/downloads/) is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="331df-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="331df-119">Voer Hallo `Get-ConfigurationParams.ps1` script (in de map Hallo hierboven gedownloade).</span><span class="sxs-lookup"><span data-stu-id="331df-119">Run hello `Get-ConfigurationParams.ps1` script (in hello folder you downloaded above).</span></span> <span data-ttu-id="331df-120">Typ de volgende opdracht in de PowerShell-venster Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="331df-120">Type hello following command in hello PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="331df-121">Hallo ActiveDirectoryKey is een wachtwoord dat u later gebruiken.</span><span class="sxs-lookup"><span data-stu-id="331df-121">hello ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="331df-122">Voer een wachtwoord van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="331df-122">Enter a password of your choice.</span></span> <span data-ttu-id="331df-123">AppName kan een willekeurige tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="331df-123">AppName can be any string.</span></span>

2. <span data-ttu-id="331df-124">Dit script levert de volgende waarden op die moeten worden gebruikt tijdens de activering van automation-runbook Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="331df-124">This script outputs hello following values that should be used while triggering hello automation runbook.</span></span> <span data-ttu-id="331df-125">Noteer deze waarden.</span><span class="sxs-lookup"><span data-stu-id="331df-125">Make a note of these values.</span></span>

    - <span data-ttu-id="331df-126">Client-ID</span><span class="sxs-lookup"><span data-stu-id="331df-126">Client ID</span></span>
    - <span data-ttu-id="331df-127">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="331df-127">Tenant ID</span></span>
    - <span data-ttu-id="331df-128">Active Directory-sleutel (hetzelfde als Hallo een dat hierboven is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="331df-128">Active Directory key (same as hello one entered above)</span></span>
    - <span data-ttu-id="331df-129">Abonnements-id</span><span class="sxs-lookup"><span data-stu-id="331df-129">Subscription ID</span></span>

### <a name="set-up-hello-automation-account"></a><span data-ttu-id="331df-130">Hallo Automation-Account instellen</span><span class="sxs-lookup"><span data-stu-id="331df-130">Set up hello Automation Account</span></span>

1. <span data-ttu-id="331df-131">Meld u aan tooAzure en open uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="331df-131">Log on tooAzure and open your Automation account.</span></span>
2. <span data-ttu-id="331df-132">Klik op **activa** tegel tooopen Hallo lijst van activa.</span><span class="sxs-lookup"><span data-stu-id="331df-132">Click **Assets** tile tooopen hello list of assets.</span></span>
3. <span data-ttu-id="331df-133">Klik op **Modules** tegel tooopen Hallo lijst met modules.</span><span class="sxs-lookup"><span data-stu-id="331df-133">Click **Modules** tile tooopen hello list of modules.</span></span>
4. <span data-ttu-id="331df-134">Klik op **+ toevoegen van een module** knop en Hallo toevoegen module blade wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="331df-134">Click **+ Add a module** button and hello Add module blade is launched.</span></span>

    ![Instellingen voor Automation-account](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="331df-136">Nadat u hebt geselecteerd Hallo `DataTransformationApp.zip` bestand vanaf uw lokale computer, klikt u op **OK** tooimport Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="331df-136">After you have selected hello `DataTransformationApp.zip` file from your local computer, click **OK** tooimport hello module.</span></span>

   <span data-ttu-id="331df-137">Als een module tooyour-account voor Azure Automation wordt geïmporteerd, pakt deze metagegevens over Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="331df-137">When Azure Automation imports a module tooyour account, it extracts metadata about hello module.</span></span> <span data-ttu-id="331df-138">Deze bewerking kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="331df-138">This operation may take a couple of minutes.</span></span>

   ![Instellingen voor Automation-account](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="331df-140">U ontvangt een melding die module hello wordt geïmplementeerd en een andere melding wanneer het Hallo-proces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="331df-140">You receive a notification that hello module is being deployed and another notification when hello process is complete.</span></span>  <span data-ttu-id="331df-141">U kunt ook Hallo status controleren **Modules** tegel.</span><span class="sxs-lookup"><span data-stu-id="331df-141">You can also check hello status in **Modules** tile.</span></span>

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a><span data-ttu-id="331df-142">tooimport hello runbook waarmee de taakdefinitie hello wordt geactiveerd</span><span class="sxs-lookup"><span data-stu-id="331df-142">tooimport hello runbook that triggers hello job definition</span></span>

1. <span data-ttu-id="331df-143">Open uw Automation-account in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="331df-143">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="331df-144">Klik op **Runbooks** tegel tooopen Hallo lijst van runbooks.</span><span class="sxs-lookup"><span data-stu-id="331df-144">Click **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="331df-145">Klik op **+ een runbook toevoegen** en vervolgens **een bestaand runbook importeren**.</span><span class="sxs-lookup"><span data-stu-id="331df-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Een bestaand runbook importeren](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="331df-147">Klik op **Runbook bestand** en selecteer Hallo bestand tooimport `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="331df-147">Click **Runbook file** and select hello file tooimport `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="331df-148">Klik op **maken** tooimport hello runbook.</span><span class="sxs-lookup"><span data-stu-id="331df-148">Click **Create** tooimport hello runbook.</span></span> <span data-ttu-id="331df-149">Hallo nieuw runbook wordt weergegeven in de lijst Hallo van runbooks voor Hallo Automation-account.</span><span class="sxs-lookup"><span data-stu-id="331df-149">hello new runbook appears in hello list of runbooks for hello Automation account.</span></span>
7. <span data-ttu-id="331df-150">Klik op **Trigger-DataTransformation-Job** runbook en klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="331df-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="331df-151">Klik op **publiceren** en vervolgens **Ja** wanneer u om bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="331df-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="toorun-hello-runbook"></a><span data-ttu-id="331df-152">toorun hello runbook:</span><span class="sxs-lookup"><span data-stu-id="331df-152">toorun hello runbook:</span></span>
1. <span data-ttu-id="331df-153">Open uw Automation-account in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="331df-153">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="331df-154">Klik op Hallo **Runbooks** tegel tooopen Hallo lijst van runbooks.</span><span class="sxs-lookup"><span data-stu-id="331df-154">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="331df-155">Klik op **Trigger-DataTransformation-Job**.</span><span class="sxs-lookup"><span data-stu-id="331df-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="331df-156">Klik op **Start** toostart hello runbook.</span><span class="sxs-lookup"><span data-stu-id="331df-156">Click **Start** toostart hello runbook.</span></span>

   ![Runbook starten](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="331df-158">In Hallo **runbook starten** blade alle Hallo parameters opgeven.</span><span class="sxs-lookup"><span data-stu-id="331df-158">In hello **Start runbook** blade, enter all hello parameters.</span></span> <span data-ttu-id="331df-159">Klik op **OK** toosubmit Hallo gegevenstransformatie taak.</span><span class="sxs-lookup"><span data-stu-id="331df-159">Click **OK** toosubmit hello Data Transformation job.</span></span>

   ![Runbook starten](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="331df-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="331df-161">Next steps</span></span>

<span data-ttu-id="331df-162">[Uw gegevens StorSimple Data Manager UI tootransform gebruiken](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="331df-162">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
