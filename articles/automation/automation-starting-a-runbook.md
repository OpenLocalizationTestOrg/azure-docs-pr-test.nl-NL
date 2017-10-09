---
title: een runbook in Azure Automation aaaStarting | Microsoft Docs
description: Geeft een overzicht van Hallo verschillende methoden die kunnen worden gebruikt toostart een runbook in Azure Automation en biedt details over het gebruik van beide hello Azure-portal en Windows PowerShell.
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
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="6e888-103">Een runbook starten in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="6e888-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="6e888-104">Hallo volgende tabel kunt u bepalen Hallo methode toostart een runbook in Azure Automation die het meest geschikte tooyour bepaalde scenario.</span><span class="sxs-lookup"><span data-stu-id="6e888-104">hello following table will help you determine hello method toostart a runbook in Azure Automation that is most suitable tooyour particular scenario.</span></span> <span data-ttu-id="6e888-105">Dit artikel bevat informatie over het starten van een runbook met hello Azure-portal en met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e888-105">This article includes details on starting a runbook with hello Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="6e888-106">Details op Hallo andere methoden beschikbaar zijn in andere documentatie die u vanaf Hallo onderstaande koppelingen openen kunt.</span><span class="sxs-lookup"><span data-stu-id="6e888-106">Details on hello other methods are provided in other documentation that you can access from hello links below.</span></span>

