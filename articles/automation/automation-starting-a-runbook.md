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
# <a name="starting-a-runbook-in-azure-automation"></a>Een runbook starten in Azure Automation
Hallo volgende tabel kunt u bepalen Hallo methode toostart een runbook in Azure Automation die het meest geschikte tooyour bepaalde scenario. Dit artikel bevat informatie over het starten van een runbook met hello Azure-portal en met Windows PowerShell. Details op Hallo andere methoden beschikbaar zijn in andere documentatie die u vanaf Hallo onderstaande koppelingen openen kunt.

| **METHODE** | **KENMERKEN** |
| --- | --- |
| [Azure Portal](#starting-a-runbook-with-the-azure-portal) |<li>Eenvoudigste methode met interactieve gebruikersinterface.<br> <li>Formulier tooprovide eenvoudige parameterwaarden.<br> <li>Taakstatus op eenvoudige wijze volgen.<br> <li>De toegang wordt geverifieerd met aanmelding bij Azure. |
| [Windows PowerShell](https://msdn.microsoft.com/library/dn690259.aspx) |<li>Aanroepen vanuit de opdrachtregel met Windows PowerShell-cmdlets.<br> <li>Geautomatiseerde oplossing met meerdere stappen kunnen worden opgenomen.<br> <li>Aanvraag is geverifieerd met een certificaat of de OAuth-gebruiker principal / service principal.<br> <li>Eenvoudige en complexe parameterwaarden opgeven.<br> <li>Taakstatus bijhouden.<br> <li>-Client vereist toosupport PowerShell-cmdlets. |
| [Azure Automation-API](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li>Meest flexibele methode, maar ook de meeste complex.<br> <li>Aanroepen vanuit elke gewenste aangepaste code die HTTP-aanvragen kan maken.<br> <li>Aanvraag geverifieerd met het certificaat of de Oauth-gebruiker principal / service principal.<br> <li>Eenvoudige en complexe parameterwaarden opgeven.<br> <li>Taakstatus bijhouden. |
| [Webhooks.](automation-webhooks.md) |<li>Runbook starten vanuit één HTTP-aanvraag.<br> <li>Geverifieerd met beveiligingstoken in URL.<br> <li>Client overschrijven niet parameterwaarden die zijn opgegeven wanneer webhook is gemaakt. Runbook kan één parameter die is gevuld met gegevens voor de HTTP-aanvraag Hallo kunt definiëren.<br> <li>Er is geen mogelijkheid tootrack taakstatus via webhook-URL. |
| [Reageren tooAzure waarschuwing](../log-analytics/log-analytics-alerts.md) |<li>Een runbook start in antwoord tooAzure waarschuwing.<br> <li>Configureer webhook voor het runbook en tooalert koppelen.<br> <li>Geverifieerd met beveiligingstoken in URL. |
| [Planning](automation-schedules.md) |<li>Start runbook automatisch op elk uur, dagelijks, wekelijks of maandelijks schema.<br> <li>Manipuleren planning via Azure portal, PowerShell-cmdlets of Azure-API.<br> <li>Geef de parameter waarden toobe gebruikt met planning. |
| [Vanuit een ander Runbook](automation-child-runbooks.md) |<li>Een runbook gebruiken als een activiteit in een ander runbook.<br> <li>Dit is handig voor functionaliteit die wordt gebruikt door meerdere runbooks.<br> <li>Geef de parameter waarden toochild runbook en gebruik van uitvoer in bovenliggend runbook. |

Hallo volgende afbeelding ziet u gedetailleerde stapsgewijze procedure geleid in Hallo levenscyclus van een runbook. Dit omvat verschillende manieren een runbook wordt gestart in Azure Automation, die vereist zijn voor hybride Runbook Worker tooexecute Azure Automation-runbooks en -interacties tussen de verschillende onderdelen. toolearn over het uitvoeren van Automation-runbooks in uw datacenter te verwijzen[hybride runbook workers](automation-hybrid-runbook-worker.md)

![Runbook-architectuur](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a>Een runbook starten met hello Azure-portal
1. Selecteer in de Azure-portal hello, **Automation** en klik vervolgens op Hallo-naam van een automation-account.
2. Selecteer op de Hub-menu Hallo **Runbooks**.
3. Op Hallo **Runbooks** blade, selecteert u een runbook en klik vervolgens op **Start**.
4. Als Hallo runbook parameters heeft, kunt u zich na vragen aan gebruiker tooprovide waarden met een tekstvak voor elke parameter. Zie [Runbookparameters](#Runbook-parameters) hieronder voor meer informatie over parameters.
5. Op Hallo **taak** blade kunt u Hallo status van de runbooktaak Hallo bekijken.

## <a name="starting-a-runbook-with-windows-powershell"></a>Een runbook starten met Windows PowerShell
U kunt Hallo [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart een runbook met Windows PowerShell. Hallo volgende voorbeeldcode wordt een runbook gestart naam Test-Runbook.

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

Retourneert een taak start AzureRmAutomationRunbook object waarmee u tootrack de status ervan kunt zodra Hallo runbook wordt gestart. U kunt dit object met [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine Hallo status van Hallo taak en [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget uitvoer ervan weergegeven. Hallo volgende voorbeeldcode wordt een runbook met de naam Test-Runbook, wordt er gewacht totdat deze is voltooid en vervolgens de uitvoer wordt gestart.

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

Als Hallo runbook parameters vereist, dan u als opgeven moet een [hashtabel](http://technet.microsoft.com/library/hh847780.aspx) waarbij Hallo-sleutel van Hallo hashtabel overeenkomt met Hallo parameternaam en Hallo-waarde is de waarde van de Hallo-parameter. Hallo volgende voorbeeld ziet u hoe toostart een runbook met twee Reeksparameters met de naam FirstName en LastName, een geheel getal met de naam RepeatCount en een Boole-parameter met de naam Show. Zie voor meer informatie over parameters [Runbookparameters](#Runbook-parameters) hieronder.

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a>Runbook-parameters
Wanneer u een runbook vanuit hello Azure Portal of met Windows PowerShell start, Hallo instructie verzonden via hello Azure Automation-webservice. Deze service biedt geen ondersteuning voor parameters met complexe gegevenstypen. Als u een waarde tooprovide voor een complexe parameter moet, wordt u deze inline vanuit een ander runbook aanroepen moet zoals beschreven in [onderliggende runbooks in Azure Automation](automation-child-runbooks.md).

Hello Azure Automation-webservice biedt speciale functionaliteit voor parameters die bepaalde gegevenstypen gebruiken, zoals beschreven in Hallo uit te voeren.

### <a name="named-values"></a>Naamwaarden
Als Hallo parameter gegevenstype [object] is, wordt u Hallo volgende JSON-indeling toosend een lijst met benoemde waarden kunt gebruiken: *{Name1: 'Value1', Naam2: 'Waarde2', Name3: 'Value3'}*. Deze waarden moeten eenvoudige typen. Hallo runbook ontvangt Hallo parameter als een [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) met eigenschappen die met de naam value tooeach overeenkomen.

Overweeg het volgende testrunbook dat een parameter met de naam van de gebruiker accepteert Hallo.

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

Hallo kan volgende tekst worden gebruikt voor de parameter user Hallo.

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

Dit resulteert in Hallo na uitvoer.

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a>Matrices
Als Hallo-parameter een matrix zoals [array is] of [string []], kunt u Hallo volgende JSON-indeling toosend deze een lijst met waarden: *[Value1, Value2, Value3]*. Deze waarden moeten eenvoudige typen.

Overweeg het volgende testrunbook dat een parameter met de naam accepteert Hallo *gebruiker*.

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

Hallo kan volgende tekst worden gebruikt voor de parameter user Hallo.

```
["Joe","Smith",2,true]
```

Dit resulteert in Hallo na uitvoer.

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a>Referenties
Als de parameter Hallo gegevenstype **PSCredential**, kunt u Hallo-naam van een Azure Automation opgeven [referentieasset](automation-credentials.md). Hallo runbook haalt Hallo-referentie met Hallo-naam die u opgeeft.

Overweeg het volgende testrunbook dat een parameter met de naam van de referentie accepteert Hallo.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

Hallo volgende tekst kan worden gebruikt voor Hallo gebruiker parameter mits het referentie-element *mijn referentie*.

```
My Credential
```

Ervan uitgaand dat Hallo gebruikersnaam in het Hallo-referentie is *jsmith*, resulteert dit in de volgende uitvoer Hallo.

```
jsmith
```

## <a name="next-steps"></a>Volgende stappen
* Hallo runbook-architectuur in het huidige artikel biedt een overzicht van het beheer van bronnen van de runbooks in Azure en on-premises met Hallo Hybrid Runbook Worker.  toolearn over het uitvoeren van Automation-runbooks in uw datacenter te verwijzen[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).
* toolearn meer informatie over Hallo modulaire runbooks toobe gebruikt door andere runbooks voor specifieke of algemene functies, maken te verwijzen[onderliggende Runbooks](automation-child-runbooks.md).

