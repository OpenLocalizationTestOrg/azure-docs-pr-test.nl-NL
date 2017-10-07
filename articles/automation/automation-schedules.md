---
title: aaaSchedules in Azure Automation | Microsoft Docs
description: Automation-planningen worden automatisch gebruikt tooschedule runbooks in Azure Automation toostart. Hierin wordt beschreven hoe toocreate en beheren van een planning in zodat u automatisch een runbook op een bepaald tijdstip of volgens een terugkerende planning starten kunt.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1c2da639-ad20-4848-920b-88e471b2e1d9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2016
ms.author: magoedte
ms.openlocfilehash: 888a5d15fd3442a2b8ab18dd8b0eb4ab9ad0c0d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Een runbook in Azure Automation plannen
tooschedule een runbook in Azure Automation toostart op een opgegeven periode, koppelt u het tooone of meer schema's. Een planning kan geconfigureerde tooeither uitvoeren nadat de of op een de opnieuw elk uur optreedt beëindigd of dagelijks schema voor runbooks in de klassieke Azure-portal Hallo en voor runbooks in hello Azure-portal kunt u ook plannen ze voor wekelijks, maandelijks, specifieke dagen van week Hallo of dagen Hallo maand of een bepaalde dag van de maand Hallo.  Een runbook kan gekoppelde toomultiple schema's en een planning kan meerdere runbooks gekoppeld tooit hebben.

> [!NOTE]
> Schema's bieden momenteel geen ondersteuning voor Azure Automation DSC-configuraties.
> 
> 

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell-Cmdlets
Hallo-cmdlets in de volgende tabel Hallo gebruikte toocreate zijn en schema's met Windows PowerShell in Azure Automation beheren. Ze worden verzonden als onderdeel van Hallo [Azure PowerShell-module](/powershell/azure/overview).

