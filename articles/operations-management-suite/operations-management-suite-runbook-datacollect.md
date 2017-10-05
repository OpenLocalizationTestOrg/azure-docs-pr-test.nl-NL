---
title: Verzamelen van gegevens met een runbook in Azure Automation Log Analytics | Microsoft Docs
description: Stapsgewijze zelfstudie die helpt bij het maken van een runbook in Azure Automation voor het verzamelen van gegevens in de OMS-opslagplaats voor analyse van logboekanalyse.
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
ms.openlocfilehash: 59f674c9c6404da7f5384539189f41a4ba1a939a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="ba787-103">Gegevens verzamelen in logboekanalyse met een Azure Automation-runbook</span><span class="sxs-lookup"><span data-stu-id="ba787-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="ba787-104">U kunt een aanzienlijke hoeveelheid gegevens in logboekanalyse verzamelen uit diverse bronnen, zoals [gegevensbronnen](../log-analytics/log-analytics-data-sources.md) op agents en ook [gegevens verzameld van Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ba787-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="ba787-105">Er zijn een scenario's waarin u wilt verzamelen van gegevens die niet worden geopend via deze standaard bronnen.</span><span class="sxs-lookup"><span data-stu-id="ba787-105">There are a scenarios though where you need to collect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="ba787-106">In dergelijke gevallen kunt u de [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) om gegevens te schrijven met logboekanalyse vanaf elke client REST-API.</span><span class="sxs-lookup"><span data-stu-id="ba787-106">In these cases, you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span></span>  <span data-ttu-id="ba787-107">Een veelgebruikte methode voor het uitvoeren van deze gegevensverzameling maakt gebruik van een runbook in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ba787-107">A common method to perform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="ba787-108">Deze zelfstudie wordt door het proces voor het maken en plannen van een runbook in Azure Automation om gegevens te schrijven met logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="ba787-108">This tutorial walks through the process for creating and scheduling a runbook in Azure Automation to write data to Log Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ba787-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ba787-109">Prerequisites</span></span>
<span data-ttu-id="ba787-110">Dit scenario vereist de volgende bronnen die zijn geconfigureerd in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ba787-110">This scenario requires the following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="ba787-111">Beide mag een gratis account.</span><span class="sxs-lookup"><span data-stu-id="ba787-111">Both can be a free account.</span></span>

