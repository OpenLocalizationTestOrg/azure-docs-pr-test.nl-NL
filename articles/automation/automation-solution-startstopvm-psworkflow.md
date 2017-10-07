---
title: aaaStarting en stoppen virtuele machines met een Azure Automation - PowerShell Workflow | Microsoft Docs
description: Grafische versie van Azure Automation-scenario met inbegrip van runbooks toostart en stop klassieke virtuele machines.
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
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="8e56f-103">Azure Automation-scenario: starten en stoppen van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="8e56f-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="8e56f-104">Dit scenario Azure Automation omvat runbooks toostart en stop klassieke virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8e56f-104">This Azure Automation scenario includes runbooks toostart and stop classic virtual machines.</span></span>  <span data-ttu-id="8e56f-105">U kunt dit scenario voor een van de volgende hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8e56f-105">You can use this scenario for any of hello following:</span></span>  

* <span data-ttu-id="8e56f-106">Hallo runbooks zonder aanpassingen gebruiken in uw eigen omgeving.</span><span class="sxs-lookup"><span data-stu-id="8e56f-106">Use hello runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="8e56f-107">Hallo runbooks tooperform aangepast functionaliteit wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8e56f-107">Modify hello runbooks tooperform customized functionality.</span></span>  
* <span data-ttu-id="8e56f-108">Hallo runbooks aanroepen vanuit een ander runbook als onderdeel van een algemene oplossing.</span><span class="sxs-lookup"><span data-stu-id="8e56f-108">Call hello runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="8e56f-109">Hallo runbooks gebruiken als zelfstudies toolearn runbook authoring concepten.</span><span class="sxs-lookup"><span data-stu-id="8e56f-109">Use hello runbooks as tutorials toolearn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e56f-110">Grafisch</span><span class="sxs-lookup"><span data-stu-id="8e56f-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="8e56f-111">PowerShell-werkstroom</span><span class="sxs-lookup"><span data-stu-id="8e56f-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="8e56f-112">Dit is Hallo PowerShell Workflow-runbook-versie van dit scenario.</span><span class="sxs-lookup"><span data-stu-id="8e56f-112">This is hello PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="8e56f-113">Het is ook beschikbaar via [grafische runbooks](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="8e56f-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="8e56f-114">Hallo scenario ophalen</span><span class="sxs-lookup"><span data-stu-id="8e56f-114">Getting hello scenario</span></span>
<span data-ttu-id="8e56f-115">Dit scenario bestaat uit twee PowerShell Workflow-runbooks die u kunt downloaden van Hallo koppelingen te volgen.</span><span class="sxs-lookup"><span data-stu-id="8e56f-115">This scenario consists of two PowerShell Workflow runbooks that you can download from hello following links.</span></span>  <span data-ttu-id="8e56f-116">Zie Hallo [grafische versie](automation-solution-startstopvm-graphical.md) van dit scenario voor koppelingen toohello grafische runbooks.</span><span class="sxs-lookup"><span data-stu-id="8e56f-116">See hello [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links toohello graphical runbooks.</span></span>

| <span data-ttu-id="8e56f-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="8e56f-117">Runbook</span></span> | <span data-ttu-id="8e56f-118">Koppeling</span><span class="sxs-lookup"><span data-stu-id="8e56f-118">Link</span></span> | <span data-ttu-id="8e56f-119">Type</span><span class="sxs-lookup"><span data-stu-id="8e56f-119">Type</span></span> | <span data-ttu-id="8e56f-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8e56f-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8e56f-121">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e56f-121">Start-AzureVMs</span></span> |[<span data-ttu-id="8e56f-122">Klassieke Azure-machines starten</span><span class="sxs-lookup"><span data-stu-id="8e56f-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="8e56f-123">PowerShell-werkstroom</span><span class="sxs-lookup"><span data-stu-id="8e56f-123">PowerShell Workflow</span></span> |<span data-ttu-id="8e56f-124">Start alle klassieke virtuele machines in een Azure subscriptionor alle virtuele machines met de naam van een bepaalde service.</span><span class="sxs-lookup"><span data-stu-id="8e56f-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="8e56f-125">Stop AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e56f-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="8e56f-126">Stoppen van Azure Classic VM 's</span><span class="sxs-lookup"><span data-stu-id="8e56f-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="8e56f-127">PowerShell-werkstroom</span><span class="sxs-lookup"><span data-stu-id="8e56f-127">PowerShell Workflow</span></span> |<span data-ttu-id="8e56f-128">Alle virtuele machines in een automation-account of alle virtuele machines met de naam van een bepaalde service stopt.</span><span class="sxs-lookup"><span data-stu-id="8e56f-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-hello-scenario"></a><span data-ttu-id="8e56f-129">Installeren en configureren van Hallo-scenario</span><span class="sxs-lookup"><span data-stu-id="8e56f-129">Installing and configuring hello scenario</span></span>
### <a name="1-install-hello-runbooks"></a><span data-ttu-id="8e56f-130">1. Hallo runbooks installeren</span><span class="sxs-lookup"><span data-stu-id="8e56f-130">1. Install hello runbooks</span></span>
<span data-ttu-id="8e56f-131">Na het downloaden van Hallo runbooks, kunt u deze importeren met behulp van de procedure Hallo in [importeren van een Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="8e56f-131">After downloading hello runbooks, you can import them using hello procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-hello-description-and-requirements"></a><span data-ttu-id="8e56f-132">2. Bekijk Hallo beschrijving en vereisten</span><span class="sxs-lookup"><span data-stu-id="8e56f-132">2. Review hello description and requirements</span></span>
<span data-ttu-id="8e56f-133">Hallo runbooks bevatten opmerkingen help-tekst met een beschrijving en de vereiste activa.</span><span class="sxs-lookup"><span data-stu-id="8e56f-133">hello runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="8e56f-134">U kunt ook ophalen Hallo dezelfde informatie uit dit artikel.</span><span class="sxs-lookup"><span data-stu-id="8e56f-134">You can also get hello same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="8e56f-135">3. Activa configureren</span><span class="sxs-lookup"><span data-stu-id="8e56f-135">3. Configure assets</span></span>
<span data-ttu-id="8e56f-136">Hallo runbooks vereisen Hallo assets die u moet maken en vullen met de juiste waarden te volgen.</span><span class="sxs-lookup"><span data-stu-id="8e56f-136">hello runbooks require hello following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="8e56f-137">Activatype</span><span class="sxs-lookup"><span data-stu-id="8e56f-137">Asset Type</span></span> | <span data-ttu-id="8e56f-138">De Assetnaam van de</span><span class="sxs-lookup"><span data-stu-id="8e56f-138">Asset Name</span></span> | <span data-ttu-id="8e56f-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8e56f-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8e56f-140">Referentie</span><span class="sxs-lookup"><span data-stu-id="8e56f-140">Credential</span></span> |<span data-ttu-id="8e56f-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="8e56f-141">AzureCredential</span></span> |<span data-ttu-id="8e56f-142">Bevat de referenties voor een account met autoriteit toostart stop de virtuele machines en in hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8e56f-142">Contains credentials for an account that has authority toostart and stop virtual machines in hello Azure subscription.</span></span>  <span data-ttu-id="8e56f-143">U kunt ook een andere referentie-element opgeven in Hallo **referentie** parameter Hallo **Add-AzureAccount** activiteit.</span><span class="sxs-lookup"><span data-stu-id="8e56f-143">Alternatively, you can specify another credential asset in hello **Credential** parameter of hello **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="8e56f-144">Variabele</span><span class="sxs-lookup"><span data-stu-id="8e56f-144">Variable</span></span> |<span data-ttu-id="8e56f-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="8e56f-145">AzureSubscriptionId</span></span> |<span data-ttu-id="8e56f-146">Hallo abonnements-ID van uw Azure-abonnement bevat.</span><span class="sxs-lookup"><span data-stu-id="8e56f-146">Contains hello subscription ID of your Azure subscription.</span></span> |

## <a name="using-hello-scenario"></a><span data-ttu-id="8e56f-147">Met behulp van Hallo scenario</span><span class="sxs-lookup"><span data-stu-id="8e56f-147">Using hello scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="8e56f-148">Parameters</span><span class="sxs-lookup"><span data-stu-id="8e56f-148">Parameters</span></span>
<span data-ttu-id="8e56f-149">Hallo runbooks hebben Hallo parameters te volgen.</span><span class="sxs-lookup"><span data-stu-id="8e56f-149">hello runbooks each have hello following parameters.</span></span>  <span data-ttu-id="8e56f-150">U moet waarden opgeven voor de verplichte parameters en u kunt eventueel waarden opgeven voor de andere parameters, afhankelijk van uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="8e56f-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="8e56f-151">Parameter</span><span class="sxs-lookup"><span data-stu-id="8e56f-151">Parameter</span></span> | <span data-ttu-id="8e56f-152">Type</span><span class="sxs-lookup"><span data-stu-id="8e56f-152">Type</span></span> | <span data-ttu-id="8e56f-153">Verplicht</span><span class="sxs-lookup"><span data-stu-id="8e56f-153">Mandatory</span></span> | <span data-ttu-id="8e56f-154">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8e56f-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8e56f-155">Servicenaam</span><span class="sxs-lookup"><span data-stu-id="8e56f-155">ServiceName</span></span> |<span data-ttu-id="8e56f-156">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e56f-156">string</span></span> |<span data-ttu-id="8e56f-157">Nee</span><span class="sxs-lookup"><span data-stu-id="8e56f-157">No</span></span> |<span data-ttu-id="8e56f-158">Als een waarde is opgegeven, worden alle virtuele machines met die servicenaam de gestart of gestopt.</span><span class="sxs-lookup"><span data-stu-id="8e56f-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="8e56f-159">Als geen waarde is opgegeven, worden alle klassieke virtuele machines in Azure-abonnement Hallo de gestart of gestopt.</span><span class="sxs-lookup"><span data-stu-id="8e56f-159">If no value is provided, then all classic virtual machines in hello Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="8e56f-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="8e56f-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="8e56f-161">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e56f-161">string</span></span> |<span data-ttu-id="8e56f-162">Nee</span><span class="sxs-lookup"><span data-stu-id="8e56f-162">No</span></span> |<span data-ttu-id="8e56f-163">Hallo naam bevat van Hallo [variabelenactivum](#installing-and-configuring-the-scenario) die Hallo abonnements-ID van uw Azure-abonnement bevat.</span><span class="sxs-lookup"><span data-stu-id="8e56f-163">Contains hello name of hello [variable asset](#installing-and-configuring-the-scenario) that contains hello subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="8e56f-164">Als u een waarde niet opgeeft *AzureSubscriptionId* wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e56f-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="8e56f-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="8e56f-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="8e56f-166">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e56f-166">string</span></span> |<span data-ttu-id="8e56f-167">Nee</span><span class="sxs-lookup"><span data-stu-id="8e56f-167">No</span></span> |<span data-ttu-id="8e56f-168">Hallo naam bevat van Hallo [referentieasset](#installing-and-configuring-the-scenario) die Hallo referenties voor Hallo runbook toouse bevat.</span><span class="sxs-lookup"><span data-stu-id="8e56f-168">Contains hello name of hello [credential asset](#installing-and-configuring-the-scenario) that contains hello credentials for hello runbook toouse.</span></span>  <span data-ttu-id="8e56f-169">Als u een waarde niet opgeeft *AzureCredential* wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e56f-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-hello-runbooks"></a><span data-ttu-id="8e56f-170">Hallo runbooks starten</span><span class="sxs-lookup"><span data-stu-id="8e56f-170">Starting hello runbooks</span></span>
<span data-ttu-id="8e56f-171">U kunt een van de methoden Hallo in [een runbook starten in Azure Automation](automation-starting-a-runbook.md) toostart ofwel Hallo runbooks in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="8e56f-171">You can use any of hello methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toostart either of hello runbooks in this scenario.</span></span>

<span data-ttu-id="8e56f-172">Hallo volgende voorbeeldopdrachten maakt gebruik van Windows PowerShell toorun **StartAzureVMs** toostart alle virtuele machines met de naam van de service Hallo *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="8e56f-172">hello following sample commands uses Windows PowerShell toorun **StartAzureVMs** toostart all virtual machines with hello service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="8e56f-173">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="8e56f-173">Output</span></span>
<span data-ttu-id="8e56f-174">Hallo runbooks wordt [uitvoer van een bericht](automation-runbook-output-and-messages.md) voor elke virtuele machine die aangeeft of start Hallo of stop-instructie is ingediend.</span><span class="sxs-lookup"><span data-stu-id="8e56f-174">hello runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not hello start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="8e56f-175">U kunt zoeken naar een specifieke tekenreeks in Hallo toodetermine hello uitvoerresultaat voor elk runbook.</span><span class="sxs-lookup"><span data-stu-id="8e56f-175">You can look for a specific string in hello output toodetermine hello result for each runbook.</span></span>  <span data-ttu-id="8e56f-176">Hallo eventuele uitvoertekenreeksen worden vermeld in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e56f-176">hello possible output strings are listed in hello following table.</span></span>

| <span data-ttu-id="8e56f-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="8e56f-177">Runbook</span></span> | <span data-ttu-id="8e56f-178">Voorwaarde</span><span class="sxs-lookup"><span data-stu-id="8e56f-178">Condition</span></span> | <span data-ttu-id="8e56f-179">Bericht</span><span class="sxs-lookup"><span data-stu-id="8e56f-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8e56f-180">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e56f-180">Start-AzureVMs</span></span> |<span data-ttu-id="8e56f-181">Virtuele machine wordt al uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8e56f-181">Virtual machine is already running</span></span> |<span data-ttu-id="8e56f-182">MyVM wordt al uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8e56f-182">MyVM is already running</span></span> |
| <span data-ttu-id="8e56f-183">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e56f-183">Start-AzureVMs</span></span> |<span data-ttu-id="8e56f-184">Start-aanvraag voor de virtuele machine zijn verzonden</span><span class="sxs-lookup"><span data-stu-id="8e56f-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="8e56f-185">MyVM is gestart</span><span class="sxs-lookup"><span data-stu-id="8e56f-185">MyVM has been started</span></span> |
| <span data-ttu-id="8e56f-186">Start AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e56f-186">Start-AzureVMs</span></span> |<span data-ttu-id="8e56f-187">De startaanvraag voor de virtuele machine is mislukt</span><span class="sxs-lookup"><span data-stu-id="8e56f-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="8e56f-188">MyVM toostart is mislukt</span><span class="sxs-lookup"><span data-stu-id="8e56f-188">MyVM failed toostart</span></span> |
| <span data-ttu-id="8e56f-189">Stop AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e56f-189">Stop-AzureVMs</span></span> |<span data-ttu-id="8e56f-190">Virtuele machine is al gestopt.</span><span class="sxs-lookup"><span data-stu-id="8e56f-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="8e56f-191">MyVM is al gestopt.</span><span class="sxs-lookup"><span data-stu-id="8e56f-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="8e56f-192">Stop AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e56f-192">Stop-AzureVMs</span></span> |<span data-ttu-id="8e56f-193">Stoppen van de aanvraag voor de virtuele machine zijn verzonden</span><span class="sxs-lookup"><span data-stu-id="8e56f-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="8e56f-194">MyVM is gestopt</span><span class="sxs-lookup"><span data-stu-id="8e56f-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="8e56f-195">Stop AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e56f-195">Stop-AzureVMs</span></span> |<span data-ttu-id="8e56f-196">Aanvraag tot stoppen voor de virtuele machine is mislukt</span><span class="sxs-lookup"><span data-stu-id="8e56f-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="8e56f-197">MyVM toostop is mislukt</span><span class="sxs-lookup"><span data-stu-id="8e56f-197">MyVM failed toostop</span></span> |

<span data-ttu-id="8e56f-198">Bijvoorbeeld Hallo volgende codefragment uit een runbook probeert toostart alle virtuele machines met de naam van de service Hallo *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="8e56f-198">For example, hello following code snippet from a runbook attempts toostart all virtual machines with hello service name *MyServiceName*.</span></span>  <span data-ttu-id="8e56f-199">Als een van de Hallo aanvragen mislukken start, kunnen acties worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8e56f-199">If any of hello start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="8e56f-200">In detail</span><span class="sxs-lookup"><span data-stu-id="8e56f-200">Detailed breakdown</span></span>
<span data-ttu-id="8e56f-201">Hier volgt een gedetailleerd overzicht van Hallo runbooks in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="8e56f-201">Following is a detailed breakdown of hello runbooks in this scenario.</span></span>  <span data-ttu-id="8e56f-202">U kunt deze informatie gebruiken tooeither hello runbooks of alleen toolearn daarvan voor het ontwerpen van uw eigen automatiseringsscenario's aanpassen.</span><span class="sxs-lookup"><span data-stu-id="8e56f-202">You can use this information tooeither customize hello runbooks or just toolearn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="8e56f-203">Parameters</span><span class="sxs-lookup"><span data-stu-id="8e56f-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="8e56f-204">Hallo werkstroom begint met het Hallo-waarden ophalen voor Hallo [invoerparameters](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="8e56f-204">hello workflow starts by getting hello values for hello [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="8e56f-205">Standaardnamen worden gebruikt als Hallo elementnamen zijn niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8e56f-205">If hello asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="8e56f-206">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="8e56f-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="8e56f-207">Deze regel wordt gedeclareerd Hallo-uitvoer van Hallo runbook is een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="8e56f-207">This line declares that hello output of hello runbook will be a string.</span></span>  <span data-ttu-id="8e56f-208">Dit is niet vereist, maar wordt aanbevolen voor wanneer Hallo runbook wordt gebruikt als een [onderliggend runbook](automation-child-runbooks.md) zodat een bovenliggend runbook Hallo uitvoer weten tooexpect typt.</span><span class="sxs-lookup"><span data-stu-id="8e56f-208">This is not required but is a best practice for when hello runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know hello output type tooexpect.</span></span>

### <a name="authentication"></a><span data-ttu-id="8e56f-209">Authentication</span><span class="sxs-lookup"><span data-stu-id="8e56f-209">Authentication</span></span>
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="8e56f-210">de volgende regels Hallo Hallo ingesteld [referenties](automation-credentials.md) en Azure-abonnement dat wordt gebruikt voor de rest van de runbook Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e56f-210">hello next lines set hello [credentials](automation-credentials.md) and Azure subscription that will be used for hello rest of hello runbook.</span></span>
<span data-ttu-id="8e56f-211">Eerst gebruiken we **Get-AutomationPSCredential** tooget Hallo asset die heeft Hallo-referenties met toegang tot virtuele machines toostart en stop in hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8e56f-211">First we use **Get-AutomationPSCredential** tooget hello asset that holds hello credentials with access toostart and stop virtual machines in hello Azure subscription.</span></span> <span data-ttu-id="8e56f-212">**-AzureAccount** maakt gebruik van deze asset tooset Hallo-referenties.</span><span class="sxs-lookup"><span data-stu-id="8e56f-212">**Add-AzureAccount** then uses this asset tooset hello credentials.</span></span>  <span data-ttu-id="8e56f-213">Hallo-uitvoer is tooa dummy-variabele toegewezen zodat deze niet is opgenomen in Hallo runbookuitvoer.</span><span class="sxs-lookup"><span data-stu-id="8e56f-213">hello output is assigned tooa dummy variable so that it isn't included in hello runbook output.</span></span>  

<span data-ttu-id="8e56f-214">Hallo-variabelenactivum met Hallo abonnement-ID wordt vervolgens opgehaald met **Get-AutomationVariable** en het Hallo-abonnement in te stellen **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="8e56f-214">hello variable asset with hello subscription ID is then retrieved with **Get-AutomationVariable** and hello subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="8e56f-215">Virtuele machines ophalen</span><span class="sxs-lookup"><span data-stu-id="8e56f-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="8e56f-216">**Get-AzureVM** is gebruikte tooretrieve Hallo virtuele machines Hallo runbook samenwerkt.</span><span class="sxs-lookup"><span data-stu-id="8e56f-216">**Get-AzureVM** is used tooretrieve hello virtual machines hello runbook will work with.</span></span>  <span data-ttu-id="8e56f-217">Als een waarde is opgegeven in Hallo **ServiceName** invoer variabele vervolgens alleen Hallo virtuele machines met die servicenaam worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="8e56f-217">If a value is provided in hello **ServiceName** input variable, then only hello virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="8e56f-218">Als **ServiceName** is leeg, en vervolgens alle virtuele machines worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="8e56f-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="8e56f-219">Virtuele machines starten/stoppen en uitvoer te sturen</span><span class="sxs-lookup"><span data-stu-id="8e56f-219">Start/Stop virtual machines and send output</span></span>
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="8e56f-220">de volgende regels Hallo stapsgewijs door elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8e56f-220">hello next lines step through each virtual machine.</span></span>  <span data-ttu-id="8e56f-221">Eerst Hallo **PowerState** Hallo virtuele machine is ingeschakeld toosee als deze al uitgevoerd of is gestopt, afhankelijk van het Hallo-runbook is.</span><span class="sxs-lookup"><span data-stu-id="8e56f-221">First hello **PowerState** of hello virtual machine is checked toosee if it is already running or stopped, depending on hello runbook.</span></span>  <span data-ttu-id="8e56f-222">Als het zich al in de doelstatus hello, klikt u vervolgens een bericht verzonden toooutput en Hallo runbook eindigt.</span><span class="sxs-lookup"><span data-stu-id="8e56f-222">If it is already in hello target state, then a message is sent toooutput, and hello runbook ends.</span></span>  <span data-ttu-id="8e56f-223">Als dat niet het geval is, klikt u vervolgens **Start-AzureVM** of **Stop-AzureVM** gebruikte tooattempt toostart of stop Hallo virtuele machine met Hallo resultaat van Hallo aanvraag opgeslagen tooa variabele is.</span><span class="sxs-lookup"><span data-stu-id="8e56f-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used tooattempt toostart or stop hello virtual machine with hello result of hello request stored tooa variable.</span></span>  <span data-ttu-id="8e56f-224">Een bericht vervolgens verzonden toooutput opgeven of Hallo aanvraag toostart of stoppen is verzonden.</span><span class="sxs-lookup"><span data-stu-id="8e56f-224">A message is then sent toooutput specifying whether hello request toostart or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e56f-225">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8e56f-225">Next steps</span></span>
* <span data-ttu-id="8e56f-226">Zie toolearn meer informatie over het werken met onderliggende runbooks [onderliggende runbooks in Azure Automation](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="8e56f-226">toolearn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="8e56f-227">informatie over toolearn uitvoer berichten tijdens de uitvoering van runbook en logboekregistratie toohelp oplossen, raadpleegt u [Runbook uitvoer en berichten in Azure Automation](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="8e56f-227">toolearn more about output messages during runbook execution and logging toohelp troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

