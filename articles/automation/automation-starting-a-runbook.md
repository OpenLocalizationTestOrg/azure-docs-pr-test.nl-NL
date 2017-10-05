---
title: Een runbook starten in Azure Automation | Microsoft Docs
description: Geeft een overzicht van de verschillende methoden die kunnen worden gebruikt voor het starten van een runbook in Azure Automation en biedt details over het gebruik van de Azure-portal en de Windows PowerShell.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 844831b63d5263987ed05370125fbe9f01913ab9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="f4c92-103">Een runbook starten in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f4c92-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="f4c92-104">De volgende tabel kunt u bepalen welke methode voor het starten van een runbook in Azure Automation die het meest geschikt is voor uw specifieke scenario.</span><span class="sxs-lookup"><span data-stu-id="f4c92-104">The following table will help you determine the method to start a runbook in Azure Automation that is most suitable to your particular scenario.</span></span> <span data-ttu-id="f4c92-105">Dit artikel bevat informatie over het starten van een runbook met de Azure-portal en met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f4c92-105">This article includes details on starting a runbook with the Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="f4c92-106">Meer informatie over de andere methoden beschikbaar in andere documentatie die u vanaf de onderstaande koppelingen openen kunt.</span><span class="sxs-lookup"><span data-stu-id="f4c92-106">Details on the other methods are provided in other documentation that you can access from the links below.</span></span>

