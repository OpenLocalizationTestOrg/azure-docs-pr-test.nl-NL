---
title: Starten en stoppen van virtuele machines met een Azure Automation - PowerShell Workflow | Microsoft Docs
description: Grafische versie van Azure Automation-scenario met inbegrip van runbooks starten en stoppen van klassieke virtuele machines.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="0cad4-103">Azure Automation-scenario: starten en stoppen van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="0cad4-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="0cad4-104">Dit scenario Azure Automation bevat runbooks starten en stoppen van klassieke virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="0cad4-104">This Azure Automation scenario includes runbooks to start and stop classic virtual machines.</span></span>  <span data-ttu-id="0cad4-105">U kunt dit scenario kunt gebruiken voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="0cad4-105">You can use this scenario for any of the following:</span></span>  

* <span data-ttu-id="0cad4-106">Gebruik de runbooks zonder aanpassingen in uw eigen omgeving.</span><span class="sxs-lookup"><span data-stu-id="0cad4-106">Use the runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="0cad4-107">Wijzig de runbooks voor het uitvoeren van aangepaste functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="0cad4-107">Modify the runbooks to perform customized functionality.</span></span>  
* <span data-ttu-id="0cad4-108">De runbooks aanroepen vanuit een ander runbook als onderdeel van een algemene oplossing.</span><span class="sxs-lookup"><span data-stu-id="0cad4-108">Call the runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="0cad4-109">Gebruik de runbooks als zelfstudies voor meer informatie over runbook authoring concepten.</span><span class="sxs-lookup"><span data-stu-id="0cad4-109">Use the runbooks as tutorials to learn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0cad4-110">Grafisch</span><span class="sxs-lookup"><span data-stu-id="0cad4-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="0cad4-111">PowerShell-werkstroom</span><span class="sxs-lookup"><span data-stu-id="0cad4-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="0cad4-112">Dit is de PowerShell Workflow-runbook-versie van dit scenario.</span><span class="sxs-lookup"><span data-stu-id="0cad4-112">This is the PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="0cad4-113">Het is ook beschikbaar via [grafische runbooks](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="0cad4-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="0cad4-114">Het scenario ophalen</span><span class="sxs-lookup"><span data-stu-id="0cad4-114">Getting the scenario</span></span>
<span data-ttu-id="0cad4-115">Dit scenario bestaat uit twee PowerShell Workflow-runbooks die u van de volgende koppelingen downloaden kunt.</span><span class="sxs-lookup"><span data-stu-id="0cad4-115">This scenario consists of two PowerShell Workflow runbooks that you can download from the following links.</span></span>  <span data-ttu-id="0cad4-116">Zie de [grafische versie](automation-solution-startstopvm-graphical.md) van dit scenario voor koppelingen naar grafische runbooks.</span><span class="sxs-lookup"><span data-stu-id="0cad4-116">See the [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links to the graphical runbooks.</span></span>

| <span data-ttu-id="0cad4-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="0cad4-117">Runbook</span></span> | <span data-ttu-id="0cad4-118">Koppeling</span><span class="sxs-lookup"><span data-stu-id="0cad4-118">Link</span></span> | <span data-ttu-id="0cad4-119">Type</span><span class="sxs-lookup"><span data-stu-id="0cad4-119">Type</span></span> | <span data-ttu-id="0cad4-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0cad4-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0cad4-121">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="0cad4-121">Start-AzureVMs</span></span> |[<span data-ttu-id="0cad4-122">Klassieke Azure-machines starten</span><span class="sxs-lookup"><span data-stu-id="0cad4-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="0cad4-123">PowerShell-werkstroom</span><span class="sxs-lookup"><span data-stu-id="0cad4-123">PowerShell Workflow</span></span> |<span data-ttu-id="0cad4-124">Start alle klassieke virtuele machines in een Azure subscriptionor alle virtuele machines met de naam van een bepaalde service.</span><span class="sxs-lookup"><span data-stu-id="0cad4-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="0cad4-125">Stop AzureVMs</span><span class="sxs-lookup"><span data-stu-id="0cad4-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="0cad4-126">Stoppen van Azure Classic VM 's</span><span class="sxs-lookup"><span data-stu-id="0cad4-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="0cad4-127">PowerShell-werkstroom</span><span class="sxs-lookup"><span data-stu-id="0cad4-127">PowerShell Workflow</span></span> |<span data-ttu-id="0cad4-128">Alle virtuele machines in een automation-account of alle virtuele machines met de naam van een bepaalde service stopt.</span><span class="sxs-lookup"><span data-stu-id="0cad4-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-the-scenario"></a><span data-ttu-id="0cad4-129">Installeren en configureren van het scenario</span><span class="sxs-lookup"><span data-stu-id="0cad4-129">Installing and configuring the scenario</span></span>
### <a name="1-install-the-runbooks"></a><span data-ttu-id="0cad4-130">1. De runbooks installeren</span><span class="sxs-lookup"><span data-stu-id="0cad4-130">1. Install the runbooks</span></span>
<span data-ttu-id="0cad4-131">Na het downloaden van de runbooks, kunt u ze met behulp van de procedure in importeren [importeren van een Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="0cad4-131">After downloading the runbooks, you can import them using the procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-the-description-and-requirements"></a><span data-ttu-id="0cad4-132">2. Lees de beschrijving en de vereisten</span><span class="sxs-lookup"><span data-stu-id="0cad4-132">2. Review the description and requirements</span></span>
<span data-ttu-id="0cad4-133">De runbooks bevatten opmerkingen help-tekst met een beschrijving en de vereiste activa.</span><span class="sxs-lookup"><span data-stu-id="0cad4-133">The runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="0cad4-134">U kunt ook dezelfde informatie opvragen uit dit artikel.</span><span class="sxs-lookup"><span data-stu-id="0cad4-134">You can also get the same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="0cad4-135">3. Activa configureren</span><span class="sxs-lookup"><span data-stu-id="0cad4-135">3. Configure assets</span></span>
<span data-ttu-id="0cad4-136">De runbooks vereisen de volgende elementen die u moet maken en vullen met de juiste waarden.</span><span class="sxs-lookup"><span data-stu-id="0cad4-136">The runbooks require the following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="0cad4-137">Activatype</span><span class="sxs-lookup"><span data-stu-id="0cad4-137">Asset Type</span></span> | <span data-ttu-id="0cad4-138">De Assetnaam van de</span><span class="sxs-lookup"><span data-stu-id="0cad4-138">Asset Name</span></span> | <span data-ttu-id="0cad4-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0cad4-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0cad4-140">Referentie</span><span class="sxs-lookup"><span data-stu-id="0cad4-140">Credential</span></span> |<span data-ttu-id="0cad4-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="0cad4-141">AzureCredential</span></span> |<span data-ttu-id="0cad4-142">Bevat de referenties voor een account dat gemachtigd is om te starten en stoppen van virtuele machines in het Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0cad4-142">Contains credentials for an account that has authority to start and stop virtual machines in the Azure subscription.</span></span>  <span data-ttu-id="0cad4-143">U kunt ook kunt u een andere referentie-element in de **referentie** parameter van de **Add-AzureAccount** activiteit.</span><span class="sxs-lookup"><span data-stu-id="0cad4-143">Alternatively, you can specify another credential asset in the **Credential** parameter of the **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="0cad4-144">Variabele</span><span class="sxs-lookup"><span data-stu-id="0cad4-144">Variable</span></span> |<span data-ttu-id="0cad4-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="0cad4-145">AzureSubscriptionId</span></span> |<span data-ttu-id="0cad4-146">Bevat de abonnement-ID van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0cad4-146">Contains the subscription ID of your Azure subscription.</span></span> |

## <a name="using-the-scenario"></a><span data-ttu-id="0cad4-147">Met behulp van het scenario</span><span class="sxs-lookup"><span data-stu-id="0cad4-147">Using the scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="0cad4-148">Parameters</span><span class="sxs-lookup"><span data-stu-id="0cad4-148">Parameters</span></span>
<span data-ttu-id="0cad4-149">De runbooks hebben de volgende parameters.</span><span class="sxs-lookup"><span data-stu-id="0cad4-149">The runbooks each have the following parameters.</span></span>  <span data-ttu-id="0cad4-150">U moet waarden opgeven voor de verplichte parameters en u kunt eventueel waarden opgeven voor de andere parameters, afhankelijk van uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="0cad4-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="0cad4-151">Parameter</span><span class="sxs-lookup"><span data-stu-id="0cad4-151">Parameter</span></span> | <span data-ttu-id="0cad4-152">Type</span><span class="sxs-lookup"><span data-stu-id="0cad4-152">Type</span></span> | <span data-ttu-id="0cad4-153">Verplicht</span><span class="sxs-lookup"><span data-stu-id="0cad4-153">Mandatory</span></span> | <span data-ttu-id="0cad4-154">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0cad4-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0cad4-155">Servicenaam</span><span class="sxs-lookup"><span data-stu-id="0cad4-155">ServiceName</span></span> |<span data-ttu-id="0cad4-156">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0cad4-156">string</span></span> |<span data-ttu-id="0cad4-157">Nee</span><span class="sxs-lookup"><span data-stu-id="0cad4-157">No</span></span> |<span data-ttu-id="0cad4-158">Als een waarde is opgegeven, worden alle virtuele machines met die servicenaam de gestart of gestopt.</span><span class="sxs-lookup"><span data-stu-id="0cad4-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="0cad4-159">Als geen waarde is opgegeven, worden alle klassieke virtuele machines in het Azure-abonnement de gestart of gestopt.</span><span class="sxs-lookup"><span data-stu-id="0cad4-159">If no value is provided, then all classic virtual machines in the Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="0cad4-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="0cad4-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="0cad4-161">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0cad4-161">string</span></span> |<span data-ttu-id="0cad4-162">Nee</span><span class="sxs-lookup"><span data-stu-id="0cad4-162">No</span></span> |<span data-ttu-id="0cad4-163">Bevat de naam van de [variabelenactivum](#installing-and-configuring-the-scenario) die de abonnement-ID van uw Azure-abonnement bevat.</span><span class="sxs-lookup"><span data-stu-id="0cad4-163">Contains the name of the [variable asset](#installing-and-configuring-the-scenario) that contains the subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="0cad4-164">Als u een waarde niet opgeeft *AzureSubscriptionId* wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0cad4-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="0cad4-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="0cad4-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="0cad4-166">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0cad4-166">string</span></span> |<span data-ttu-id="0cad4-167">Nee</span><span class="sxs-lookup"><span data-stu-id="0cad4-167">No</span></span> |<span data-ttu-id="0cad4-168">Bevat de naam van de [referentieasset](#installing-and-configuring-the-scenario) die de referenties voor het runbook bevat.</span><span class="sxs-lookup"><span data-stu-id="0cad4-168">Contains the name of the [credential asset](#installing-and-configuring-the-scenario) that contains the credentials for the runbook to use.</span></span>  <span data-ttu-id="0cad4-169">Als u een waarde niet opgeeft *AzureCredential* wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0cad4-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-the-runbooks"></a><span data-ttu-id="0cad4-170">Starten van de runbooks</span><span class="sxs-lookup"><span data-stu-id="0cad4-170">Starting the runbooks</span></span>
<span data-ttu-id="0cad4-171">U kunt een van de methoden in [een runbook starten in Azure Automation](automation-starting-a-runbook.md) een van de runbooks in dit scenario te starten.</span><span class="sxs-lookup"><span data-stu-id="0cad4-171">You can use any of the methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to start either of the runbooks in this scenario.</span></span>

<span data-ttu-id="0cad4-172">De volgende voorbeeldopdrachten maakt gebruik van Windows PowerShell om uit te voeren **StartAzureVMs** alle virtuele machines starten met de naam van de *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="0cad4-172">The following sample commands uses Windows PowerShell to run **StartAzureVMs** to start all virtual machines with the service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="0cad4-173">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="0cad4-173">Output</span></span>
<span data-ttu-id="0cad4-174">De runbooks wordt [uitvoer van een bericht](automation-runbook-output-and-messages.md) voor elke virtuele machine die aangeeft of de instructie starten of stoppen met succes is ingediend.</span><span class="sxs-lookup"><span data-stu-id="0cad4-174">The runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not the start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="0cad4-175">U kunt zoeken naar een specifieke tekenreeks in de uitvoer van het resultaat voor elk runbook te bepalen.</span><span class="sxs-lookup"><span data-stu-id="0cad4-175">You can look for a specific string in the output to determine the result for each runbook.</span></span>  <span data-ttu-id="0cad4-176">De uitvoer-tekenreeksen worden in de volgende tabel vermeld.</span><span class="sxs-lookup"><span data-stu-id="0cad4-176">The possible output strings are listed in the following table.</span></span>

| <span data-ttu-id="0cad4-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="0cad4-177">Runbook</span></span> | <span data-ttu-id="0cad4-178">Voorwaarde</span><span class="sxs-lookup"><span data-stu-id="0cad4-178">Condition</span></span> | <span data-ttu-id="0cad4-179">Bericht</span><span class="sxs-lookup"><span data-stu-id="0cad4-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0cad4-180">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="0cad4-180">Start-AzureVMs</span></span> |<span data-ttu-id="0cad4-181">Virtuele machine wordt al uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0cad4-181">Virtual machine is already running</span></span> |<span data-ttu-id="0cad4-182">MyVM wordt al uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0cad4-182">MyVM is already running</span></span> |
| <span data-ttu-id="0cad4-183">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="0cad4-183">Start-AzureVMs</span></span> |<span data-ttu-id="0cad4-184">Start-aanvraag voor de virtuele machine zijn verzonden</span><span class="sxs-lookup"><span data-stu-id="0cad4-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="0cad4-185">MyVM is gestart</span><span class="sxs-lookup"><span data-stu-id="0cad4-185">MyVM has been started</span></span> |
| <span data-ttu-id="0cad4-186">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="0cad4-186">Start-AzureVMs</span></span> |<span data-ttu-id="0cad4-187">De startaanvraag voor de virtuele machine is mislukt</span><span class="sxs-lookup"><span data-stu-id="0cad4-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="0cad4-188">MyVM kan niet worden gestart</span><span class="sxs-lookup"><span data-stu-id="0cad4-188">MyVM failed to start</span></span> |
| <span data-ttu-id="0cad4-189">Stop AzureVMs</span><span class="sxs-lookup"><span data-stu-id="0cad4-189">Stop-AzureVMs</span></span> |<span data-ttu-id="0cad4-190">Virtuele machine is al gestopt.</span><span class="sxs-lookup"><span data-stu-id="0cad4-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="0cad4-191">MyVM is al gestopt.</span><span class="sxs-lookup"><span data-stu-id="0cad4-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="0cad4-192">Stop AzureVMs</span><span class="sxs-lookup"><span data-stu-id="0cad4-192">Stop-AzureVMs</span></span> |<span data-ttu-id="0cad4-193">Stoppen van de aanvraag voor de virtuele machine zijn verzonden</span><span class="sxs-lookup"><span data-stu-id="0cad4-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="0cad4-194">MyVM is gestopt</span><span class="sxs-lookup"><span data-stu-id="0cad4-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="0cad4-195">Stop AzureVMs</span><span class="sxs-lookup"><span data-stu-id="0cad4-195">Stop-AzureVMs</span></span> |<span data-ttu-id="0cad4-196">Aanvraag tot stoppen voor de virtuele machine is mislukt</span><span class="sxs-lookup"><span data-stu-id="0cad4-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="0cad4-197">MyVM kan niet stoppen</span><span class="sxs-lookup"><span data-stu-id="0cad4-197">MyVM failed to stop</span></span> |

<span data-ttu-id="0cad4-198">Bijvoorbeeld het volgende codefragment vanuit een runbook wordt gestart van alle virtuele machines met de naam van de service *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="0cad4-198">For example, the following code snippet from a runbook attempts to start all virtual machines with the service name *MyServiceName*.</span></span>  <span data-ttu-id="0cad4-199">Als een van de start-aanvragen mislukken, kunnen acties worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0cad4-199">If any of the start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="0cad4-200">In detail</span><span class="sxs-lookup"><span data-stu-id="0cad4-200">Detailed breakdown</span></span>
<span data-ttu-id="0cad4-201">Hier volgt een gedetailleerd overzicht van de runbooks in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="0cad4-201">Following is a detailed breakdown of the runbooks in this scenario.</span></span>  <span data-ttu-id="0cad4-202">Deze informatie kunt u alleen wilt leren van deze voor het ontwerpen van uw eigen automatiseringsscenario's of aanpassen van de runbooks.</span><span class="sxs-lookup"><span data-stu-id="0cad4-202">You can use this information to either customize the runbooks or just to learn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="0cad4-203">Parameters</span><span class="sxs-lookup"><span data-stu-id="0cad4-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="0cad4-204">De werkstroom wordt gestart met het ophalen van de waarden voor de [invoerparameters](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="0cad4-204">The workflow starts by getting the values for the [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="0cad4-205">Standaardnamen worden gebruikt als de namen van de asset niet wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0cad4-205">If the asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="0cad4-206">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="0cad4-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="0cad4-207">Deze regel wordt aangegeven dat de uitvoer van het runbook zal een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="0cad4-207">This line declares that the output of the runbook will be a string.</span></span>  <span data-ttu-id="0cad4-208">Dit is niet vereist, maar wordt aanbevolen voor wanneer het runbook wordt gebruikt als een [onderliggend runbook](automation-child-runbooks.md) zodat een bovenliggend runbook het uitvoertype weten kunnen verwachten.</span><span class="sxs-lookup"><span data-stu-id="0cad4-208">This is not required but is a best practice for when the runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know the output type to expect.</span></span>

### <a name="authentication"></a><span data-ttu-id="0cad4-209">Authentication</span><span class="sxs-lookup"><span data-stu-id="0cad4-209">Authentication</span></span>
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="0cad4-210">De volgende set regels de [referenties](automation-credentials.md) en Azure-abonnement dat wordt gebruikt voor de rest van het runbook.</span><span class="sxs-lookup"><span data-stu-id="0cad4-210">The next lines set the [credentials](automation-credentials.md) and Azure subscription that will be used for the rest of the runbook.</span></span>
<span data-ttu-id="0cad4-211">Eerst gebruiken we **Get-AutomationPSCredential** ophalen van de activa die de referenties die toegang heeft tot het starten en stoppen van virtuele machines in het Azure-abonnement bevat.</span><span class="sxs-lookup"><span data-stu-id="0cad4-211">First we use **Get-AutomationPSCredential** to get the asset that holds the credentials with access to start and stop virtual machines in the Azure subscription.</span></span> <span data-ttu-id="0cad4-212">**-AzureAccount** vervolgens dit activum gebruikt de referenties in te stellen.</span><span class="sxs-lookup"><span data-stu-id="0cad4-212">**Add-AzureAccount** then uses this asset to set the credentials.</span></span>  <span data-ttu-id="0cad4-213">De uitvoer is toegewezen aan een dummy-variabele, zodat deze niet is opgenomen in de runbookuitvoer.</span><span class="sxs-lookup"><span data-stu-id="0cad4-213">The output is assigned to a dummy variable so that it isn't included in the runbook output.</span></span>  

<span data-ttu-id="0cad4-214">De variabele asset met het abonnement-ID wordt vervolgens opgehaald met **Get-AutomationVariable** en het abonnement in te stellen **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="0cad4-214">The variable asset with the subscription ID is then retrieved with **Get-AutomationVariable** and the subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="0cad4-215">Virtuele machines ophalen</span><span class="sxs-lookup"><span data-stu-id="0cad4-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="0cad4-216">**Get-AzureVM** wordt gebruikt voor het ophalen van de virtuele machines die is voor het runbook geschikt.</span><span class="sxs-lookup"><span data-stu-id="0cad4-216">**Get-AzureVM** is used to retrieve the virtual machines the runbook will work with.</span></span>  <span data-ttu-id="0cad4-217">Als een waarde is opgegeven de **ServiceName** variabele, invoer en vervolgens alleen de virtuele machines met die servicenaam worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="0cad4-217">If a value is provided in the **ServiceName** input variable, then only the virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="0cad4-218">Als **ServiceName** is leeg, en vervolgens alle virtuele machines worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="0cad4-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="0cad4-219">Virtuele machines starten/stoppen en uitvoer te sturen</span><span class="sxs-lookup"><span data-stu-id="0cad4-219">Start/Stop virtual machines and send output</span></span>
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="0cad4-220">De volgende regels stap via elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0cad4-220">The next lines step through each virtual machine.</span></span>  <span data-ttu-id="0cad4-221">Eerste de **PowerState** van de virtuele machine wordt gecontroleerd om te zien of deze al uitgevoerd of is gestopt, afhankelijk van het runbook is.</span><span class="sxs-lookup"><span data-stu-id="0cad4-221">First the **PowerState** of the virtual machine is checked to see if it is already running or stopped, depending on the runbook.</span></span>  <span data-ttu-id="0cad4-222">Als het zich al in de doelstatus, is een bericht verzonden naar uitvoer en de runbook-ends.</span><span class="sxs-lookup"><span data-stu-id="0cad4-222">If it is already in the target state, then a message is sent to output, and the runbook ends.</span></span>  <span data-ttu-id="0cad4-223">Als dat niet het geval is, klikt u vervolgens **Start-AzureVM** of **Stop-AzureVM** wordt gebruikt om te starten of stoppen van de virtuele machine met het resultaat van de aanvraag aan een variabele opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0cad4-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used to attempt to start or stop the virtual machine with the result of the request stored to a variable.</span></span>  <span data-ttu-id="0cad4-224">Een bericht wordt dan gezonden naar uitvoer die aangeeft of de aanvraag om te starten of stoppen is verzonden.</span><span class="sxs-lookup"><span data-stu-id="0cad4-224">A message is then sent to output specifying whether the request to start or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cad4-225">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0cad4-225">Next steps</span></span>
* <span data-ttu-id="0cad4-226">Zie voor meer informatie over het werken met onderliggende runbooks, [onderliggende runbooks in Azure Automation](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="0cad4-226">To learn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="0cad4-227">Zie voor meer informatie over Uitvoerberichten tijdens de uitvoering van runbook en logboekregistratie om op te lossen, [Runbook uitvoer en berichten in Azure Automation](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="0cad4-227">To learn more about output messages during runbook execution and logging to help troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