| Cmdlets | Beschrijving |
|:--- |:--- |
| **Azure Resource Manager-cmdlets** | |
| [Get-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/get-azurermautomationschedule) |Haalt een schema. |
| [Nieuwe AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) |Een nieuw schema maakt. |
| [Verwijder AzureRmAutomationSchedule](/powershell/module/azurerm.automation/remove-azurermautomationschedule) |Hiermee verwijdert u een planning. |
| [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) |Hiermee stelt u Hallo-eigenschappen voor een bestaand schema. |
| [Get-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/set-azurermautomationscheduledrunbook) |Geplande runbooks opgehaald. |
| [Register AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) |Een runbook koppelt met een schema. |
| [Hef de registratie van AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/unregister-azurermautomationscheduledrunbook) |Een runbook uit een planning dissociates. |
| **Azure Service Management-cmdlets** | |
| [Get-AzureAutomationSchedule](/powershell/module/azure/get-azureautomationschedule?view=azuresmps-3.7.0) |Haalt een schema. |
| [Nieuwe AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) |Een nieuw schema maakt. |
| [Verwijder AzureAutomationSchedule](/powershell/module/azure/remove-azureautomationschedule?view=azuresmps-3.7.0) |Hiermee verwijdert u een planning. |
| [Set-AzureAutomationSchedule](/powershell/module/azure/set-azureautomationschedule?view=azuresmps-3.7.0) |Hiermee stelt u Hallo-eigenschappen voor een bestaand schema. |
| [Get-AzureAutomationScheduledRunbook](/powershell/module/azure/get-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Geplande runbooks opgehaald. |
| [Register AzureAutomationScheduledRunbook](/powershell/module/azure/register-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Een runbook koppelt met een schema. |
| [Hef de registratie van AzureAutomationScheduledRunbook](/powershell/module/azure/unregister-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Een runbook uit een planning dissociates. |

## <a name="creating-a-schedule"></a>Een schema maken
In de klassieke portal Hallo of met Windows PowerShell, kunt u een nieuw schema voor runbooks in hello Azure-portal. U hebt ook Hallo-optie voor het maken van een nieuw schema wanneer u een runbook tooa planning hello Azure classic met een koppeling of Azure-portal.

> [!NOTE]
> Azure Automation gebruikt de meest recente modules Hallo in uw Automation-account wanneer een nieuwe geplande taak wordt uitgevoerd.  tooavoid die invloed hebben op uw runbooks en Hallo processen die ze automatiseren, test u eerst alle runbooks die schema's met een speciaal ontworpen is voor het testen van Automation-account hebt gekoppeld.  Dit valideert uw geplande runbooks gaan toowork correct en als dat niet zo is, kunt u verder oplossen en toepassen eventueel vereiste voordat migreren Hallo bijgewerkt runbook versie tooproduction wijzigen.  
>  Uw Automation-account krijgt niet automatisch nieuwe versies van modules tenzij u ze handmatig hebt bijgewerkt door het selecteren van Hallo [Azure-Modules WU](automation-update-azure-modules.md) optie uit Hallo **Modules** blade. 
>  

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate een nieuw schema in hello Azure-portal
1. Klik in hello Azure-portal van uw automation-account op Hallo **activa** tegel tooopen hello **activa** blade.
2. Klik op Hallo **planningen** tegel tooopen hello **planningen** blade.
3. Klik op **toevoegen van een planning** Hallo boven aan het Hallo-blade.
4. Op Hallo **nieuwe planning** blade, typ een **naam** en optioneel een **beschrijving** voor Hallo nieuwe planning.
5. Hallo-planning wordt één keer uitgevoerd of volgens een terugkerende planning selecteren door te selecteren **eenmaal** of **terugkeerpatroon**.  Als u selecteert **eenmaal** Geef een **begintijd** en klik vervolgens op **maken**.  Als u selecteert **terugkeerpatroon**, Geef een **begintijd** en frequentie voor hoe vaak Hallo runbook toorepeat - door Hallo **uur**, **dag**, **week**, of door **maand**.  Als u selecteert **week** of **maand** uit de vervolgkeuzelijst hello, Hallo **terugkeerpatroon optie** wordt weergegeven in de blade Hallo en geselecteerde hello **terugkeerpatroon optie** blade worden weergegeven en kunt u Hallo dag van de week selecteren als u hebt geselecteerd **week**.  Als u hebt geselecteerd **maand**, kunt u kiezen door **weekdagen** of specifieke dagen van maand op Hallo Hallo agenda en tot slot wilt u toch toorun op Hallo van laatste dag van de maand Hallo of niet, en klik vervolgens op **OK** .   

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>een nieuw schema in de klassieke Azure-portal Hallo toocreate
1. In de klassieke Azure-portal hello, selecteer Automation en selecteer vervolgens Hallo-naam van een Automation-account.
2. Selecteer Hallo **activa** tabblad.
3. Aan de onderkant van de Hallo van Hallo-venster, klikt u op **instelling toevoegen**.
4. Klik op **planning toevoegen**.
5. Typ een **naam** en optioneel een **beschrijving** voor nieuwe schedule.your Hallo planning wordt uitgevoerd **één keer**, **per uur**, **Dagelijkse**, **wekelijkse**, of **maandelijkse**.
6. Geef een **begintijd** en andere opties, afhankelijk van Hallo type schema dat u hebt geselecteerd.

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate een nieuwe planning met Windows PowerShell
Kunt u Hallo [nieuw AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) cmdlet toocreate een nieuw schema in Azure Automation voor klassieke runbooks of [nieuw AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) cmdlet voor runbooks in hello Azure Portal. De begintijd Hallo voor Hallo planning en Hallo frequentie die moet worden uitgevoerd, moet u opgeven.

Hallo volgende steekproef opdrachten tonen hoe een planning voor Hallo toocreate 15 en 30 van elke maand met een cmdlet voor Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"

Hallo volgende voorbeeldopdrachten tonen hoe een nieuw schema toocreate die wordt uitgevoerd elke dag om 3:30 uur op 20 januari 2015 beginnen met een Azure-servicebeheer-cmdlet.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

## <a name="linking-a-schedule-tooa-runbook"></a>Een planning tooa runbook koppelen
Een runbook kan gekoppelde toomultiple schema's en een planning kan meerdere runbooks gekoppeld tooit hebben. Als een runbook parameters heeft, kunt u waarden opgeven voor deze. U moet waarden opgeven voor de verplichte parameters en waarden kan opgeven voor optionele parameters.  Deze waarden wordt telkens Hallo runbook wordt gestart door dit schema worden gebruikt.  U kunt koppelen Hallo hetzelfde runbook tooanother schema en geef andere parameterwaarden.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink een runbook plannen tooa Hello Azure-portal
1. Klik in hello Azure-portal van uw automation-account op Hallo **Runbooks** tegel tooopen hello **Runbooks** blade.
2. Klik op de naam Hallo van Hallo runbook tooschedule.
3. Als Hallo runbook niet op dit moment gekoppelde tooa planning is, wordt u worden gegeven Hallo optie toocreate een nieuwe planning of tooan bestaande planning koppelen.  
4. Als Hallo runbook parameters heeft, kunt u de optie Hallo **instellingen (standaard: Azure) voor uitvoeren wijzigen** en Hallo **Parameters** blade wordt weergegeven waarin u dienovereenkomstig Hallo gegevens kunt invoeren.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink een runbook plannen tooa Hello klassieke Azure-portal
1. Selecteer in de klassieke Azure-portal hello, **Automation** en klik vervolgens op Hallo-naam van een Automation-account.
2. Selecteer Hallo **Runbooks** tabblad.
3. Klik op de naam Hallo van Hallo runbook tooschedule.
4. Klik op Hallo **planning** tabblad.
5. Als Hallo runbook niet op dit moment gekoppelde tooa planning is, dan u de optie hello te krijgt**tooa nieuwe planning koppelen** of **tooan bestaande planning koppelen**.  Als het Hallo-runbook is momenteel gekoppelde tooa planning, klikt u op **koppeling** op Hallo onderaan Hallo venster tooaccess deze opties.
6. Als Hallo runbook parameters heeft, wordt u gevraagd hun waarden.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink een planning tooa runbook met Windows PowerShell
Kunt u Hallo [registreren AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink een planning tooa klassieke runbook of [registreren AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) cmdlet voor runbooks in hello Azure-portal.  U kunt waarden voor Hallo runbookparameters met Hallo Parameters parameter opgeven. Zie [een Runbook starten in Azure Automation](automation-starting-a-runbook.md) voor meer informatie over het opgeven van parameterwaarden.

Hallo volgende steekproef opdrachten weergeven hoe toolink een planning tooa runbook met een Azure Resource Manager-cmdlet met parameters.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"
Hallo volgende steekproef opdrachten weergeven hoe toolink een schema met behulp van een cmdlet voor Azure-servicebeheer met parameters.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

## <a name="disabling-a-schedule"></a>Het uitschakelen van een planning
Wanneer u een planning uitschakelt, wordt elke tooit runbooks die zijn gekoppeld niet meer uitgevoerd op die planning. U kunt handmatig taakplanning uitschakelen of stel een verlooptijd voor schema's met een frequentie wanneer u deze maakt. Wanneer de verlooptijd van Hallo is bereikt, wordt Hallo schema uitgeschakeld.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable een planning uit hello Azure-portal
1. Klik in hello Azure-portal van uw automation-account op Hallo **activa** tegel tooopen hello **activa** blade.
2. Klik op Hallo **planningen** tegel tooopen hello **planningen** blade.
3. Klik op Hallo-naam van een planning tooopen Hallo-blade met meer informatie.
4. Wijziging **ingeschakeld** te**Nee**.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable een planning uit Hallo klassieke Azure-portal
U kunt een planning in de klassieke Azure-portal uit Hallo Details van de planning pagina voor de planning Hallo Hallo uitschakelen.

1. In de klassieke Azure-portal hello, Automation selecteren en klik vervolgens op Hallo-naam van een Automation-account.
2. Selecteer Hallo activa tabblad.
3. Klik op Hallo-naam van een planning tooopen de detailpagina ervan.
4. Wijziging **ingeschakeld** te**Nee**.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable een planning met Windows PowerShell
U kunt Hallo [Set AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet toochange Hallo eigenschappen van een bestaande planning voor een klassieke runbook of [Set AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) cmdlet voor runbooks in hello Azure Portal. Hallo toodisable plannen, geef **false** voor Hallo **IsEnabled** parameter.

Hallo volgende steekproef opdrachten weergeven hoe toodisable een planning voor een runbook met een cmdlet voor Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"

Hallo volgende voorbeeldopdrachten laten zien hoe een planning met toodisable Hallo Azure Service Management-cmdlet.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

## <a name="next-steps"></a>Volgende stappen
* Zie tooget gestart met runbooks in Azure Automation [een Runbook starten in Azure Automation](automation-starting-a-runbook.md) 

