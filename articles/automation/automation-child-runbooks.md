---
title: aaaChild runbooks in Azure Automation | Microsoft Docs
description: Beschrijft de verschillende methoden voor het starten van een runbook in Azure Automation vanuit een ander runbook en delen van gegevens tussen deze Hallo.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 919887b9-43e2-4c16-883c-f81807fe37db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d3d06818d344b565d53cc4f4705b41dcfcf9a376
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="child-runbooks-in-azure-automation"></a>Onderliggende runbooks in Azure Automation
Het is een best practice in Azure Automation toowrite herbruikbare, modulaire runbooks met een aparte functie die kan worden gebruikt door andere runbooks. Een bovenliggend runbook roept vaak een of meer onderliggende runbooks functionaliteit tooperform vereist. Er zijn twee manieren toocall een onderliggend runbook en elke manier kent duidelijke verschillen die u moet begrijpen zodat u kunt bepalen wat de beste optie voor uw verschillende scenario's.

## <a name="invoking-a-child-runbook-using-inline-execution"></a>Aanroepen van een onderliggend runbook met inline-uitvoering
tooinvoke een runbook inline vanuit een ander runbook u Hallo-naam van Hallo runbook gebruiken en geef waarden op voor de parameters precies zoals wanneer u een activiteit of cmdlet.  Alle runbooks in dezelfde Automation-account Hallo beschikbaar tooall anderen toobe op deze manier gebruikt zijn. Hallo bovenliggend runbook wacht Hallo onderliggend runbook toocomplete voordat u de volgende regel toohello verplaatst, en eventuele uitvoer wordt rechtstreeks toohello bovenliggende geretourneerd.

Als u een runbook inline aanroept, voert deze Hallo dezelfde taak als Hallo bovenliggende runbook. Er zijn geen vermelding in de taakgeschiedenis Hallo van Hallo onderliggend runbook dat is uitgevoerd. Eventuele uitzonderingen en eventuele Stroomuitvoer van Hallo onderliggend runbook worden gekoppeld met bovenliggende Hallo. Dit resulteert in minder taken en zorgt ervoor dat ze gemakkelijker tootrack en tootroubleshoot omdat eventuele uitzonderingen worden veroorzaakt door Hallo onderliggend runbook en een van de Stroomuitvoer zijn gekoppeld aan Hallo bovenliggende taak.

Wanneer een runbook wordt gepubliceerd, moet alle onderliggende runbooks die daardoor worden aangeroepen al zijn gepubliceerd. Dit is omdat Azure Automation een koppeling met onderliggende runbooks maakt wanneer een runbook wordt gecompileerd. Als ze niet, Hallo bovenliggend runbook toopublish correct wordt weergegeven, maar wordt een uitzondering gegenereerd wanneer deze wordt gestart. Als dit gebeurt, kunt u Hallo bovenliggend runbook in de volgorde tooproperly verwijzing Hallo onderliggende runbooks opnieuw publiceren. U hoeft geen toorepublish Hallo bovenliggend runbook als een Hallo onderliggende runbooks is gewijzigd, omdat het Hallo-koppeling wordt al zijn gemaakt.

