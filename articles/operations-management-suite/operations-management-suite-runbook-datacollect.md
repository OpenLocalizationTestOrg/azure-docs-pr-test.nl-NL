---
title: aaaCollecting Log Analytics-gegevens met een runbook in Azure Automation | Microsoft Docs
description: Stapsgewijze zelfstudie die helpt bij het maken van een runbook in Azure Automation toocollect gegevens in Hallo OMS-opslagplaats voor analyse door logboekanalyse.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="49901-103">Gegevens verzamelen in logboekanalyse met een Azure Automation-runbook</span><span class="sxs-lookup"><span data-stu-id="49901-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="49901-104">U kunt een aanzienlijke hoeveelheid gegevens in logboekanalyse verzamelen uit diverse bronnen, zoals [gegevensbronnen](../log-analytics/log-analytics-data-sources.md) op agents en ook [gegevens verzameld van Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="49901-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="49901-105">Er zijn een scenario's waarbij u toocollect gegevens nodig hebt die niet worden geopend via deze standaard bronnen.</span><span class="sxs-lookup"><span data-stu-id="49901-105">There are a scenarios though where you need toocollect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="49901-106">In dergelijke gevallen kunt u Hallo [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) toowrite gegevens tooLog Analytics vanaf elke client REST-API.</span><span class="sxs-lookup"><span data-stu-id="49901-106">In these cases, you can use hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) toowrite data tooLog Analytics from any REST API client.</span></span>  <span data-ttu-id="49901-107">Een algemene methode tooperform deze gegevensverzameling is met behulp van een runbook in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="49901-107">A common method tooperform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="49901-108">Deze zelfstudie wordt begeleid Hallo-proces voor het maken en plannen van een runbook in Azure Automation toowrite gegevens tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="49901-108">This tutorial walks through hello process for creating and scheduling a runbook in Azure Automation toowrite data tooLog Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="49901-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="49901-109">Prerequisites</span></span>
<span data-ttu-id="49901-110">Dit scenario vereist Hallo resources die zijn geconfigureerd in uw Azure-abonnement te volgen.</span><span class="sxs-lookup"><span data-stu-id="49901-110">This scenario requires hello following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="49901-111">Beide mag een gratis account.</span><span class="sxs-lookup"><span data-stu-id="49901-111">Both can be a free account.</span></span>

