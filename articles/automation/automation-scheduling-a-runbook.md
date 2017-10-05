---
title: Planning van een runbook in Azure Automation | Microsoft Docs
description: Beschrijft hoe een planning maken in Azure Automation, zodat u automatisch een runbook op een bepaald tijdstip of volgens een terugkerende planning starten kunt.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 52f1d55f141bb1b3948e3b7039cfc131a5e407b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Een runbook in Azure Automation plannen
Als u een runbook in Azure Automation om te beginnen bij een bepaalde tijd plannen, koppelt u deze aan een of meer planningen. Een schema kan worden geconfigureerd voor uitvoeren nadat de of op een opnieuw optreedt per uur of dagelijks schema voor runbooks in de klassieke Azure portal en voor runbooks in de Azure portal, kunt u bovendien plannen ze voor wekelijks, maandelijks, specifieke dagen van de week of dagen van de maand of een bepaalde dag van de maand.  Een runbook kan worden gekoppeld aan meerdere planningen kan, en een planning meerdere runbooks die zijn gekoppeld.

## <a name="creating-a-schedule"></a>Een schema maken
U kunt een nieuw schema voor runbooks maken in de Azure-portal in de klassieke portal of met Windows PowerShell. U hebt ook de optie voor het maken van een nieuw schema wanneer u een runbook koppelen aan een schema met de Azure classic of Azure-portal.

> [!NOTE]
> Wanneer u een schema aan een runbook koppelt, wordt Automation slaat de huidige versies van de modules in uw account en koppelt ze aan die planning.  Dit betekent dat als u een module met versie 1.0 had in uw account wanneer u een planning gemaakt en vervolgens de module naar versie 2.0 bijwerken, de planning wordt blijven gebruiken 1.0.  Als u wilt de bijgewerkte moduleversie gebruiken, moet u een nieuw schema maken. 
> 
> 

### <a name="to-create-a-new-schedule-in-the-azure-classic-portal"></a>Een nieuwe planning maken in de klassieke Azure portal
1. In de klassieke Azure portal, selecteer Automation en vervolgens selecteert u de naam van een automation-account.
2. Selecteer de **activa** tabblad.
3. Klik onderaan in het venster **instelling toevoegen**.
4. Klik op **planning toevoegen**.
5. Typ een **naam** en optioneel een **beschrijving** voor de nieuwe schedule.your planning wordt uitgevoerd **één keer**, **per uur**, **dagelijkse**, **wekelijkse**, of **maandelijkse**.
6. Geef een **begintijd** en andere opties, afhankelijk van het type van het schema dat u hebt geselecteerd.

### <a name="to-create-a-new-schedule-in-the-azure-portal"></a>Een nieuwe planning maken in de Azure portal
1. Klik in de Azure-portal van uw automation-account op de **activa** tegel openen de **activa** blade.
2. Klik op de **planningen** tegel openen de **planningen** blade.
3. Klik op **toevoegen van een planning** boven aan de blade.
4. Op de **nieuwe planning** blade, typ een **naam** en optioneel een **beschrijving** voor het nieuwe schema.
5. Selecteer de planning wordt één keer uitgevoerd of volgens een terugkerende planning door te selecteren **eenmaal** of **terugkeerpatroon**.  Als u selecteert **eenmaal** Geef een **begintijd** en klik vervolgens op **maken**.  Als u selecteert **terugkeerpatroon**, Geef een **begintijd** en de frequentie voor hoe vaak het runbook moet worden herhaald - door **uur**, **dag**, **week**, of door **maand**.  Als u selecteert **week** of **maand** uit de vervolgkeuzelijst de **terugkeerpatroon optie** wordt weergegeven in de blade en geselecteerde de **terugkeerpatroon optie** blade worden weergegeven en kunt u de dag van week selecteren als u hebt geselecteerd **week**.  Als u hebt geselecteerd **maand**, kunt u kiezen door **weekdagen** of specifieke dagen van de maand op de kalender en tot slot wilt u uitvoeren op de laatste dag van de maand of niet, en klik vervolgens op **OK**.   

