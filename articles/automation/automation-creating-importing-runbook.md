---
title: aaaCreating of importeren van een runbook in Azure Automation
description: Dit artikel wordt beschreven hoe toocreate een nieuw runbook in Azure Automation of importeren uit een bestand.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a>Maken of importeren van een runbook in Azure Automation
U kunt een runbook tooAzure Automation door een van beide toevoegen [maken van een nieuwe](#creating-a-new-runbook) of een bestaand runbook importeren vanuit een bestand of vanuit Hallo [Runbookgalerie](automation-runbook-gallery.md). In dit artikel bevat informatie over het maken en importeren van runbooks uit een bestand.  U kunt alle informatie over de toegang tot de community-runbooks en modules in Hallo krijgen [galerieën Runbook en de module voor Azure Automation](automation-runbook-gallery.md).

## <a name="creating-a-new-runbook"></a>Een nieuw runbook maken
U kunt een nieuw runbook maken in Azure Automation met behulp van een hello Azure portals of Windows PowerShell. Als het Hallo-runbook is gemaakt, kunt u bewerken met behulp van informatie in [Learning PowerShell Workflow](automation-powershell-workflow.md) en [grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md).

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a>een nieuw Azure Automation-runbook met de klassieke Azure-portal Hallo toocreate
U kunt alleen werken met [PowerShell Workflow-runbooks](automation-runbook-types.md#powershell-workflow-runbooks) in hello Azure-portal.

1. In de klassieke Azure-portal hello, klikt u op, **nieuw**, **App Services**, **Automation**, **Runbook**, **snelle invoer**.
2. Geef informatie op Hallo vereist en klik vervolgens op **maken**. Hallo runbooknaam moet beginnen met een letter en letters, cijfers, onderstrepingstekens en streepjes kan hebben.
3. Als u tooedit hello runbook nu wilt, klikt u op **Runbook bewerken**. Klik anders op **OK**.
4. Uw nieuwe runbook wordt weergegeven op Hallo **Runbooks** tabblad.

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a>toocreate een nieuw Azure Automation-runbook Hello Azure-portal
1. Open uw Automation-account in hello Azure-portal.
2. Selecteer in de Hallo Hub, **Runbooks** tooopen Hallo lijst van runbooks.
3. Klik op Hallo **een runbook toevoegen** knop en vervolgens **een nieuw runbook maken**.
4. Typ een **naam** voor Hallo runbook en selecteer de [Type](automation-runbook-types.md). Hallo runbooknaam moet beginnen met een letter en letters, cijfers, onderstrepingstekens en streepjes kan hebben.
5. Klik op **maken** toocreate Hallo runbook en open Hallo-editor.

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a>toocreate een nieuw Azure Automation-runbook met Windows PowerShell
U kunt Hallo [nieuw AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) cmdlet toocreate een lege [PowerShell Workflow-runbook](automation-runbook-types.md#powershell-workflow-runbooks). U kunt Hallo opgeven **naam** parameter toocreate een leeg runbook dat u later bewerken kunt of kunt u Hallo **pad** parameter tooimport een runbook-bestand. Hallo **Type** parameter zijn ook opgenomen toospecify een van de vier hello runbooktypen.

Hallo volgende steekproef opdrachten tonen hoe een nieuw, leeg runbook toocreate.

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a>Een runbook importeren uit een bestand in Azure Automation
U kunt een nieuw runbook maken in Azure Automation via een PowerShell-script of PowerShell-werkstroom (.ps1 extensie) of een geëxporteerde grafisch runbook (.graphrunbook) importeren.  U moet opgeven Hallo [type runbook](automation-runbook-types.md) die wordt gemaakt van Hallo importeren, waarbij rekening wordt gehouden account Hallo overwegingen te volgen.

* Een bestand .graphrunbook kan alleen worden geïmporteerd in een nieuwe [grafisch runbook](automation-runbook-types.md#graphical-runbooks), en de grafische runbooks kunnen alleen worden gemaakt vanuit een bestand .graphrunbook.
* Een ps1-bestand met een PowerShell-werkstroom kan alleen worden geïmporteerd in een [PowerShell Workflow-runbook](automation-runbook-types.md#powershell-workflow-runbooks).  Als het Hallo-bestand bevat meerdere PowerShell-werkstromen, mislukken Hallo importeren. U moet elke werkstroom tooits eigen bestand opslaan en importeren van elk afzonderlijk.
* Een .ps1-bestand bevat geen een werkstroom kan worden geïmporteerd in hetzij een [PowerShell-runbook](automation-runbook-types.md#powershell-runbooks) of een [PowerShell Workflow-runbook](automation-runbook-types.md#powershell-workflow-runbooks).  Als het is geïmporteerd in een PowerShell Workflow-runbook, dan is geconverteerde tooa werkstroom en opmerkingen worden opgenomen in Hallo runbook geven Hallo-wijzigingen die zijn aangebracht.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a>een runbook uit een bestand met de klassieke Azure-portal Hallo tooimport
U kunt hello te volgen procedure tooimport een scriptbestand in Azure Automation.  Houd er rekening mee dat u alleen een ps1-bestand kunt importeren in een PowerShell Workflow-runbook met behulp van deze portal.  U moet hello Azure-portal gebruiken voor andere typen.

1. Selecteer in hello Azure Management portal **Automation** en selecteer vervolgens een Automation-Account.
2. Klik op **Import**.
3. Klik op **bladeren naar bestand** en zoek Hallo script bestand tooimport.
4. Als u tooedit hello runbook nu wilt, klikt u op **Runbook bewerken**. Klik anders op OK.
5. Hallo nieuwe runbook wordt weergegeven op Hallo **Runbooks** tabblad voor Hallo Automation-Account.
6. U moet [hello runbook publiceren](#publishing-a-runbook) voordat u deze kunt uitvoeren.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a>tooimport een runbook uit een bestand met hello Azure-portal
U kunt hello te volgen procedure tooimport een scriptbestand in Azure Automation.  

> [!NOTE]
> Houd er rekening mee dat u alleen een ps1-bestand kunt importeren in een PowerShell Workflow-runbook met behulp van Hallo-portal.
> 
> 

1. Open uw Automation-account in hello Azure-portal.
2. Selecteer in de Hallo Hub, **Runbooks** tooopen Hallo lijst van runbooks.
3. Klik op Hallo **een runbook toevoegen** knop en vervolgens **importeren**.
4. Klik op **Runbook bestand** tooselect Hallo bestand tooimport
5. Als hello **naam** veld is ingeschakeld, hebt u Hallo optie toochange deze.  Hallo runbooknaam moet beginnen met een letter en letters, cijfers, onderstrepingstekens en streepjes kan hebben.
6. Hallo [runbooktype](automation-runbook-types.md) wordt automatisch geselecteerd, maar u kunt Hallo type wijzigen nadat u de toepasselijke beperkingen Hallo rekening. 
7. Hallo nieuwe runbook wordt weergegeven in de lijst Hallo van runbooks voor Hallo Automation-Account.
8. U moet [hello runbook publiceren](#publishing-a-runbook) voordat u deze kunt uitvoeren.

> [!NOTE]
> Als u een grafisch runbook of een grafische PowerShell workflow-runbook importeert, hebt u Hallo optie tooconvert toohello ander type desgewenst. U kunt tootextual niet converteren.
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a>tooimport een runbook uit een scriptbestand met Windows PowerShell
U kunt Hallo [importeren AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet tooimport een scriptbestand als concept PowerShell Workflow-runbook. Als er bestaat al een runbook hello, Hallo importeren mislukt tenzij u Hallo *-Force* parameter. 

Hallo volgende voorbeeldopdrachten laten zien hoe tooimport een script bestand in een runbook.

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a>Een runbook publiceren
Wanneer u maakt of een nieuw runbook importeert, moet u het publiceren voordat u deze kunt uitvoeren.  Elk runbook in Automation heeft een ontwerpversie en een gepubliceerde versie. Alleen Hallo gepubliceerde versie is beschikbaar toobe uitvoeren en alleen de conceptversie Hallo kan worden bewerkt. Hallo gepubliceerde versie wordt niet beïnvloed door de conceptversie van eventuele wijzigingen toohello. Wanneer het Hallo-conceptversie beschikbaar moet worden gesteld, publiceert u deze die Hallo gepubliceerde versie met de conceptversie Hallo overschrijft.

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a>toopublish een runbook met behulp van de klassieke Azure-portal Hallo
1. Hallo runbook in de klassieke Azure-portal Hallo openen.
2. Klik boven Hallo van welkomstscherm op **auteur**.
3. Aan de onderkant van de Hallo van Hallo scherm, klikt u op **publiceren** en vervolgens **Ja** toohello verificatiebericht.

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a>toopublish een runbook met behulp van hello Azure-portal
1. Open Hallo runbook hello Azure-portal.
2. Klik op Hallo **bewerken** knop.
3. Klik op Hallo **publiceren** knop en vervolgens **Ja** toohello verificatiebericht.

## <a name="toopublish-a-runbook-using-windows-powershell"></a>toopublish een runbook met behulp van Windows PowerShell
U kunt Hallo [publiceren AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet toopublish een runbook met Windows PowerShell. Hallo volgende steekproef opdrachten weergeven hoe toopublish een voorbeeldrunbook.

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a>Volgende stappen
* Zie toolearn over hoe u kunt profiteren van hello Runbook- en PowerShell-Module Gallery [galerieën Runbook en de module voor Azure Automation](automation-runbook-gallery.md)
* Zie toolearn meer informatie over het bewerken van PowerShell en PowerShell Workflow-runbooks met een teksteditor [tekstuele runbooks in Azure Automation bewerken](automation-edit-textual-runbook.md)
* toolearn meer informatie over het ontwerpen van een grafische runbook, Zie [grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md)