| <span data-ttu-id="6e888-107">**METHODE**</span><span class="sxs-lookup"><span data-stu-id="6e888-107">**METHOD**</span></span> | <span data-ttu-id="6e888-108">**KENMERKEN**</span><span class="sxs-lookup"><span data-stu-id="6e888-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="6e888-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6e888-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="6e888-110">Eenvoudigste methode met interactieve gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="6e888-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="6e888-111">Formulier tooprovide eenvoudige parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="6e888-111">Form tooprovide simple parameter values.</span></span><br> <li><span data-ttu-id="6e888-112">Taakstatus op eenvoudige wijze volgen.</span><span class="sxs-lookup"><span data-stu-id="6e888-112">Easily track job state.</span></span><br> <li><span data-ttu-id="6e888-113">De toegang wordt geverifieerd met aanmelding bij Azure.</span><span class="sxs-lookup"><span data-stu-id="6e888-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="6e888-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e888-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="6e888-115">Aanroepen vanuit de opdrachtregel met Windows PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="6e888-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="6e888-116">Geautomatiseerde oplossing met meerdere stappen kunnen worden opgenomen.</span><span class="sxs-lookup"><span data-stu-id="6e888-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="6e888-117">Aanvraag is geverifieerd met een certificaat of de OAuth-gebruiker principal / service principal.</span><span class="sxs-lookup"><span data-stu-id="6e888-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="6e888-118">Eenvoudige en complexe parameterwaarden opgeven.</span><span class="sxs-lookup"><span data-stu-id="6e888-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="6e888-119">Taakstatus bijhouden.</span><span class="sxs-lookup"><span data-stu-id="6e888-119">Track job state.</span></span><br> <li><span data-ttu-id="6e888-120">-Client vereist toosupport PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="6e888-120">Client required toosupport PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="6e888-121">Azure Automation-API</span><span class="sxs-lookup"><span data-stu-id="6e888-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="6e888-122">Meest flexibele methode, maar ook de meeste complex.</span><span class="sxs-lookup"><span data-stu-id="6e888-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="6e888-123">Aanroepen vanuit elke gewenste aangepaste code die HTTP-aanvragen kan maken.</span><span class="sxs-lookup"><span data-stu-id="6e888-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="6e888-124">Aanvraag geverifieerd met het certificaat of de Oauth-gebruiker principal / service principal.</span><span class="sxs-lookup"><span data-stu-id="6e888-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="6e888-125">Eenvoudige en complexe parameterwaarden opgeven.</span><span class="sxs-lookup"><span data-stu-id="6e888-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="6e888-126">Taakstatus bijhouden.</span><span class="sxs-lookup"><span data-stu-id="6e888-126">Track job state.</span></span> |
| [<span data-ttu-id="6e888-127">Webhooks.</span><span class="sxs-lookup"><span data-stu-id="6e888-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="6e888-128">Runbook starten vanuit één HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="6e888-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="6e888-129">Geverifieerd met beveiligingstoken in URL.</span><span class="sxs-lookup"><span data-stu-id="6e888-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="6e888-130">Client overschrijven niet parameterwaarden die zijn opgegeven wanneer webhook is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e888-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="6e888-131">Runbook kan één parameter die is gevuld met gegevens voor de HTTP-aanvraag Hallo kunt definiëren.</span><span class="sxs-lookup"><span data-stu-id="6e888-131">Runbook can define single parameter that is populated with hello HTTP request details.</span></span><br> <li><span data-ttu-id="6e888-132">Er is geen mogelijkheid tootrack taakstatus via webhook-URL.</span><span class="sxs-lookup"><span data-stu-id="6e888-132">No ability tootrack job state through webhook URL.</span></span> |
| [<span data-ttu-id="6e888-133">Reageren tooAzure waarschuwing</span><span class="sxs-lookup"><span data-stu-id="6e888-133">Respond tooAzure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="6e888-134">Een runbook start in antwoord tooAzure waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="6e888-134">Start a runbook in response tooAzure alert.</span></span><br> <li><span data-ttu-id="6e888-135">Configureer webhook voor het runbook en tooalert koppelen.</span><span class="sxs-lookup"><span data-stu-id="6e888-135">Configure webhook for runbook and link tooalert.</span></span><br> <li><span data-ttu-id="6e888-136">Geverifieerd met beveiligingstoken in URL.</span><span class="sxs-lookup"><span data-stu-id="6e888-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="6e888-137">Planning</span><span class="sxs-lookup"><span data-stu-id="6e888-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="6e888-138">Start runbook automatisch op elk uur, dagelijks, wekelijks of maandelijks schema.</span><span class="sxs-lookup"><span data-stu-id="6e888-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="6e888-139">Manipuleren planning via Azure portal, PowerShell-cmdlets of Azure-API.</span><span class="sxs-lookup"><span data-stu-id="6e888-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="6e888-140">Geef de parameter waarden toobe gebruikt met planning.</span><span class="sxs-lookup"><span data-stu-id="6e888-140">Provide parameter values toobe used with schedule.</span></span> |
| [<span data-ttu-id="6e888-141">Vanuit een ander Runbook</span><span class="sxs-lookup"><span data-stu-id="6e888-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="6e888-142">Een runbook gebruiken als een activiteit in een ander runbook.</span><span class="sxs-lookup"><span data-stu-id="6e888-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="6e888-143">Dit is handig voor functionaliteit die wordt gebruikt door meerdere runbooks.</span><span class="sxs-lookup"><span data-stu-id="6e888-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="6e888-144">Geef de parameter waarden toochild runbook en gebruik van uitvoer in bovenliggend runbook.</span><span class="sxs-lookup"><span data-stu-id="6e888-144">Provide parameter values toochild runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="6e888-145">Hallo volgende afbeelding ziet u gedetailleerde stapsgewijze procedure geleid in Hallo levenscyclus van een runbook.</span><span class="sxs-lookup"><span data-stu-id="6e888-145">hello following image illustrates detailed step-by-step process in hello life cycle of a runbook.</span></span> <span data-ttu-id="6e888-146">Dit omvat verschillende manieren een runbook wordt gestart in Azure Automation, die vereist zijn voor hybride Runbook Worker tooexecute Azure Automation-runbooks en -interacties tussen de verschillende onderdelen.</span><span class="sxs-lookup"><span data-stu-id="6e888-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker tooexecute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="6e888-147">toolearn over het uitvoeren van Automation-runbooks in uw datacenter te verwijzen[hybride runbook workers](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="6e888-147">toolearn about executing Automation runbooks in your datacenter, refer too[hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Runbook-architectuur](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="6e888-149">Een runbook starten met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6e888-149">Starting a runbook with hello Azure portal</span></span>
1. <span data-ttu-id="6e888-150">Selecteer in de Azure-portal hello, **Automation** en klik vervolgens op Hallo-naam van een automation-account.</span><span class="sxs-lookup"><span data-stu-id="6e888-150">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="6e888-151">Selecteer op de Hub-menu Hallo **Runbooks**.</span><span class="sxs-lookup"><span data-stu-id="6e888-151">On hello Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="6e888-152">Op Hallo **Runbooks** blade, selecteert u een runbook en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="6e888-152">On hello **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="6e888-153">Als Hallo runbook parameters heeft, kunt u zich na vragen aan gebruiker tooprovide waarden met een tekstvak voor elke parameter.</span><span class="sxs-lookup"><span data-stu-id="6e888-153">If hello runbook has parameters, you will be prompted tooprovide values with a text box for each parameter.</span></span> <span data-ttu-id="6e888-154">Zie [Runbookparameters](#Runbook-parameters) hieronder voor meer informatie over parameters.</span><span class="sxs-lookup"><span data-stu-id="6e888-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="6e888-155">Op Hallo **taak** blade kunt u Hallo status van de runbooktaak Hallo bekijken.</span><span class="sxs-lookup"><span data-stu-id="6e888-155">On hello **Job** blade, you can view hello status of hello runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="6e888-156">Een runbook starten met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e888-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="6e888-157">U kunt Hallo [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart een runbook met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e888-157">You can use hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a runbook with Windows PowerShell.</span></span> <span data-ttu-id="6e888-158">Hallo volgende voorbeeldcode wordt een runbook gestart naam Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="6e888-158">hello following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="6e888-159">Retourneert een taak start AzureRmAutomationRunbook object waarmee u tootrack de status ervan kunt zodra Hallo runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="6e888-159">Start-AzureRmAutomationRunbook returns a job object that you can use tootrack its status once hello runbook is started.</span></span> <span data-ttu-id="6e888-160">U kunt dit object met [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine Hallo status van Hallo taak en [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget uitvoer ervan weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6e888-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello status of hello job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget its output.</span></span> <span data-ttu-id="6e888-161">Hallo volgende voorbeeldcode wordt een runbook met de naam Test-Runbook, wordt er gewacht totdat deze is voltooid en vervolgens de uitvoer wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="6e888-161">hello following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

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

<span data-ttu-id="6e888-162">Als Hallo runbook parameters vereist, dan u als opgeven moet een [hashtabel](http://technet.microsoft.com/library/hh847780.aspx) waarbij Hallo-sleutel van Hallo hashtabel overeenkomt met Hallo parameternaam en Hallo-waarde is de waarde van de Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="6e888-162">If hello runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key of hello hashtable matches hello parameter name and hello value is hello parameter value.</span></span> <span data-ttu-id="6e888-163">Hallo volgende voorbeeld ziet u hoe toostart een runbook met twee Reeksparameters met de naam FirstName en LastName, een geheel getal met de naam RepeatCount en een Boole-parameter met de naam Show.</span><span class="sxs-lookup"><span data-stu-id="6e888-163">hello following example shows how toostart a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="6e888-164">Zie voor meer informatie over parameters [Runbookparameters](#Runbook-parameters) hieronder.</span><span class="sxs-lookup"><span data-stu-id="6e888-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="6e888-165">Runbook-parameters</span><span class="sxs-lookup"><span data-stu-id="6e888-165">Runbook parameters</span></span>
<span data-ttu-id="6e888-166">Wanneer u een runbook vanuit hello Azure Portal of met Windows PowerShell start, Hallo instructie verzonden via hello Azure Automation-webservice.</span><span class="sxs-lookup"><span data-stu-id="6e888-166">When you start a runbook from hello Azure Portal or Windows PowerShell, hello instruction is sent through hello Azure Automation web service.</span></span> <span data-ttu-id="6e888-167">Deze service biedt geen ondersteuning voor parameters met complexe gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="6e888-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="6e888-168">Als u een waarde tooprovide voor een complexe parameter moet, wordt u deze inline vanuit een ander runbook aanroepen moet zoals beschreven in [onderliggende runbooks in Azure Automation](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="6e888-168">If you need tooprovide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="6e888-169">Hello Azure Automation-webservice biedt speciale functionaliteit voor parameters die bepaalde gegevenstypen gebruiken, zoals beschreven in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="6e888-169">hello Azure Automation web service will provide special functionality for parameters using certain data types as described in hello following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="6e888-170">Naamwaarden</span><span class="sxs-lookup"><span data-stu-id="6e888-170">Named values</span></span>
<span data-ttu-id="6e888-171">Als Hallo parameter gegevenstype [object] is, wordt u Hallo volgende JSON-indeling toosend een lijst met benoemde waarden kunt gebruiken: *{Name1: 'Value1', Naam2: 'Waarde2', Name3: 'Value3'}*.</span><span class="sxs-lookup"><span data-stu-id="6e888-171">If hello parameter is data type [object], then you can use hello following JSON format toosend it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="6e888-172">Deze waarden moeten eenvoudige typen.</span><span class="sxs-lookup"><span data-stu-id="6e888-172">These values must be simple types.</span></span> <span data-ttu-id="6e888-173">Hallo runbook ontvangt Hallo parameter als een [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) met eigenschappen die met de naam value tooeach overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="6e888-173">hello runbook will receive hello parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond tooeach named value.</span></span>

<span data-ttu-id="6e888-174">Overweeg het volgende testrunbook dat een parameter met de naam van de gebruiker accepteert Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e888-174">Consider hello following test runbook that accepts a parameter called user.</span></span>

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

<span data-ttu-id="6e888-175">Hallo kan volgende tekst worden gebruikt voor de parameter user Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e888-175">hello following text could be used for hello user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="6e888-176">Dit resulteert in Hallo na uitvoer.</span><span class="sxs-lookup"><span data-stu-id="6e888-176">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="6e888-177">Matrices</span><span class="sxs-lookup"><span data-stu-id="6e888-177">Arrays</span></span>
<span data-ttu-id="6e888-178">Als Hallo-parameter een matrix zoals [array is] of [string []], kunt u Hallo volgende JSON-indeling toosend deze een lijst met waarden: *[Value1, Value2, Value3]*.</span><span class="sxs-lookup"><span data-stu-id="6e888-178">If hello parameter is an array such as [array] or [string[]], then you can use hello following JSON format toosend it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="6e888-179">Deze waarden moeten eenvoudige typen.</span><span class="sxs-lookup"><span data-stu-id="6e888-179">These values must be simple types.</span></span>

<span data-ttu-id="6e888-180">Overweeg het volgende testrunbook dat een parameter met de naam accepteert Hallo *gebruiker*.</span><span class="sxs-lookup"><span data-stu-id="6e888-180">Consider hello following test runbook that accepts a parameter called *user*.</span></span>

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

<span data-ttu-id="6e888-181">Hallo kan volgende tekst worden gebruikt voor de parameter user Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e888-181">hello following text could be used for hello user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="6e888-182">Dit resulteert in Hallo na uitvoer.</span><span class="sxs-lookup"><span data-stu-id="6e888-182">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="6e888-183">Referenties</span><span class="sxs-lookup"><span data-stu-id="6e888-183">Credentials</span></span>
<span data-ttu-id="6e888-184">Als de parameter Hallo gegevenstype **PSCredential**, kunt u Hallo-naam van een Azure Automation opgeven [referentieasset](automation-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="6e888-184">If hello parameter is data type **PSCredential**, then you can provide hello name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="6e888-185">Hallo runbook haalt Hallo-referentie met Hallo-naam die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="6e888-185">hello runbook will retrieve hello credential with hello name that you specify.</span></span>

<span data-ttu-id="6e888-186">Overweeg het volgende testrunbook dat een parameter met de naam van de referentie accepteert Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e888-186">Consider hello following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="6e888-187">Hallo volgende tekst kan worden gebruikt voor Hallo gebruiker parameter mits het referentie-element *mijn referentie*.</span><span class="sxs-lookup"><span data-stu-id="6e888-187">hello following text could be used for hello user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="6e888-188">Ervan uitgaand dat Hallo gebruikersnaam in het Hallo-referentie is *jsmith*, resulteert dit in de volgende uitvoer Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e888-188">Assuming hello username in hello credential was *jsmith*, this results in hello following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="6e888-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e888-189">Next steps</span></span>
* <span data-ttu-id="6e888-190">Hallo runbook-architectuur in het huidige artikel biedt een overzicht van het beheer van bronnen van de runbooks in Azure en on-premises met Hallo Hybrid Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="6e888-190">hello runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with hello Hybrid Runbook Worker.</span></span>  <span data-ttu-id="6e888-191">toolearn over het uitvoeren van Automation-runbooks in uw datacenter te verwijzen[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="6e888-191">toolearn about executing Automation runbooks in your datacenter, refer too[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="6e888-192">toolearn meer informatie over Hallo modulaire runbooks toobe gebruikt door andere runbooks voor specifieke of algemene functies, maken te verwijzen[onderliggende Runbooks](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="6e888-192">toolearn more about hello creating modular runbooks toobe used by other runbooks for specific or common functions, refer too[Child Runbooks](automation-child-runbooks.md).</span></span>