- <span data-ttu-id="49901-112">[Meld u werkruimte](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="49901-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="49901-113">[Azure automation-account](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="49901-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="49901-114">Overzicht van scenario</span><span class="sxs-lookup"><span data-stu-id="49901-114">Overview of scenario</span></span>
<span data-ttu-id="49901-115">Voor deze zelfstudie schrijft u een runbook dat informatie over het automatiseren van taken verzamelt.</span><span class="sxs-lookup"><span data-stu-id="49901-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="49901-116">Azure Automation-Runbooks worden geïmplementeerd met PowerShell, zodat u beginnen door te schrijven en testen van een script in hello Azure Automation-editor.</span><span class="sxs-lookup"><span data-stu-id="49901-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in hello Azure Automation editor.</span></span>  <span data-ttu-id="49901-117">Zodra u hebt gecontroleerd dat u Hallo vereist informatie wilt verzamelen, moet u schrijven die gegevens tooLog Analytics en controleer of aangepaste Hallo-gegevenstype.</span><span class="sxs-lookup"><span data-stu-id="49901-117">Once you verify that you're collecting hello required information, you'll write that data tooLog Analytics and verify hello custom data type.</span></span>  <span data-ttu-id="49901-118">Ten slotte gaat u een planning toostart hello runbook maken met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="49901-118">Finally, you'll create a schedule toostart hello runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="49901-119">U kunt Azure Automation toosend taak informatie tooLog Analytics zonder dit runbook configureren.</span><span class="sxs-lookup"><span data-stu-id="49901-119">You can configure Azure Automation toosend job information tooLog Analytics without this runbook.</span></span>  <span data-ttu-id="49901-120">Dit scenario wordt voornamelijk gebruikt toosupport Hallo zelfstudie en het wordt aanbevolen dat u tooa Hallo-test gegevenswerkruimte verzenden.</span><span class="sxs-lookup"><span data-stu-id="49901-120">This scenario is primarily used toosupport hello tutorial, and it's recommended that you send hello data tooa test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="49901-121">1. Data Collector API-module installeren</span><span class="sxs-lookup"><span data-stu-id="49901-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="49901-122">Elke [aanvraag van HTTP-Data Collector API Hallo](../log-analytics/log-analytics-data-collector-api.md#create-a-request) moet op de juiste manier zijn geformatteerd en autorisatie-header bevatten.</span><span class="sxs-lookup"><span data-stu-id="49901-122">Every [request from hello HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="49901-123">U kunt dit doen in uw runbook, maar u kunt beperken Hallo code vereist met behulp van een module die vereenvoudigt u dit proces.</span><span class="sxs-lookup"><span data-stu-id="49901-123">You can do this in your runbook, but you can reduce hello amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="49901-124">Een module die u kunt gebruiken is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in PowerShell Gallery Hallo.</span><span class="sxs-lookup"><span data-stu-id="49901-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in hello PowerShell Gallery.</span></span>

<span data-ttu-id="49901-125">toouse een [module](../automation/automation-integration-modules.md) in een runbook moet worden geïnstalleerd in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="49901-125">toouse a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="49901-126">Elk runbook in hetzelfde account kunt Hallo Hallo functies in Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="49901-126">Any runbook in hello same account can then use hello functions in hello module.</span></span>  <span data-ttu-id="49901-127">U kunt een nieuwe module installeren door te selecteren **activa** > **Modules** > **toevoegen van een module** in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="49901-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="49901-128">Hallo PowerShell Gallery al beschikt u over een snelle optie toodeploy een module direct tooyour automation-account zodat u deze optie kunt gebruiken voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="49901-128">hello PowerShell Gallery though gives you a quick option toodeploy a module directly tooyour automation account so you can use that option for this tutorial.</span></span>  

![Module OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="49901-130">Ga te[PowerShell Gallery](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="49901-130">Go too[PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="49901-131">Zoeken naar **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="49901-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="49901-132">Klik op Hallo **tooAzure Automation implementeren** knop.</span><span class="sxs-lookup"><span data-stu-id="49901-132">Click on hello **Deploy tooAzure Automation** button.</span></span>
4. <span data-ttu-id="49901-133">Selecteer uw automation-account en klik op **OK** tooinstall Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="49901-133">Select your automation account and click **OK** tooinstall hello module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="49901-134">2. Automation-variabelen maken</span><span class="sxs-lookup"><span data-stu-id="49901-134">2. Create Automation variables</span></span>
<span data-ttu-id="49901-135">[Automation-variabelen](..\automation\automation-variables.md) bevatten waarden die kunnen worden gebruikt door alle runbooks in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="49901-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="49901-136">Zij runbooks meer flexibele doordat u toochange deze waarden zonder te bewerken Hallo werkelijke runbook.</span><span class="sxs-lookup"><span data-stu-id="49901-136">They make runbooks more flexible by allowing you toochange these values without editing hello actual runbook.</span></span> <span data-ttu-id="49901-137">Elke aanvraag van Hallo HTTP Data Collector API vereist Hallo-ID en sleutel van Hallo OMS-werkruimte en variabele assets zijn ideaal toostore deze informatie.</span><span class="sxs-lookup"><span data-stu-id="49901-137">Every request from hello HTTP Data Collector API requires hello ID and key of hello OMS workspace, and variable assets are ideal toostore this information.</span></span>  

![Variabelen](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="49901-139">Navigeer in hello Azure-portal, tooyour Automation-account.</span><span class="sxs-lookup"><span data-stu-id="49901-139">In hello Azure portal, navigate tooyour Automation account.</span></span>
2. <span data-ttu-id="49901-140">Selecteer **variabelen** onder **gedeelde Resources**.</span><span class="sxs-lookup"><span data-stu-id="49901-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="49901-141">Klik op **toevoegen van een variabele** en Hallo twee variabelen in de volgende tabel Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="49901-141">Click **Add a variable** and create hello two variables in hello following table.</span></span>

| <span data-ttu-id="49901-142">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="49901-142">Property</span></span> | <span data-ttu-id="49901-143">De waarde van de werkruimte-ID</span><span class="sxs-lookup"><span data-stu-id="49901-143">Workspace ID Value</span></span> | <span data-ttu-id="49901-144">De sleutelwaarde werkruimte</span><span class="sxs-lookup"><span data-stu-id="49901-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="49901-145">Naam</span><span class="sxs-lookup"><span data-stu-id="49901-145">Name</span></span> | <span data-ttu-id="49901-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="49901-146">WorkspaceId</span></span> | <span data-ttu-id="49901-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="49901-147">WorkspaceKey</span></span> |
| <span data-ttu-id="49901-148">Type</span><span class="sxs-lookup"><span data-stu-id="49901-148">Type</span></span> | <span data-ttu-id="49901-149">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="49901-149">String</span></span> | <span data-ttu-id="49901-150">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="49901-150">String</span></span> |
| <span data-ttu-id="49901-151">Waarde</span><span class="sxs-lookup"><span data-stu-id="49901-151">Value</span></span> | <span data-ttu-id="49901-152">In de werkruimte-ID van de werkruimte voor logboekanalyse hello te plakken.</span><span class="sxs-lookup"><span data-stu-id="49901-152">Paste in hello Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="49901-153">Plak met Hallo primaire of secundaire sleutel van de werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="49901-153">Paste in with hello Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="49901-154">Versleuteld</span><span class="sxs-lookup"><span data-stu-id="49901-154">Encrypted</span></span> | <span data-ttu-id="49901-155">Nee</span><span class="sxs-lookup"><span data-stu-id="49901-155">No</span></span> | <span data-ttu-id="49901-156">Ja</span><span class="sxs-lookup"><span data-stu-id="49901-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="49901-157">3. Runbook maken</span><span class="sxs-lookup"><span data-stu-id="49901-157">3. Create runbook</span></span>

<span data-ttu-id="49901-158">Azure Automation heeft een editor in Hallo-portal waar u kunt bewerken en test uw runbook.</span><span class="sxs-lookup"><span data-stu-id="49901-158">Azure Automation has an editor in hello portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="49901-159">U hebt Hallo optie toouse Hallo script editor toowork met [PowerShell rechtstreeks](../automation/automation-edit-textual-runbook.md) of [maken van een grafisch runbook](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="49901-159">You have hello option toouse hello script editor toowork with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="49901-160">Voor deze zelfstudie werkt u met een PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="49901-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Runbook bewerken](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="49901-162">Navigeer tooyour Automation-account.</span><span class="sxs-lookup"><span data-stu-id="49901-162">Navigate tooyour Automation account.</span></span>  
2. <span data-ttu-id="49901-163">Klik op **Runbooks** > **een runbook toevoegen** > **een nieuw runbook maken**.</span><span class="sxs-lookup"><span data-stu-id="49901-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="49901-164">Runbooknaam hello, typt u **verzamelen-Automation-taken**.</span><span class="sxs-lookup"><span data-stu-id="49901-164">For hello runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="49901-165">Selecteer Hallo runbooktype **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="49901-165">For hello runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="49901-166">Klik op **maken** toocreate hello runbook en start Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="49901-166">Click **Create** toocreate hello runbook and start hello editor.</span></span>
5. <span data-ttu-id="49901-167">Kopieer en plak de volgende code in runbook Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="49901-167">Copy and paste hello following code into hello runbook.</span></span>  <span data-ttu-id="49901-168">Raadpleeg toohello opmerkingen in Hallo script voor een uitleg van Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="49901-168">Refer toohello comments in hello script for explanation of hello code.</span></span>
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="49901-169">4. Runbook-test</span><span class="sxs-lookup"><span data-stu-id="49901-169">4. Test runbook</span></span>
<span data-ttu-id="49901-170">Azure Automation omvat een omgeving te[test uw runbook](../automation/automation-testing-runbook.md) voordat u deze hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="49901-170">Azure Automation includes an environment too[test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="49901-171">U kunt Hallo gegevens verzameld door Hallo runbook controleren en nagaan of dat deze tooLog Analytics schrijft zoals verwacht voordat het wordt gepubliceerd tooproduction.</span><span class="sxs-lookup"><span data-stu-id="49901-171">You can inspect hello data collected by hello runbook and verify that it writes tooLog Analytics as expected before publishing it tooproduction.</span></span> 
 
![Runbook-test](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="49901-173">Klik op **opslaan** toosave hello runbook.</span><span class="sxs-lookup"><span data-stu-id="49901-173">Click **Save** toosave hello runbook.</span></span>
1. <span data-ttu-id="49901-174">Klik op **testvenster** tooopen hello runbook in de testomgeving Hallo.</span><span class="sxs-lookup"><span data-stu-id="49901-174">Click **Test pane** tooopen hello runbook in hello test environment.</span></span>
3. <span data-ttu-id="49901-175">Nadat uw runbook parameters heeft, bent u waarden voor deze vraag tooenter.</span><span class="sxs-lookup"><span data-stu-id="49901-175">Since your runbook has parameters, you're prompted tooenter values for them.</span></span>  <span data-ttu-id="49901-176">Voer Hallo-naam van de resourcegroep Hallo en Hallo automation-account die gaat toocollect taakgegevens uit.</span><span class="sxs-lookup"><span data-stu-id="49901-176">Enter hello name of hello resource group and hello automation account that your going toocollect job information from.</span></span>
4. <span data-ttu-id="49901-177">Klik op **Start** toohello hello runbook starten.</span><span class="sxs-lookup"><span data-stu-id="49901-177">Click **Start** toohello start hello runbook.</span></span>
3. <span data-ttu-id="49901-178">Hallo runbook wordt gestart met de status van **in de wachtrij geplaatst** voordat het kloonproces te**met**.</span><span class="sxs-lookup"><span data-stu-id="49901-178">hello runbook will start with a status of **Queued** before it goes too**Running**.</span></span>  
3. <span data-ttu-id="49901-179">Hallo runbook uitgebreide uitvoer moet worden weergegeven met Hallo-taken verzameld in json-indeling.</span><span class="sxs-lookup"><span data-stu-id="49901-179">hello runbook should display verbose output with hello jobs collected in json format.</span></span>  <span data-ttu-id="49901-180">Als er geen taken worden weergegeven, klikt u vervolgens er mogelijk is er geen taken die zijn gemaakt in automation-account in Hallo Hallo afgelopen uur.</span><span class="sxs-lookup"><span data-stu-id="49901-180">If no jobs are listed, then there may have been no jobs created in hello automation account in hello last hour.</span></span>  <span data-ttu-id="49901-181">Probeer een runbook wordt gestart in Hallo automation-account en Voer Hallo test vervolgens opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="49901-181">Try starting any runbook in hello automation account and then perform hello test again.</span></span>
4. <span data-ttu-id="49901-182">Zorg ervoor dat Hallo uitvoer wordt niet weergegeven na de eventuele fouten in Hallo opdracht tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="49901-182">Ensure that hello output doesn't show any errors in hello post command tooLog Analytics.</span></span>  <span data-ttu-id="49901-183">U hebt een bericht vergelijkbaar toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="49901-183">You should have a message similar toohello following.</span></span>

    ![Post-uitvoer](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="49901-185">5. Controleer de records in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="49901-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="49901-186">Als Hallo runbook in de test is voltooid en u gecontroleerd dat Hallo uitvoer is ontvangen, kunt u controleren Hallo records zijn gemaakt met een [logboek zoeken in logboekanalyse](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="49901-186">Once hello runbook has completed in test, and you verified that hello output was successfully received, you can verify that hello records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Logboekuitvoer](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="49901-188">Hallo Azure-portal, selecteer uw werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="49901-188">In hello Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="49901-189">Klik op **Meld zoeken**.</span><span class="sxs-lookup"><span data-stu-id="49901-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="49901-190">Type Hallo na de opdracht `Type=AutomationJob_CL` en klik op de knop Zoeken Hallo.</span><span class="sxs-lookup"><span data-stu-id="49901-190">Type hello following command `Type=AutomationJob_CL` and click hello search button.</span></span> <span data-ttu-id="49901-191">Houd er rekening mee dat het recordtype Hallo _CL die niet is opgegeven in de script Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="49901-191">Note that hello record type includes _CL that isn't specified in hello script.</span></span>  <span data-ttu-id="49901-192">Dat achtervoegsel wordt automatisch toegevoegd toohello logboek type tooindicate dat het een type aangepaste logboek is.</span><span class="sxs-lookup"><span data-stu-id="49901-192">That suffix is automatically appended toohello log type tooindicate that it's a custom log type.</span></span>
4. <span data-ttu-id="49901-193">Hier ziet u een of meer records geretourneerd die aangeeft dat runbook Hallo werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="49901-193">You should see one or more records returned indicating that hello runbook is working as expected.</span></span>


## <a name="6-publish-hello-runbook"></a><span data-ttu-id="49901-194">6. Hallo runbook publiceren</span><span class="sxs-lookup"><span data-stu-id="49901-194">6. Publish hello runbook</span></span>
<span data-ttu-id="49901-195">Nadat u hebt geverifieerd dat Hallo runbook correct werkt, moet u toopublish zodat u deze in productie kan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="49901-195">Once you've verified that hello runbook is working correctly, you need toopublish it so you can run it in production.</span></span>  <span data-ttu-id="49901-196">U kunt doorgaan tooedit en Hallo runbook testen zonder de gepubliceerde versie Hallo worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="49901-196">You can continue tooedit and test hello runbook without modifying hello published version.</span></span>  

![Runbook publiceren](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="49901-198">Automation-account tooyour retourneren.</span><span class="sxs-lookup"><span data-stu-id="49901-198">Return tooyour automation account.</span></span>
2. <span data-ttu-id="49901-199">Klik op **Runbooks** en selecteer **verzamelen-Automation-taken**.</span><span class="sxs-lookup"><span data-stu-id="49901-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="49901-200">Klik op **bewerken** en vervolgens **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="49901-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="49901-201">Klik op **Ja** wanneer gestelde tooverify dat u wilt dat toooverwrite Hallo eerder gepubliceerde versie.</span><span class="sxs-lookup"><span data-stu-id="49901-201">Click **Yes** when asked tooverify that you want toooverwrite hello previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="49901-202">7. Opties voor logboekregistratie instellen</span><span class="sxs-lookup"><span data-stu-id="49901-202">7. Set logging options</span></span> 
<span data-ttu-id="49901-203">Test, die u zou kunnen tooview [uitgebreide uitvoer](../automation/automation-runbook-output-and-messages.md#message-streams) omdat u de variabele $VerbosePreference Hallo in Hallo script ingesteld.</span><span class="sxs-lookup"><span data-stu-id="49901-203">For test, you were able tooview [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set hello $VerbosePreference variable in hello script.</span></span>  <span data-ttu-id="49901-204">Voor productie moet u tooset Hallo logboekeigenschappen voor Hallo runbook als u wilt dat tooview uitgebreide uitvoer.</span><span class="sxs-lookup"><span data-stu-id="49901-204">For production, you need tooset hello logging properties for hello runbook if you want tooview verbose output.</span></span>  <span data-ttu-id="49901-205">Voor Hallo runbook in deze zelfstudie gebruikt, wordt dit Hallo json-gegevens worden verzonden tooLog Analytics weergegeven.</span><span class="sxs-lookup"><span data-stu-id="49901-205">For hello runbook used in this tutorial, this will display hello json data being sent tooLog Analytics.</span></span>

![Logboekregistratie en tracering](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="49901-207">Selecteer in het Hallo-eigenschappen voor uw runbook **logboekregistratie en tracering** onder **Runbookinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="49901-207">In hello properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="49901-208">Wijzig de instelling Hallo voor **logboekregistratie van uitgebreide records** te**op**.</span><span class="sxs-lookup"><span data-stu-id="49901-208">Change hello setting for **Log verbose records** too**On**.</span></span>
3. <span data-ttu-id="49901-209">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="49901-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="49901-210">8. Runbook plannen</span><span class="sxs-lookup"><span data-stu-id="49901-210">8. Schedule runbook</span></span>
<span data-ttu-id="49901-211">Hallo meest voorkomende manier toostart een runbook dat bewakingsgegevens verzamelt is tooschedule het toorun automatisch.</span><span class="sxs-lookup"><span data-stu-id="49901-211">hello most common way toostart a runbook that collects monitoring data is tooschedule it toorun automatically.</span></span>  <span data-ttu-id="49901-212">U dit doen door het maken van een [schema in Azure Automation](../automation/automation-schedules.md) en tooyour runbook kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="49901-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it tooyour runbook.</span></span>

![Runbook plannen](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="49901-214">Selecteer in de eigenschappen voor uw runbook hello **planningen** onder **Resources**.</span><span class="sxs-lookup"><span data-stu-id="49901-214">In hello properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="49901-215">Klik op **toevoegen van een planning** > **koppelen van een planning tooyour runbook** > **Maak een nieuwe planning**.</span><span class="sxs-lookup"><span data-stu-id="49901-215">Click **Add a schedule** > **Link a schedule tooyour runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="49901-216">Typ waarden voor Hallo planning en klik op volgende Hallo **maken**.</span><span class="sxs-lookup"><span data-stu-id="49901-216">Type in hello following values for hello schedule and click **Create**.</span></span>

| <span data-ttu-id="49901-217">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="49901-217">Property</span></span> | <span data-ttu-id="49901-218">Waarde</span><span class="sxs-lookup"><span data-stu-id="49901-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="49901-219">Naam</span><span class="sxs-lookup"><span data-stu-id="49901-219">Name</span></span> | <span data-ttu-id="49901-220">AutomationJobs-per uur</span><span class="sxs-lookup"><span data-stu-id="49901-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="49901-221">Wordt gestart</span><span class="sxs-lookup"><span data-stu-id="49901-221">Starts</span></span> | <span data-ttu-id="49901-222">Selecteer elk gewenst moment minstens 5 minuten afgelopen Hallo huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="49901-222">Select any time at least 5 minutes past hello current time.</span></span> |
| <span data-ttu-id="49901-223">Terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="49901-223">Recurrence</span></span> | <span data-ttu-id="49901-224">Terugkerend</span><span class="sxs-lookup"><span data-stu-id="49901-224">Recurring</span></span> |
| <span data-ttu-id="49901-225">Herhaald elke</span><span class="sxs-lookup"><span data-stu-id="49901-225">Recur every</span></span> | <span data-ttu-id="49901-226">1 uur</span><span class="sxs-lookup"><span data-stu-id="49901-226">1 hour</span></span> |
| <span data-ttu-id="49901-227">Vervaldatum van de set</span><span class="sxs-lookup"><span data-stu-id="49901-227">Set expiration</span></span> | <span data-ttu-id="49901-228">Nee</span><span class="sxs-lookup"><span data-stu-id="49901-228">No</span></span> |

<span data-ttu-id="49901-229">Als Hallo planning is gemaakt, moet u tooset Hallo parameterwaarden die worden gebruikt telkens wanneer die deze planning Hallo runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="49901-229">Once hello schedule is created, you need tooset hello parameter values that will be used each time this schedule starts hello runbook.</span></span>

6. <span data-ttu-id="49901-230">Klik op **parameters configureren en instellingen uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="49901-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="49901-231">Vul in de waarden voor uw **ResourceGroupName** en **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="49901-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="49901-232">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="49901-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="49901-233">9. Controleer of u runbook wordt gestart volgens planning</span><span class="sxs-lookup"><span data-stu-id="49901-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="49901-234">Telkens wanneer een runbook wordt gestart, [wordt een taak gemaakt](../automation/automation-runbook-execution.md) en eventuele uitvoer in het logboek geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="49901-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="49901-235">Dit zijn in feite Hallo verzamelen van dezelfde taken die Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="49901-235">In fact, these are hello same jobs that hello runbook is collecting.</span></span>  <span data-ttu-id="49901-236">U kunt controleren dat Hallo runbook start zoals verwacht door het Hallo-taken voor het Hallo-runbook controleren na de begintijd Hallo voor Hallo planning is verstreken.</span><span class="sxs-lookup"><span data-stu-id="49901-236">You can verify that hello runbook starts as expected by checking hello jobs for hello runbook after hello start time for hello schedule has passed.</span></span>

![Taken](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="49901-238">Selecteer in de eigenschappen voor uw runbook hello **taken** onder **Resources**.</span><span class="sxs-lookup"><span data-stu-id="49901-238">In hello properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="49901-239">U ziet dat een lijst met taken voor elke keer Hallo runbook is gestart.</span><span class="sxs-lookup"><span data-stu-id="49901-239">You should see a listing of jobs for each time hello runbook was started.</span></span>
3. <span data-ttu-id="49901-240">Klik op een van de Hallo taken tooview de details ervan.</span><span class="sxs-lookup"><span data-stu-id="49901-240">Click on one of hello jobs tooview its details.</span></span>
4. <span data-ttu-id="49901-241">Klik op **alle logboeken** tooview Hallo logboeken en uitvoer van Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="49901-241">Click on **All logs** tooview hello logs and output from hello runbook.</span></span>
5. <span data-ttu-id="49901-242">Schuif toohello onder toofind een vermelding vergelijkbare toohello in onderstaande afbeelding.</span><span class="sxs-lookup"><span data-stu-id="49901-242">Scroll toohello bottom toofind an entry similar toohello image below.</span></span><br>![Uitgebreide](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="49901-244">Klik op deze vermelding tooview Hallo gedetailleerde json-gegevens die tooLog Analytics is verzonden.</span><span class="sxs-lookup"><span data-stu-id="49901-244">Click on this entry tooview hello detailed json data  that was sent tooLog Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="49901-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="49901-245">Next steps</span></span>
- <span data-ttu-id="49901-246">Gebruik [ontwerper](../log-analytics/log-analytics-view-designer.md) toocreate weergeven van een weergave Hallo gegevens dat u toohello logboekanalyse opslagplaats hebt verzameld.</span><span class="sxs-lookup"><span data-stu-id="49901-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) toocreate a view displaying hello data that you've collected toohello Log Analytics repository.</span></span>
- <span data-ttu-id="49901-247">Uw runbook in het pakket een [beheeroplossing](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span><span class="sxs-lookup"><span data-stu-id="49901-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span></span>
- <span data-ttu-id="49901-248">Meer informatie over [logboekanalyse](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="49901-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="49901-249">Meer informatie over [Azure Automation](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="49901-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="49901-250">Meer informatie over Hallo [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="49901-250">Learn more about hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>