### <a name="to-create-a-new-schedule-with-windows-powershell"></a>Een nieuw schema maken met Windows PowerShell
U kunt de [nieuw AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet een nieuwe planning maken in Azure Automation voor klassieke runbooks of [nieuw AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet voor runbooks in de Azure-portal. De begintijd voor de planning en de frequentie die moet worden uitgevoerd, moet u opgeven.

De volgende voorbeeldopdrachten laten zien hoe een nieuw schema dat elke dag om 3:30 PM op 20 januari 2015 beginnen met een cmdlet voor Azure Service Management wordt uitgevoerd.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

De volgende voorbeeldopdrachten laat zien hoe maakt u een planning voor de 15e en 30e van elke maand met een cmdlet voor Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-to-a-runbook"></a>Een planning koppelen aan een runbook
Een runbook kan worden gekoppeld aan meerdere planningen kan, en een planning meerdere runbooks die zijn gekoppeld. Als een runbook parameters heeft, kunt u waarden opgeven voor deze. U moet waarden opgeven voor de verplichte parameters en waarden kan opgeven voor optionele parameters.  Deze waarden worden gebruikt wanneer die het runbook wordt gestart door dit schema.  U kunt hetzelfde runbook koppelen aan een ander schema en andere parameterwaarden opgeven.

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-classic-portal"></a>Een planning koppelen aan een runbook met de klassieke Azure portal
1. Selecteer in de klassieke Azure portal **Automation** en klik vervolgens op de naam van een automation-account.
2. Selecteer de **Runbooks** tabblad.
3. Klik op de naam van het runbook te plannen.
4. Klik op de **planning** tabblad.
5. Als het runbook is momenteel niet gekoppeld aan een schema, dan krijgt u de optie voor het **koppeling naar een nieuw schema** of **koppelen aan een bestaand schema**.  Als het runbook is momenteel gekoppeld aan een schema, klikt u op **koppeling** aan de onderkant van het venster voor toegang tot deze opties.
6. Als het runbook parameters heeft, wordt u gevraagd hun waarden.  

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-portal"></a>Een planning koppelen aan een runbook met de Azure-portal
1. Klik in de Azure-portal van uw automation-account op de **Runbooks** tegel openen de **Runbooks** blade.
2. Klik op de naam van het runbook te plannen.
3. Als het runbook is momenteel niet gekoppeld aan een schema, vervolgens krijgt u de optie voor het maken van een nieuwe planning of een koppeling naar een bestaand schema.  
4. Als het runbook parameters heeft, kunt u de optie **instellingen (standaard: Azure) voor uitvoeren wijzigen** en de **Parameters** blade wordt weergegeven waarin u overeenkomstig de gegevens kunt invoeren.  

### <a name="to-link-a-schedule-to-a-runbook-with-windows-powershell"></a>Een planning aan een runbook met Windows PowerShell koppelen
Kunt u de [registreren AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) een planning koppelen aan een klassieke runbook of [registreren AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet voor runbooks in de Azure-portal.  U kunt waarden voor het runbook parameters opgeven met de Parameters-parameter. Zie [een Runbook starten in Azure Automation](automation-starting-a-runbook.md) voor meer informatie over het opgeven van parameterwaarden.

De volgende voorbeeldopdrachten laten zien hoe een planning met een Azure-servicebeheer-cmdlet parameters koppelen.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

De volgende voorbeeldopdrachten laten zien hoe een planning koppelen aan een runbook met een Azure Resource Manager-cmdlet met parameters.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a>Het uitschakelen van een planning
Wanneer u een planning uitschakelt, wordt alle runbooks die zijn gekoppeld niet meer uitgevoerd op die planning. U kunt handmatig taakplanning uitschakelen of stel een verlooptijd voor schema's met een frequentie wanneer u deze maakt. Wanneer de verlooptijd is bereikt, wordt het schema uitgeschakeld.

### <a name="to-disable-a-schedule-from-the-azure-classic-portal"></a>Uitschakelen van een planning van de klassieke Azure portal
U kunt een planning in de klassieke Azure portal op de pagina Details van de planning voor de planning uitschakelen.

1. In de klassieke Azure portal, selecteer Automation en klik vervolgens de naam van een automation-account.
2. Selecteer het tabblad activa.
3. Klik op de naam van een planning te openen, de detailpagina ervan.
4. Wijziging **ingeschakeld** naar **Nee**.

### <a name="to-disable-a-schedule-from-the-azure-portal"></a>Uitschakelen van een planning van de Azure-portal
1. Klik in de Azure-portal van uw automation-account op de **activa** tegel openen de **activa** blade.
2. Klik op de **planningen** tegel openen de **planningen** blade.
3. Klik op de naam van een planning om de blade details te openen.
4. Wijziging **ingeschakeld** naar **Nee**.

### <a name="to-disable-a-schedule-with-windows-powershell"></a>Een planning met Windows PowerShell uitschakelen
U kunt de [Set AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet om de eigenschappen van een bestaande planning voor een klassieke runbook wijzigen of [Set AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet voor runbooks in de Azure-portal. Schakel de planning opgeven **false** voor de **IsEnabled** parameter.

De volgende voorbeeldopdrachten laten zien hoe een schema met de cmdlet Azure Service Management uitschakelen.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

De volgende voorbeeldopdrachten laten zien hoe een runbook met een cmdlet voor Azure Resource Manager-taakplanning uitschakelen.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het werken met schema's, [planning Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)
* Om te beginnen met runbooks in Azure Automation, Zie [een Runbook starten in Azure Automation](automation-starting-a-runbook.md) 