- <span data-ttu-id="ba787-112">[Meld u werkruimte](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ba787-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="ba787-113">[Azure automation-account](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ba787-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="ba787-114">Overzicht van scenario</span><span class="sxs-lookup"><span data-stu-id="ba787-114">Overview of scenario</span></span>
<span data-ttu-id="ba787-115">Voor deze zelfstudie schrijft u een runbook dat informatie over het automatiseren van taken verzamelt.</span><span class="sxs-lookup"><span data-stu-id="ba787-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="ba787-116">Azure Automation-Runbooks worden geïmplementeerd met PowerShell, zodat u beginnen door te schrijven en testen van een script in de Azure Automation-editor.</span><span class="sxs-lookup"><span data-stu-id="ba787-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in the Azure Automation editor.</span></span>  <span data-ttu-id="ba787-117">Zodra u hebt gecontroleerd dat u de vereiste gegevens wilt verzamelen, hebt u die gegevens schrijven naar Log Analytics en controleer of het aangepaste gegevenstype.</span><span class="sxs-lookup"><span data-stu-id="ba787-117">Once you verify that you're collecting the required information, you'll write that data to Log Analytics and verify the custom data type.</span></span>  <span data-ttu-id="ba787-118">Ten slotte, maakt u een planning voor het starten van het runbook met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="ba787-118">Finally, you'll create a schedule to start the runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="ba787-119">U kunt Azure Automation voor het verzenden van informatie over de taak met logboekanalyse zonder dit runbook configureren.</span><span class="sxs-lookup"><span data-stu-id="ba787-119">You can configure Azure Automation to send job information to Log Analytics without this runbook.</span></span>  <span data-ttu-id="ba787-120">Dit scenario wordt voornamelijk gebruikt ter ondersteuning van de zelfstudie en het wordt aanbevolen dat u de gegevens naar een test-werkruimte verzenden.</span><span class="sxs-lookup"><span data-stu-id="ba787-120">This scenario is primarily used to support the tutorial, and it's recommended that you send the data to a test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="ba787-121">1. Data Collector API-module installeren</span><span class="sxs-lookup"><span data-stu-id="ba787-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="ba787-122">Elke [aanvraag van de API van HTTP-Data Collector](../log-analytics/log-analytics-data-collector-api.md#create-a-request) moet op de juiste manier zijn geformatteerd en autorisatie-header bevatten.</span><span class="sxs-lookup"><span data-stu-id="ba787-122">Every [request from the HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="ba787-123">U kunt dit doen in uw runbook, maar u kunt de hoeveelheid code vereist met behulp van een module die vereenvoudigt u dit proces verkleinen.</span><span class="sxs-lookup"><span data-stu-id="ba787-123">You can do this in your runbook, but you can reduce the amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="ba787-124">Een module die u kunt gebruiken is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in de PowerShell-galerie.</span><span class="sxs-lookup"><span data-stu-id="ba787-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in the PowerShell Gallery.</span></span>

<span data-ttu-id="ba787-125">Gebruik een [module](../automation/automation-integration-modules.md) in een runbook moet worden geïnstalleerd in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="ba787-125">To use a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="ba787-126">Elk runbook in hetzelfde account kunt vervolgens de functies gebruiken in de module.</span><span class="sxs-lookup"><span data-stu-id="ba787-126">Any runbook in the same account can then use the functions in the module.</span></span>  <span data-ttu-id="ba787-127">U kunt een nieuwe module installeren door te selecteren **activa** > **Modules** > **toevoegen van een module** in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="ba787-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="ba787-128">De PowerShell-galerie hebt u al een snelle mogelijkheid voor het implementeren van een module rechtstreeks op uw automation-account, zodat u deze optie voor deze zelfstudie gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="ba787-128">The PowerShell Gallery though gives you a quick option to deploy a module directly to your automation account so you can use that option for this tutorial.</span></span>  

![Module OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="ba787-130">Ga naar [PowerShell Gallery](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="ba787-130">Go to [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="ba787-131">Zoeken naar **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="ba787-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="ba787-132">Klik op de **implementeren in Azure Automation** knop.</span><span class="sxs-lookup"><span data-stu-id="ba787-132">Click on the **Deploy to Azure Automation** button.</span></span>
4. <span data-ttu-id="ba787-133">Selecteer uw automation-account en klik op **OK** de module te installeren.</span><span class="sxs-lookup"><span data-stu-id="ba787-133">Select your automation account and click **OK** to install the module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="ba787-134">2. Automation-variabelen maken</span><span class="sxs-lookup"><span data-stu-id="ba787-134">2. Create Automation variables</span></span>
<span data-ttu-id="ba787-135">[Automation-variabelen](..\automation\automation-variables.md) bevatten waarden die kunnen worden gebruikt door alle runbooks in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="ba787-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="ba787-136">Zij runbooks flexibelere doordat u deze waarden te wijzigen zonder de werkelijke runbook bewerken.</span><span class="sxs-lookup"><span data-stu-id="ba787-136">They make runbooks more flexible by allowing you to change these values without editing the actual runbook.</span></span> <span data-ttu-id="ba787-137">Elke aanvraag van de HTTP-gegevens Collector API vereist de ID en sleutel van de OMS-werkruimte en variabele assets zijn ideaal voor het opslaan van deze informatie.</span><span class="sxs-lookup"><span data-stu-id="ba787-137">Every request from the HTTP Data Collector API requires the ID and key of the OMS workspace, and variable assets are ideal to store this information.</span></span>  

![Variabelen](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="ba787-139">Ga in de Azure-portal naar uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="ba787-139">In the Azure portal, navigate to your Automation account.</span></span>
2. <span data-ttu-id="ba787-140">Selecteer **variabelen** onder **gedeelde Resources**.</span><span class="sxs-lookup"><span data-stu-id="ba787-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="ba787-141">Klik op **toevoegen van een variabele** en maken van de twee variabelen in de volgende tabel.</span><span class="sxs-lookup"><span data-stu-id="ba787-141">Click **Add a variable** and create the two variables in the following table.</span></span>

| <span data-ttu-id="ba787-142">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ba787-142">Property</span></span> | <span data-ttu-id="ba787-143">De waarde van de werkruimte-ID</span><span class="sxs-lookup"><span data-stu-id="ba787-143">Workspace ID Value</span></span> | <span data-ttu-id="ba787-144">De sleutelwaarde werkruimte</span><span class="sxs-lookup"><span data-stu-id="ba787-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="ba787-145">Naam</span><span class="sxs-lookup"><span data-stu-id="ba787-145">Name</span></span> | <span data-ttu-id="ba787-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="ba787-146">WorkspaceId</span></span> | <span data-ttu-id="ba787-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="ba787-147">WorkspaceKey</span></span> |
| <span data-ttu-id="ba787-148">Type</span><span class="sxs-lookup"><span data-stu-id="ba787-148">Type</span></span> | <span data-ttu-id="ba787-149">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ba787-149">String</span></span> | <span data-ttu-id="ba787-150">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ba787-150">String</span></span> |
| <span data-ttu-id="ba787-151">Waarde</span><span class="sxs-lookup"><span data-stu-id="ba787-151">Value</span></span> | <span data-ttu-id="ba787-152">In de werkruimte-ID van de werkruimte voor logboekanalyse te plakken.</span><span class="sxs-lookup"><span data-stu-id="ba787-152">Paste in the Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="ba787-153">Plakken aan met de primaire of secundaire sleutel van de werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="ba787-153">Paste in with the Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="ba787-154">Versleuteld</span><span class="sxs-lookup"><span data-stu-id="ba787-154">Encrypted</span></span> | <span data-ttu-id="ba787-155">Nee</span><span class="sxs-lookup"><span data-stu-id="ba787-155">No</span></span> | <span data-ttu-id="ba787-156">Ja</span><span class="sxs-lookup"><span data-stu-id="ba787-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="ba787-157">3. Runbook maken</span><span class="sxs-lookup"><span data-stu-id="ba787-157">3. Create runbook</span></span>

<span data-ttu-id="ba787-158">Azure Automation heeft een editor in de portal kunt u bewerken en test uw runbook.</span><span class="sxs-lookup"><span data-stu-id="ba787-158">Azure Automation has an editor in the portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="ba787-159">U hebt de mogelijkheid de scripteditor gebruiken om te werken met [PowerShell rechtstreeks](../automation/automation-edit-textual-runbook.md) of [maken van een grafisch runbook](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="ba787-159">You have the option to use the script editor to work with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="ba787-160">Voor deze zelfstudie werkt u met een PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="ba787-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Runbook bewerken](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="ba787-162">Navigeer naar uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="ba787-162">Navigate to your Automation account.</span></span>  
2. <span data-ttu-id="ba787-163">Klik op **Runbooks** > **een runbook toevoegen** > **een nieuw runbook maken**.</span><span class="sxs-lookup"><span data-stu-id="ba787-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="ba787-164">Typ voor de runbooknaam **verzamelen-Automation-taken**.</span><span class="sxs-lookup"><span data-stu-id="ba787-164">For the runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="ba787-165">Selecteer het runbooktype **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ba787-165">For the runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="ba787-166">Klik op **maken** voor het maken van het runbook en start de editor.</span><span class="sxs-lookup"><span data-stu-id="ba787-166">Click **Create** to create the runbook and start the editor.</span></span>
5. <span data-ttu-id="ba787-167">Kopieer en plak de volgende code in het runbook.</span><span class="sxs-lookup"><span data-stu-id="ba787-167">Copy and paste the following code into the runbook.</span></span>  <span data-ttu-id="ba787-168">Raadpleeg de opmerkingen in het script voor een uitleg van de code.</span><span class="sxs-lookup"><span data-stu-id="ba787-168">Refer to the comments in the script for explanation of the code.</span></span>
    
        # Get information required for the automation account from parameter values when the runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate to the Automation account using the Azure connection created when the Automation account was created.
        # Code copied from the runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set the $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set the name of the record type.
        $logType = "AutomationJob"
        
        # Get the jobs from the past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert the job data to json
            $body = $jobs | ConvertTo-Json
        
            # Write the body to verbose output so we can inspect it if verbose logging is on for the runbook.
            Write-Verbose $body
        
            # Send the data to Log Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="ba787-169">4. Runbook-test</span><span class="sxs-lookup"><span data-stu-id="ba787-169">4. Test runbook</span></span>
<span data-ttu-id="ba787-170">Azure Automation omvat een omgeving naar [test uw runbook](../automation/automation-testing-runbook.md) voordat u deze hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="ba787-170">Azure Automation includes an environment to [test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="ba787-171">U kunt de gegevens die worden verzameld door het runbook controleren en nagaan of dat deze met logboekanalyse schrijft naar verwachting voordat het wordt gepubliceerd naar productie.</span><span class="sxs-lookup"><span data-stu-id="ba787-171">You can inspect the data collected by the runbook and verify that it writes to Log Analytics as expected before publishing it to production.</span></span> 
 
![Runbook-test](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="ba787-173">Klik op **opslaan** om op te slaan van het runbook.</span><span class="sxs-lookup"><span data-stu-id="ba787-173">Click **Save** to save the runbook.</span></span>
1. <span data-ttu-id="ba787-174">Klik op **testvenster** openen van het runbook in de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ba787-174">Click **Test pane** to open the runbook in the test environment.</span></span>
3. <span data-ttu-id="ba787-175">Nadat uw runbook parameters heeft, wordt u gevraagd waarden op te geven voor hen.</span><span class="sxs-lookup"><span data-stu-id="ba787-175">Since your runbook has parameters, you're prompted to enter values for them.</span></span>  <span data-ttu-id="ba787-176">Voer de naam van de resourcegroep en de automation-account die uw gaat voor het verzamelen van informatie over de taak uit.</span><span class="sxs-lookup"><span data-stu-id="ba787-176">Enter the name of the resource group and the automation account that your going to collect job information from.</span></span>
4. <span data-ttu-id="ba787-177">Klik op **Start** toe aan het begin van het runbook.</span><span class="sxs-lookup"><span data-stu-id="ba787-177">Click **Start** to the start the runbook.</span></span>
3. <span data-ttu-id="ba787-178">Het runbook wordt gestart met de status van **in de wachtrij geplaatst** voordat deze verwijst **met**.</span><span class="sxs-lookup"><span data-stu-id="ba787-178">The runbook will start with a status of **Queued** before it goes to **Running**.</span></span>  
3. <span data-ttu-id="ba787-179">Het runbook uitgebreide uitvoer moet worden weergegeven met de taken die worden verzameld in json-indeling.</span><span class="sxs-lookup"><span data-stu-id="ba787-179">The runbook should display verbose output with the jobs collected in json format.</span></span>  <span data-ttu-id="ba787-180">Als er geen taken worden weergegeven, klikt u vervolgens er mogelijk is er geen taken in het automation-account in het afgelopen uur gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ba787-180">If no jobs are listed, then there may have been no jobs created in the automation account in the last hour.</span></span>  <span data-ttu-id="ba787-181">Probeer een runbook wordt gestart in de automation-account en voer de test vervolgens opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="ba787-181">Try starting any runbook in the automation account and then perform the test again.</span></span>
4. <span data-ttu-id="ba787-182">Zorg ervoor dat de uitvoer met logboekanalyse fouten wordt niet in de post-opdracht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ba787-182">Ensure that the output doesn't show any errors in the post command to Log Analytics.</span></span>  <span data-ttu-id="ba787-183">U hebt een bericht dat lijkt op het volgende.</span><span class="sxs-lookup"><span data-stu-id="ba787-183">You should have a message similar to the following.</span></span>

    ![Post-uitvoer](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="ba787-185">5. Controleer de records in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ba787-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="ba787-186">Als het runbook in de test is voltooid en u geverifieerd dat de uitvoer is ontvangen, kunt u controleren of de records zijn gemaakt met behulp van een [logboek zoeken in logboekanalyse](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="ba787-186">Once the runbook has completed in test, and you verified that the output was successfully received, you can verify that the records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Logboekuitvoer](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="ba787-188">Selecteer in de Azure-portal uw werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="ba787-188">In the Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="ba787-189">Klik op **Meld zoeken**.</span><span class="sxs-lookup"><span data-stu-id="ba787-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="ba787-190">Typ de volgende opdracht `Type=AutomationJob_CL` en klik op de zoekknop.</span><span class="sxs-lookup"><span data-stu-id="ba787-190">Type the following command `Type=AutomationJob_CL` and click the search button.</span></span> <span data-ttu-id="ba787-191">Houd er rekening mee dat het recordtype _CL die niet is opgegeven in het script bevat.</span><span class="sxs-lookup"><span data-stu-id="ba787-191">Note that the record type includes _CL that isn't specified in the script.</span></span>  <span data-ttu-id="ba787-192">Dat achtervoegsel wordt automatisch toegevoegd aan het logboektype om aan te geven dat het een type aangepaste logboek is.</span><span class="sxs-lookup"><span data-stu-id="ba787-192">That suffix is automatically appended to the log type to indicate that it's a custom log type.</span></span>
4. <span data-ttu-id="ba787-193">Hier ziet u een of meer records geretourneerd die aangeeft dat het runbook correct werkt.</span><span class="sxs-lookup"><span data-stu-id="ba787-193">You should see one or more records returned indicating that the runbook is working as expected.</span></span>


## <a name="6-publish-the-runbook"></a><span data-ttu-id="ba787-194">6. Het runbook publiceren</span><span class="sxs-lookup"><span data-stu-id="ba787-194">6. Publish the runbook</span></span>
<span data-ttu-id="ba787-195">Nadat u hebt geverifieerd dat het runbook correct werkt, moet u publiceert deze zodat u deze in productie kan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ba787-195">Once you've verified that the runbook is working correctly, you need to publish it so you can run it in production.</span></span>  <span data-ttu-id="ba787-196">U kunt doorgaan met bewerken en het runbook testen zonder te wijzigen van de gepubliceerde versie.</span><span class="sxs-lookup"><span data-stu-id="ba787-196">You can continue to edit and test the runbook without modifying the published version.</span></span>  

![Runbook publiceren](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="ba787-198">Ga terug naar uw automation-account.</span><span class="sxs-lookup"><span data-stu-id="ba787-198">Return to your automation account.</span></span>
2. <span data-ttu-id="ba787-199">Klik op **Runbooks** en selecteer **verzamelen-Automation-taken**.</span><span class="sxs-lookup"><span data-stu-id="ba787-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="ba787-200">Klik op **bewerken** en vervolgens **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="ba787-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="ba787-201">Klik op **Ja** wanneer u wordt gevraagd om te controleren dat u wilt de volgende eerder gepubliceerde versie overschrijven.</span><span class="sxs-lookup"><span data-stu-id="ba787-201">Click **Yes** when asked to verify that you want to overwrite the previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="ba787-202">7. Opties voor logboekregistratie instellen</span><span class="sxs-lookup"><span data-stu-id="ba787-202">7. Set logging options</span></span> 
<span data-ttu-id="ba787-203">Test, kon u om weer te geven [uitgebreide uitvoer](../automation/automation-runbook-output-and-messages.md#message-streams) omdat u de variabele $VerbosePreference in het script instellen.</span><span class="sxs-lookup"><span data-stu-id="ba787-203">For test, you were able to view [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set the $VerbosePreference variable in the script.</span></span>  <span data-ttu-id="ba787-204">Voor productie moet u de logboekregistratie-eigenschappen instellen voor het runbook als u wilt weergeven, uitgebreide uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ba787-204">For production, you need to set the logging properties for the runbook if you want to view verbose output.</span></span>  <span data-ttu-id="ba787-205">Voor het runbook in deze zelfstudie gebruikt, wordt de json-gegevens worden verzonden met logboekanalyse weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ba787-205">For the runbook used in this tutorial, this will display the json data being sent to Log Analytics.</span></span>

![Logboekregistratie en tracering](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="ba787-207">Selecteer in de eigenschappen voor uw runbook **logboekregistratie en tracering** onder **Runbookinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="ba787-207">In the properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="ba787-208">Wijzig de instelling voor **logboekregistratie van uitgebreide records** naar **op**.</span><span class="sxs-lookup"><span data-stu-id="ba787-208">Change the setting for **Log verbose records** to **On**.</span></span>
3. <span data-ttu-id="ba787-209">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ba787-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="ba787-210">8. Runbook plannen</span><span class="sxs-lookup"><span data-stu-id="ba787-210">8. Schedule runbook</span></span>
<span data-ttu-id="ba787-211">De meeste gevallen een runbook dat bewakingsgegevens verzamelt starten is om te plannen om automatisch uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ba787-211">The most common way to start a runbook that collects monitoring data is to schedule it to run automatically.</span></span>  <span data-ttu-id="ba787-212">U dit doen door het maken van een [schema in Azure Automation](../automation/automation-schedules.md) en aan uw runbook koppelen.</span><span class="sxs-lookup"><span data-stu-id="ba787-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it to your runbook.</span></span>

![Runbook plannen](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="ba787-214">Selecteer in de eigenschappen voor uw runbook **planningen** onder **Resources**.</span><span class="sxs-lookup"><span data-stu-id="ba787-214">In the properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="ba787-215">Klik op **toevoegen van een planning** > **een planning aan uw runbook koppelen** > **Maak een nieuwe planning**.</span><span class="sxs-lookup"><span data-stu-id="ba787-215">Click **Add a schedule** > **Link a schedule to your runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="ba787-216">Typ de volgende waarden voor de planning en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="ba787-216">Type in the following values for the schedule and click **Create**.</span></span>

| <span data-ttu-id="ba787-217">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ba787-217">Property</span></span> | <span data-ttu-id="ba787-218">Waarde</span><span class="sxs-lookup"><span data-stu-id="ba787-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="ba787-219">Naam</span><span class="sxs-lookup"><span data-stu-id="ba787-219">Name</span></span> | <span data-ttu-id="ba787-220">AutomationJobs-per uur</span><span class="sxs-lookup"><span data-stu-id="ba787-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="ba787-221">Wordt gestart</span><span class="sxs-lookup"><span data-stu-id="ba787-221">Starts</span></span> | <span data-ttu-id="ba787-222">Selecteer die telkens wanneer u ten minste 5 minuten na de huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="ba787-222">Select any time at least 5 minutes past the current time.</span></span> |
| <span data-ttu-id="ba787-223">Terugkeerpatroon</span><span class="sxs-lookup"><span data-stu-id="ba787-223">Recurrence</span></span> | <span data-ttu-id="ba787-224">Terugkerend</span><span class="sxs-lookup"><span data-stu-id="ba787-224">Recurring</span></span> |
| <span data-ttu-id="ba787-225">Herhaald elke</span><span class="sxs-lookup"><span data-stu-id="ba787-225">Recur every</span></span> | <span data-ttu-id="ba787-226">1 uur</span><span class="sxs-lookup"><span data-stu-id="ba787-226">1 hour</span></span> |
| <span data-ttu-id="ba787-227">Vervaldatum van de set</span><span class="sxs-lookup"><span data-stu-id="ba787-227">Set expiration</span></span> | <span data-ttu-id="ba787-228">Nee</span><span class="sxs-lookup"><span data-stu-id="ba787-228">No</span></span> |

<span data-ttu-id="ba787-229">Zodra de planning is gemaakt, moet u de parameterwaarden die worden gebruikt telkens wanneer die deze planning wordt gestart voor het runbook instellen.</span><span class="sxs-lookup"><span data-stu-id="ba787-229">Once the schedule is created, you need to set the parameter values that will be used each time this schedule starts the runbook.</span></span>

6. <span data-ttu-id="ba787-230">Klik op **parameters configureren en instellingen uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="ba787-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="ba787-231">Vul in de waarden voor uw **ResourceGroupName** en **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="ba787-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="ba787-232">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ba787-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="ba787-233">9. Controleer of u runbook wordt gestart volgens planning</span><span class="sxs-lookup"><span data-stu-id="ba787-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="ba787-234">Telkens wanneer een runbook wordt gestart, [wordt een taak gemaakt](../automation/automation-runbook-execution.md) en eventuele uitvoer in het logboek geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="ba787-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="ba787-235">Dit zijn in feite hetzelfde taken die het verzamelen van het runbook.</span><span class="sxs-lookup"><span data-stu-id="ba787-235">In fact, these are the same jobs that the runbook is collecting.</span></span>  <span data-ttu-id="ba787-236">U kunt controleren of het runbook wordt gestart zoals verwacht door het controleren van de taken voor het runbook nadat de begintijd voor de planning is verstreken.</span><span class="sxs-lookup"><span data-stu-id="ba787-236">You can verify that the runbook starts as expected by checking the jobs for the runbook after the start time for the schedule has passed.</span></span>

![Taken](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="ba787-238">Selecteer in de eigenschappen voor uw runbook **taken** onder **Resources**.</span><span class="sxs-lookup"><span data-stu-id="ba787-238">In the properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="ba787-239">U ziet een lijst met taken voor elke keer dat het runbook is gestart.</span><span class="sxs-lookup"><span data-stu-id="ba787-239">You should see a listing of jobs for each time the runbook was started.</span></span>
3. <span data-ttu-id="ba787-240">Klik op een van de taken om de details ervan weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ba787-240">Click on one of the jobs to view its details.</span></span>
4. <span data-ttu-id="ba787-241">Klik op **alle logboeken** de logboekbestanden weergeven en de uitvoer van het runbook.</span><span class="sxs-lookup"><span data-stu-id="ba787-241">Click on **All logs** to view the logs and output from the runbook.</span></span>
5. <span data-ttu-id="ba787-242">Schuif naar beneden naar een vermelding zoeken die lijken op de onderstaande afbeelding.</span><span class="sxs-lookup"><span data-stu-id="ba787-242">Scroll to the bottom to find an entry similar to the image below.</span></span><br>![Uitgebreide](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="ba787-244">Klik op dit item om de gedetailleerde json-gegevens die is verzonden met logboekanalyse weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ba787-244">Click on this entry to view the detailed json data  that was sent to Log Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="ba787-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ba787-245">Next steps</span></span>
- <span data-ttu-id="ba787-246">Gebruik [ontwerper](../log-analytics/log-analytics-view-designer.md) voor het maken van een weergave om de gegevens die u hebt verzameld naar de opslagplaats voor logboekanalyse weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ba787-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) to create a view displaying the data that you've collected to the Log Analytics repository.</span></span>
- <span data-ttu-id="ba787-247">Uw runbook in het pakket een [beheeroplossing](operations-management-suite-solutions-creating.md) te distribueren naar klanten.</span><span class="sxs-lookup"><span data-stu-id="ba787-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) to distribute to customers.</span></span>
- <span data-ttu-id="ba787-248">Meer informatie over [logboekanalyse](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="ba787-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="ba787-249">Meer informatie over [Azure Automation](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="ba787-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="ba787-250">Meer informatie over de [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="ba787-250">Learn more about the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>