| <span data-ttu-id="f4c92-107">**METHODE**</span><span class="sxs-lookup"><span data-stu-id="f4c92-107">**METHOD**</span></span> | <span data-ttu-id="f4c92-108">**KENMERKEN**</span><span class="sxs-lookup"><span data-stu-id="f4c92-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="f4c92-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f4c92-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="f4c92-110">Eenvoudigste methode met interactieve gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="f4c92-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="f4c92-111">Formulier eenvoudige parameterwaarden opgeven.</span><span class="sxs-lookup"><span data-stu-id="f4c92-111">Form to provide simple parameter values.</span></span><br> <li><span data-ttu-id="f4c92-112">Taakstatus op eenvoudige wijze volgen.</span><span class="sxs-lookup"><span data-stu-id="f4c92-112">Easily track job state.</span></span><br> <li><span data-ttu-id="f4c92-113">De toegang wordt geverifieerd met aanmelding bij Azure.</span><span class="sxs-lookup"><span data-stu-id="f4c92-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="f4c92-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4c92-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="f4c92-115">Aanroepen vanuit de opdrachtregel met Windows PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f4c92-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="f4c92-116">Geautomatiseerde oplossing met meerdere stappen kunnen worden opgenomen.</span><span class="sxs-lookup"><span data-stu-id="f4c92-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="f4c92-117">Aanvraag is geverifieerd met een certificaat of de OAuth-gebruiker principal / service principal.</span><span class="sxs-lookup"><span data-stu-id="f4c92-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="f4c92-118">Eenvoudige en complexe parameterwaarden opgeven.</span><span class="sxs-lookup"><span data-stu-id="f4c92-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="f4c92-119">Taakstatus bijhouden.</span><span class="sxs-lookup"><span data-stu-id="f4c92-119">Track job state.</span></span><br> <li><span data-ttu-id="f4c92-120">De client vereist ter ondersteuning van PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f4c92-120">Client required to support PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="f4c92-121">Azure Automation-API</span><span class="sxs-lookup"><span data-stu-id="f4c92-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="f4c92-122">Meest flexibele methode, maar ook de meeste complex.</span><span class="sxs-lookup"><span data-stu-id="f4c92-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="f4c92-123">Aanroepen vanuit elke gewenste aangepaste code die HTTP-aanvragen kan maken.</span><span class="sxs-lookup"><span data-stu-id="f4c92-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="f4c92-124">Aanvraag geverifieerd met het certificaat of de Oauth-gebruiker principal / service principal.</span><span class="sxs-lookup"><span data-stu-id="f4c92-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="f4c92-125">Eenvoudige en complexe parameterwaarden opgeven.</span><span class="sxs-lookup"><span data-stu-id="f4c92-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="f4c92-126">Taakstatus bijhouden.</span><span class="sxs-lookup"><span data-stu-id="f4c92-126">Track job state.</span></span> |
| [<span data-ttu-id="f4c92-127">Webhooks.</span><span class="sxs-lookup"><span data-stu-id="f4c92-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="f4c92-128">Runbook starten vanuit één HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="f4c92-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="f4c92-129">Geverifieerd met beveiligingstoken in URL.</span><span class="sxs-lookup"><span data-stu-id="f4c92-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="f4c92-130">Client overschrijven niet parameterwaarden die zijn opgegeven wanneer webhook is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f4c92-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="f4c92-131">Runbook kunt definiëren één parameter die is gevuld met de details van de HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="f4c92-131">Runbook can define single parameter that is populated with the HTTP request details.</span></span><br> <li><span data-ttu-id="f4c92-132">Er is geen mogelijkheid om bij te houden taakstatus via webhook-URL.</span><span class="sxs-lookup"><span data-stu-id="f4c92-132">No ability to track job state through webhook URL.</span></span> |
| [<span data-ttu-id="f4c92-133">Reageren op Azure waarschuwing</span><span class="sxs-lookup"><span data-stu-id="f4c92-133">Respond to Azure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="f4c92-134">Een runbook starten in reactie op Azure waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="f4c92-134">Start a runbook in response to Azure alert.</span></span><br> <li><span data-ttu-id="f4c92-135">Webhook voor runbook en een koppeling naar een waarschuwing configureren.</span><span class="sxs-lookup"><span data-stu-id="f4c92-135">Configure webhook for runbook and link to alert.</span></span><br> <li><span data-ttu-id="f4c92-136">Geverifieerd met beveiligingstoken in URL.</span><span class="sxs-lookup"><span data-stu-id="f4c92-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="f4c92-137">Planning</span><span class="sxs-lookup"><span data-stu-id="f4c92-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="f4c92-138">Start runbook automatisch op elk uur, dagelijks, wekelijks of maandelijks schema.</span><span class="sxs-lookup"><span data-stu-id="f4c92-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="f4c92-139">Manipuleren planning via Azure portal, PowerShell-cmdlets of Azure-API.</span><span class="sxs-lookup"><span data-stu-id="f4c92-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="f4c92-140">Parameterwaarden moet worden gebruikt met een planning opgeven.</span><span class="sxs-lookup"><span data-stu-id="f4c92-140">Provide parameter values to be used with schedule.</span></span> |
| [<span data-ttu-id="f4c92-141">Vanuit een ander Runbook</span><span class="sxs-lookup"><span data-stu-id="f4c92-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="f4c92-142">Een runbook gebruiken als een activiteit in een ander runbook.</span><span class="sxs-lookup"><span data-stu-id="f4c92-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="f4c92-143">Dit is handig voor functionaliteit die wordt gebruikt door meerdere runbooks.</span><span class="sxs-lookup"><span data-stu-id="f4c92-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="f4c92-144">Parameterwaarden voor onderliggend runbook opgeven en het gebruik van uitvoer in bovenliggende runbook.</span><span class="sxs-lookup"><span data-stu-id="f4c92-144">Provide parameter values to child runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="f4c92-145">De volgende afbeelding illustreert de gedetailleerde stapsgewijze proces in de levenscyclus van een runbook.</span><span class="sxs-lookup"><span data-stu-id="f4c92-145">The following image illustrates detailed step-by-step process in the life cycle of a runbook.</span></span> <span data-ttu-id="f4c92-146">Dit omvat verschillende manieren die een runbook wordt gestart in Azure Automation onderdelen vereist zijn voor hybride Runbook Worker Azure Automation-runbooks en interacties tussen de verschillende onderdelen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="f4c92-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker to execute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="f4c92-147">Raadpleeg voor meer informatie over het uitvoeren van Automation-runbooks in uw datacenter, [hybride runbook workers](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="f4c92-147">To learn about executing Automation runbooks in your datacenter, refer to [hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Runbook-architectuur](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-the-azure-portal"></a><span data-ttu-id="f4c92-149">Een runbook starten met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="f4c92-149">Starting a runbook with the Azure portal</span></span>
1. <span data-ttu-id="f4c92-150">Selecteer in de Azure-portal **Automation** en klik vervolgens op de naam van een automation-account.</span><span class="sxs-lookup"><span data-stu-id="f4c92-150">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="f4c92-151">Selecteer in het menu Hub **Runbooks**.</span><span class="sxs-lookup"><span data-stu-id="f4c92-151">On the Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="f4c92-152">Op de **Runbooks** blade, selecteert u een runbook en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="f4c92-152">On the **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="f4c92-153">Als het runbook parameters heeft, wordt u gevraagd waarden met een tekstvak voor elke parameter opgeven.</span><span class="sxs-lookup"><span data-stu-id="f4c92-153">If the runbook has parameters, you will be prompted to provide values with a text box for each parameter.</span></span> <span data-ttu-id="f4c92-154">Zie [Runbookparameters](#Runbook-parameters) hieronder voor meer informatie over parameters.</span><span class="sxs-lookup"><span data-stu-id="f4c92-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="f4c92-155">Op de **taak** blade kunt u de status van de runbooktaak weergeven.</span><span class="sxs-lookup"><span data-stu-id="f4c92-155">On the **Job** blade, you can view the status of the runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="f4c92-156">Een runbook starten met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4c92-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="f4c92-157">U kunt de [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) een runbook starten met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f4c92-157">You can use the [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a runbook with Windows PowerShell.</span></span> <span data-ttu-id="f4c92-158">De volgende voorbeeldcode wordt een runbook met de naam Test-Runbook gestart.</span><span class="sxs-lookup"><span data-stu-id="f4c92-158">The following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="f4c92-159">Start AzureRmAutomationRunbook retourneert een taakobject dat u de status ervan bijhouden kunt zodra het runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="f4c92-159">Start-AzureRmAutomationRunbook returns a job object that you can use to track its status once the runbook is started.</span></span> <span data-ttu-id="f4c92-160">U kunt dit object met [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) om te bepalen van de status van de taak en [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) ophalen van de uitvoer ervan weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f4c92-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) to determine the status of the job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) to get its output.</span></span> <span data-ttu-id="f4c92-161">De volgende voorbeeldcode wordt gestart van een runbook met de naam Test-Runbook, wordt er gewacht totdat deze is voltooid en vervolgens de uitvoer ervan weergegeven wordt.</span><span class="sxs-lookup"><span data-stu-id="f4c92-161">The following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

<span data-ttu-id="f4c92-162">Als het runbook parameters vereist, dan u als opgeven moet een [hashtabel](http://technet.microsoft.com/library/hh847780.aspx) waar de sleutel van de hashtabel overeenkomt met de parameternaam van de en de waarde is de waarde van parameter.</span><span class="sxs-lookup"><span data-stu-id="f4c92-162">If the runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key of the hashtable matches the parameter name and the value is the parameter value.</span></span> <span data-ttu-id="f4c92-163">Het volgende voorbeeld ziet hoe u een runbook met twee Reeksparameters met de naam FirstName en LastName, een geheel getal met de naam RepeatCount en een Boole-parameter met de naam Show start.</span><span class="sxs-lookup"><span data-stu-id="f4c92-163">The following example shows how to start a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="f4c92-164">Zie voor meer informatie over parameters [Runbookparameters](#Runbook-parameters) hieronder.</span><span class="sxs-lookup"><span data-stu-id="f4c92-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="f4c92-165">Runbook-parameters</span><span class="sxs-lookup"><span data-stu-id="f4c92-165">Runbook parameters</span></span>
<span data-ttu-id="f4c92-166">Wanneer u een runbook vanuit de Azure Portal of de Windows PowerShell start, wordt de instructie verzonden via de Azure Automation-webservice.</span><span class="sxs-lookup"><span data-stu-id="f4c92-166">When you start a runbook from the Azure Portal or Windows PowerShell, the instruction is sent through the Azure Automation web service.</span></span> <span data-ttu-id="f4c92-167">Deze service biedt geen ondersteuning voor parameters met complexe gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="f4c92-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="f4c92-168">Als u moet een waarde opgeven voor een complexe parameter, moet u deze inline vanuit een ander runbook aanroepen moet zoals beschreven in [onderliggende runbooks in Azure Automation](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="f4c92-168">If you need to provide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="f4c92-169">De webservice Azure Automation biedt speciale functionaliteit voor parameters die bepaalde gegevenstypen zoals beschreven in de volgende secties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f4c92-169">The Azure Automation web service will provide special functionality for parameters using certain data types as described in the following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="f4c92-170">Naamwaarden</span><span class="sxs-lookup"><span data-stu-id="f4c92-170">Named values</span></span>
<span data-ttu-id="f4c92-171">Als de parameter gegevenstype [object] is, dan kunt u de volgende JSON-indeling te verzenden in een lijst met naamwaarden: *{Name1: 'Value1', Naam2: 'Waarde2', Name3: 'Value3'}*.</span><span class="sxs-lookup"><span data-stu-id="f4c92-171">If the parameter is data type [object], then you can use the following JSON format to send it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="f4c92-172">Deze waarden moeten eenvoudige typen.</span><span class="sxs-lookup"><span data-stu-id="f4c92-172">These values must be simple types.</span></span> <span data-ttu-id="f4c92-173">Het runbook ontvangt de parameter als een [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) met eigenschappen die met elke benoemde waarde overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="f4c92-173">The runbook will receive the parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond to each named value.</span></span>

<span data-ttu-id="f4c92-174">Houd rekening met het volgende testrunbook dat een parameter met de naam van de gebruiker accepteert.</span><span class="sxs-lookup"><span data-stu-id="f4c92-174">Consider the following test runbook that accepts a parameter called user.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

<span data-ttu-id="f4c92-175">De volgende tekst kan worden gebruikt voor de parameter user.</span><span class="sxs-lookup"><span data-stu-id="f4c92-175">The following text could be used for the user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="f4c92-176">Dit resulteert in de volgende uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f4c92-176">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="f4c92-177">Matrices</span><span class="sxs-lookup"><span data-stu-id="f4c92-177">Arrays</span></span>
<span data-ttu-id="f4c92-178">Als de parameter een matrix zoals [array is] of [string []], kunt u de volgende JSON-indeling gebruiken om te verzenden in een lijst met waarden: *[Value1, Value2, Value3]*.</span><span class="sxs-lookup"><span data-stu-id="f4c92-178">If the parameter is an array such as [array] or [string[]], then you can use the following JSON format to send it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="f4c92-179">Deze waarden moeten eenvoudige typen.</span><span class="sxs-lookup"><span data-stu-id="f4c92-179">These values must be simple types.</span></span>

<span data-ttu-id="f4c92-180">Houd rekening met het volgende testrunbook dat een parameter met de naam accepteert *gebruiker*.</span><span class="sxs-lookup"><span data-stu-id="f4c92-180">Consider the following test runbook that accepts a parameter called *user*.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

<span data-ttu-id="f4c92-181">De volgende tekst kan worden gebruikt voor de parameter user.</span><span class="sxs-lookup"><span data-stu-id="f4c92-181">The following text could be used for the user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="f4c92-182">Dit resulteert in de volgende uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f4c92-182">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="f4c92-183">Referenties</span><span class="sxs-lookup"><span data-stu-id="f4c92-183">Credentials</span></span>
<span data-ttu-id="f4c92-184">Als de parameter gegevenstype **PSCredential**, kunt u de naam van een Azure Automation opgeven [referentieasset](automation-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="f4c92-184">If the parameter is data type **PSCredential**, then you can provide the name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="f4c92-185">Het runbook haalt de referentie met de naam die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="f4c92-185">The runbook will retrieve the credential with the name that you specify.</span></span>

<span data-ttu-id="f4c92-186">Houd rekening met het volgende testrunbook dat een parameter met de naam van de referentie accepteert.</span><span class="sxs-lookup"><span data-stu-id="f4c92-186">Consider the following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="f4c92-187">De volgende tekst kan worden gebruikt voor de gebruiker parameter mits het referentie-element *mijn referentie*.</span><span class="sxs-lookup"><span data-stu-id="f4c92-187">The following text could be used for the user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="f4c92-188">Als de gebruikersnaam in de referentie is *jsmith*, resulteert dit in de volgende uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f4c92-188">Assuming the username in the credential was *jsmith*, this results in the following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="f4c92-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f4c92-189">Next steps</span></span>
* <span data-ttu-id="f4c92-190">De runbook-architectuur in het huidige artikel biedt een overzicht van het beheer van bronnen van de runbooks in Azure en on-premises met de hybride Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="f4c92-190">The runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with the Hybrid Runbook Worker.</span></span>  <span data-ttu-id="f4c92-191">Raadpleeg voor meer informatie over het uitvoeren van Automation-runbooks in uw datacenter, [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="f4c92-191">To learn about executing Automation runbooks in your datacenter, refer to [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="f4c92-192">Raadpleeg voor meer informatie over het maken, modulaire runbooks moet worden gebruikt door andere runbooks voor specifieke of algemene functies [onderliggende Runbooks](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="f4c92-192">To learn more about the creating modular runbooks to be used by other runbooks for specific or common functions, refer to [Child Runbooks](automation-child-runbooks.md).</span></span>