Hallo-parameters van een onderliggend runbook dat inline wordt aangeroepen elk gegevenstype met inbegrip van complexe objecten kunnen worden en er is geen [JSON-serialisatie](automation-starting-a-runbook.md#runbook-parameters) omdat er bij u Hallo runbook start met behulp hello Azure Management Portal of met Hallo De cmdlet start-AzureRmAutomationRunbook.

### <a name="runbook-types"></a>Runbooktypen
Welke typen kunnen bellen elkaar:

* Een [PowerShell-runbook](automation-runbook-types.md#powershell-runbooks) en [grafische runbooks](automation-runbook-types.md#graphical-runbooks) elke andere inline (beide zijn op basis van PowerShell) kunt aanroepen.
* Een [PowerShell Workflow-runbook](automation-runbook-types.md#powershell-workflow-runbooks) en grafische PowerShell Workflow-runbooks, kunnen elke andere inline (beide zijn op basis van PowerShell-werkstroom) aangeroepen.
* Hallo PowerShell-typen en Hallo die PowerShell Workflow typen elkaar inline kan niet worden aangeroepen en Start AzureRmAutomationRunbook moet gebruiken.

Wanneer volgorde zaak wordt gepubliceerd:

* Hallo publiceren volgorde van runbooks alleen belangrijk is voor de PowerShell-werkstromen en grafische PowerShell Workflow-runbooks.

Wanneer u een grafisch of PowerShell-werkstroom onderliggend runbook met inline-uitvoering aanroept, u alleen Hallo-naam van Hallo runbook gebruiken.  Wanneer u een PowerShell-onderliggend runbook aanroepen, moet u dezelfde naam hebben als voorafgegaan *.\\*  toospecify die Hallo script bevindt zich in de lokale directory Hallo. 

### <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld wordt een onderliggend testrunbook dat drie parameters, een complex object, een geheel getal en een Boolean-waarde accepteert aangeroepen. Hallo-uitvoer van Hallo onderliggend runbook is tooa variabele worden toegewezen.  In dit geval is Hallo onderliggend runbook een PowerShell Workflow-runbook

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true

Hieronder vindt u Hallo hetzelfde voorbeeld met een PowerShell-runbook als onderliggende hello.

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true


## <a name="starting-a-child-runbook-using-cmdlet"></a>Een onderliggend runbook met behulp van de cmdlet starten
U kunt Hallo [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) cmdlet toostart een runbook, zoals beschreven in [toostart een runbook met Windows PowerShell](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell). Er zijn twee modi voor deze cmdlet.  Hallo cmdlet retourneert Hallo taak-id in één modus zodra Hallo onderliggende taak is gemaakt voor Hallo onderliggend runbook.  Hallo in andere modus, waarbij u inschakelen door te geven Hallo **-wacht** parameter Hallo cmdlet gewacht tot Hallo onderliggende taak is voltooid en retourneert Hallo uitvoer van Hallo onderliggend runbook.

Hallo-taak van een onderliggend runbook dat is gestart met een cmdlet wordt uitgevoerd in een afzonderlijke taak van Hallo bovenliggende runbook. Dit resulteert in meer taken dan Hallo runbook inline wordt aangeroepen en maakt ze moeilijker tootrack. Hallo bovenliggende kan meerdere onderliggende runbooks asynchroon starten zonder te wachten op voor elke toocomplete. Voor dezelfde soort parallelle uitvoering Hallo onderliggende runbooks inline aanroepen, Hallo bovenliggend runbook moet toouse hello [parallelle sleutelwoord](automation-powershell-workflow.md#parallel-processing).

Parameters voor een onderliggend runbook dat is gestart met een cmdlet worden opgegeven als hashtabel, zoals beschreven in [Runbookparameters](automation-starting-a-runbook.md#runbook-parameters). Alleen eenvoudige gegevenstypen kunnen worden gebruikt. Als Hallo runbook een parameter met een complex gegevenstype heeft, moet klikt u vervolgens het worden aangeroepen inline.

### <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld wordt gestart een onderliggend runbook met parameters en vervolgens wacht toocomplete met Hallo Start AzureRmAutomationRunbook-parameter wacht. Zodra voltooid, wordt de uitvoer van Hallo onderliggend runbook verzameld.

    $params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true} 
    $joboutput = Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-ChildRunbook" -ResourceGroupName "LabRG" –Parameters $params –wait


## <a name="comparison-of-methods-for-calling-a-child-runbook"></a>Vergelijking van methoden voor het aanroepen van een onderliggend runbook
Hallo volgende tabel ziet u Hallo verschillen tussen Hallo twee methoden voor het aanroepen van een runbook vanuit een ander runbook.

|  | Inline | Cmdlet |
|:--- |:--- |:--- |
| Job |Onderliggende runbooks worden uitgevoerd in dezelfde taak als bovenliggend niveau Hallo Hallo. |Een afzonderlijke taak voor Hallo onderliggend runbook gemaakt. |
| Uitvoering |Bovenliggend runbook wacht Hallo onderliggend runbook toocomplete voordat u doorgaat. |Bovenliggend runbook gaat direct verder nadat onderliggend runbook is gestart *of* bovenliggend runbook wacht Hallo onderliggende taak toofinish. |
| Uitvoer |Bovenliggend runbook kan uitvoer rechtstreeks ophalen van onderliggend runbook. |Bovenliggend runbook moet uitvoer ophalen uit taak van onderliggend runbook *of* bovenliggend runbook kan uitvoer rechtstreeks ophalen van onderliggend runbook. |
| Parameters |Waarden voor parameters van onderliggend runbook Hallo worden afzonderlijk opgegeven en elk gegevenstype kunnen gebruiken. |Waarden voor Hallo onderliggend runbook parameters moeten worden samengevoegd in één hashtabel en kunnen alleen bestaan uit eenvoudig, matrix en object gegevenstypen die gebruiken voor de JSON-serialisatie. |
| Automation-account |Bovenliggend runbook kan alleen onderliggend runbook gebruiken in Hallo dezelfde automation-account. |Bovenliggend runbook kunt onderliggend runbook vanuit een automation-account via hello gebruiken dezelfde Azure-abonnement en zelfs een ander abonnement als u een tooit verbinding hebt. |
| Publiceren |Onderliggend runbook moet worden gepubliceerd voordat bovenliggend runbook wordt gepubliceerd. |Onderliggend runbook moet worden gepubliceerd voordat bovenliggend runbook wordt gestart. |

## <a name="next-steps"></a>Volgende stappen
* [Een runbook starten in Azure Automation](automation-starting-a-runbook.md)
* [Runbookuitvoer en -berichten in Azure Automation](automation-runbook-output-and-messages.md)

