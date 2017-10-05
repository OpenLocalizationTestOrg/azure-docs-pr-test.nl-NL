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
# <a name="scheduling-a-runbook-in-azure-automation"></a><span data-ttu-id="97840-103">Een runbook in Azure Automation plannen</span><span class="sxs-lookup"><span data-stu-id="97840-103">Scheduling a runbook in Azure Automation</span></span>
<span data-ttu-id="97840-104">Als u een runbook in Azure Automation om te beginnen bij een bepaalde tijd plannen, koppelt u deze aan een of meer planningen.</span><span class="sxs-lookup"><span data-stu-id="97840-104">To schedule a runbook in Azure Automation to start at a specified time, you link it to one or more schedules.</span></span> <span data-ttu-id="97840-105">Een schema kan worden geconfigureerd voor uitvoeren nadat de of op een opnieuw optreedt per uur of dagelijks schema voor runbooks in de klassieke Azure portal en voor runbooks in de Azure portal, kunt u bovendien plannen ze voor wekelijks, maandelijks, specifieke dagen van de week of dagen van de maand of een bepaalde dag van de maand.</span><span class="sxs-lookup"><span data-stu-id="97840-105">A schedule can be configured to either run once or on a reoccurring hourly or daily schedule for runbooks in the Azure classic portal and for runbooks in the Azure portal,  you can additionally schedule them for weekly, monthly, specific days of the week or days of the month, or a particular day of the month.</span></span>  <span data-ttu-id="97840-106">Een runbook kan worden gekoppeld aan meerdere planningen kan, en een planning meerdere runbooks die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="97840-106">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span>

## <a name="creating-a-schedule"></a><span data-ttu-id="97840-107">Een schema maken</span><span class="sxs-lookup"><span data-stu-id="97840-107">Creating a schedule</span></span>
<span data-ttu-id="97840-108">U kunt een nieuw schema voor runbooks maken in de Azure-portal in de klassieke portal of met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97840-108">You can create a new schedule for runbooks in the Azure portal, in the classic portal, or with Windows PowerShell.</span></span> <span data-ttu-id="97840-109">U hebt ook de optie voor het maken van een nieuw schema wanneer u een runbook koppelen aan een schema met de Azure classic of Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="97840-109">You also have the option of creating a new schedule when you link a runbook to a schedule using the Azure classic or Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="97840-110">Wanneer u een schema aan een runbook koppelt, wordt Automation slaat de huidige versies van de modules in uw account en koppelt ze aan die planning.</span><span class="sxs-lookup"><span data-stu-id="97840-110">When you associate a schedule with a runbook, Automation stores the current versions of the modules in your account and links them to that schedule.</span></span>  <span data-ttu-id="97840-111">Dit betekent dat als u een module met versie 1.0 had in uw account wanneer u een planning gemaakt en vervolgens de module naar versie 2.0 bijwerken, de planning wordt blijven gebruiken 1.0.</span><span class="sxs-lookup"><span data-stu-id="97840-111">This means that if you had a module with version 1.0 in your account when you created a schedule and then update the module to version 2.0, the schedule will continue to use 1.0.</span></span>  <span data-ttu-id="97840-112">Als u wilt de bijgewerkte moduleversie gebruiken, moet u een nieuw schema maken.</span><span class="sxs-lookup"><span data-stu-id="97840-112">In order to use the updated module version, you must create a new schedule.</span></span> 
> 
> 

### <a name="to-create-a-new-schedule-in-the-azure-classic-portal"></a><span data-ttu-id="97840-113">Een nieuwe planning maken in de klassieke Azure portal</span><span class="sxs-lookup"><span data-stu-id="97840-113">To create a new schedule in the Azure classic portal</span></span>
1. <span data-ttu-id="97840-114">In de klassieke Azure portal, selecteer Automation en vervolgens selecteert u de naam van een automation-account.</span><span class="sxs-lookup"><span data-stu-id="97840-114">In the Azure classic portal, select Automation and then then select the name of an automation account.</span></span>
2. <span data-ttu-id="97840-115">Selecteer de **activa** tabblad.</span><span class="sxs-lookup"><span data-stu-id="97840-115">Select the **Assets** tab.</span></span>
3. <span data-ttu-id="97840-116">Klik onderaan in het venster **instelling toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="97840-116">At the bottom of the window, click **Add Setting**.</span></span>
4. <span data-ttu-id="97840-117">Klik op **planning toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="97840-117">Click **Add Schedule**.</span></span>
5. <span data-ttu-id="97840-118">Typ een **naam** en optioneel een **beschrijving** voor de nieuwe schedule.your planning wordt uitgevoerd **één keer**, **per uur**, **dagelijkse**, **wekelijkse**, of **maandelijkse**.</span><span class="sxs-lookup"><span data-stu-id="97840-118">Type a **Name** and optionally a **Description** for the new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span></span>
6. <span data-ttu-id="97840-119">Geef een **begintijd** en andere opties, afhankelijk van het type van het schema dat u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="97840-119">Specify a **Start Time** and other options depending on the type of schedule that you selected.</span></span>

### <a name="to-create-a-new-schedule-in-the-azure-portal"></a><span data-ttu-id="97840-120">Een nieuwe planning maken in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="97840-120">To create a new schedule in the Azure portal</span></span>
1. <span data-ttu-id="97840-121">Klik in de Azure-portal van uw automation-account op de **activa** tegel openen de **activa** blade.</span><span class="sxs-lookup"><span data-stu-id="97840-121">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="97840-122">Klik op de **planningen** tegel openen de **planningen** blade.</span><span class="sxs-lookup"><span data-stu-id="97840-122">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="97840-123">Klik op **toevoegen van een planning** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="97840-123">Click **Add a schedule** at the top of the blade.</span></span>
4. <span data-ttu-id="97840-124">Op de **nieuwe planning** blade, typ een **naam** en optioneel een **beschrijving** voor het nieuwe schema.</span><span class="sxs-lookup"><span data-stu-id="97840-124">On the **New schedule** blade, type a **Name** and optionally a **Description** for the new schedule.</span></span>
5. <span data-ttu-id="97840-125">Selecteer de planning wordt één keer uitgevoerd of volgens een terugkerende planning door te selecteren **eenmaal** of **terugkeerpatroon**.</span><span class="sxs-lookup"><span data-stu-id="97840-125">Select whether the schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span></span>  <span data-ttu-id="97840-126">Als u selecteert **eenmaal** Geef een **begintijd** en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="97840-126">If you select **Once** specify a **Start time** and then click **Create**.</span></span>  <span data-ttu-id="97840-127">Als u selecteert **terugkeerpatroon**, Geef een **begintijd** en de frequentie voor hoe vaak het runbook moet worden herhaald - door **uur**, **dag**, **week**, of door **maand**.</span><span class="sxs-lookup"><span data-stu-id="97840-127">If you select **Recurrence**, specify a **Start time** and the frequency for how often you want the runbook to repeat - by **hour**, **day**, **week**, or by **month**.</span></span>  <span data-ttu-id="97840-128">Als u selecteert **week** of **maand** uit de vervolgkeuzelijst de **terugkeerpatroon optie** wordt weergegeven in de blade en geselecteerde de **terugkeerpatroon optie** blade worden weergegeven en kunt u de dag van week selecteren als u hebt geselecteerd **week**.</span><span class="sxs-lookup"><span data-stu-id="97840-128">If you select **week** or **month** from the drop-down list, the **Recurrence option** will appear in the blade and upon selection, the **Recurrence option** blade will be presented and you can select the day of week if you selected **week**.</span></span>  <span data-ttu-id="97840-129">Als u hebt geselecteerd **maand**, kunt u kiezen door **weekdagen** of specifieke dagen van de maand op de kalender en tot slot wilt u uitvoeren op de laatste dag van de maand of niet, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="97840-129">If you selected **month**, you can choose by **week days** or specific days of the month on the calendar and finally, do you want to run it on the last day of the month or not and then click **OK**.</span></span>   

### <a name="to-create-a-new-schedule-with-windows-powershell"></a><span data-ttu-id="97840-130">Een nieuw schema maken met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="97840-130">To create a new schedule with Windows PowerShell</span></span>
<span data-ttu-id="97840-131">U kunt de [nieuw AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet een nieuwe planning maken in Azure Automation voor klassieke runbooks of [nieuw AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet voor runbooks in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="97840-131">You can use the [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet to create a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="97840-132">De begintijd voor de planning en de frequentie die moet worden uitgevoerd, moet u opgeven.</span><span class="sxs-lookup"><span data-stu-id="97840-132">You must specify the start time for the schedule and the frequency it should run.</span></span>

<span data-ttu-id="97840-133">De volgende voorbeeldopdrachten laten zien hoe een nieuw schema dat elke dag om 3:30 PM op 20 januari 2015 beginnen met een cmdlet voor Azure Service Management wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="97840-133">The following sample commands show how to create a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

<span data-ttu-id="97840-134">De volgende voorbeeldopdrachten laat zien hoe maakt u een planning voor de 15e en 30e van elke maand met een cmdlet voor Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="97840-134">The following sample commands shows how to create a schedule for the 15th and 30th of every month using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-to-a-runbook"></a><span data-ttu-id="97840-135">Een planning koppelen aan een runbook</span><span class="sxs-lookup"><span data-stu-id="97840-135">Linking a schedule to a runbook</span></span>
<span data-ttu-id="97840-136">Een runbook kan worden gekoppeld aan meerdere planningen kan, en een planning meerdere runbooks die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="97840-136">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span> <span data-ttu-id="97840-137">Als een runbook parameters heeft, kunt u waarden opgeven voor deze.</span><span class="sxs-lookup"><span data-stu-id="97840-137">If a runbook has parameters, then you can provide values for them.</span></span> <span data-ttu-id="97840-138">U moet waarden opgeven voor de verplichte parameters en waarden kan opgeven voor optionele parameters.</span><span class="sxs-lookup"><span data-stu-id="97840-138">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span></span>  <span data-ttu-id="97840-139">Deze waarden worden gebruikt wanneer die het runbook wordt gestart door dit schema.</span><span class="sxs-lookup"><span data-stu-id="97840-139">These values will be used each time the runbook is started by this schedule.</span></span>  <span data-ttu-id="97840-140">U kunt hetzelfde runbook koppelen aan een ander schema en andere parameterwaarden opgeven.</span><span class="sxs-lookup"><span data-stu-id="97840-140">You can attach the same runbook to another schedule and specify different parameter values.</span></span>

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-classic-portal"></a><span data-ttu-id="97840-141">Een planning koppelen aan een runbook met de klassieke Azure portal</span><span class="sxs-lookup"><span data-stu-id="97840-141">To link a schedule to a runbook with the Azure classic portal</span></span>
1. <span data-ttu-id="97840-142">Selecteer in de klassieke Azure portal **Automation** en klik vervolgens op de naam van een automation-account.</span><span class="sxs-lookup"><span data-stu-id="97840-142">In the Azure classic portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="97840-143">Selecteer de **Runbooks** tabblad.</span><span class="sxs-lookup"><span data-stu-id="97840-143">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="97840-144">Klik op de naam van het runbook te plannen.</span><span class="sxs-lookup"><span data-stu-id="97840-144">Click on the name of the runbook to schedule.</span></span>
4. <span data-ttu-id="97840-145">Klik op de **planning** tabblad.</span><span class="sxs-lookup"><span data-stu-id="97840-145">Click the **Schedule** tab.</span></span>
5. <span data-ttu-id="97840-146">Als het runbook is momenteel niet gekoppeld aan een schema, dan krijgt u de optie voor het **koppeling naar een nieuw schema** of **koppelen aan een bestaand schema**.</span><span class="sxs-lookup"><span data-stu-id="97840-146">If the runbook is not currently linked to a schedule, then you will be given the option to **Link to a New Schedule** or **Link to an Existing Schedule**.</span></span>  <span data-ttu-id="97840-147">Als het runbook is momenteel gekoppeld aan een schema, klikt u op **koppeling** aan de onderkant van het venster voor toegang tot deze opties.</span><span class="sxs-lookup"><span data-stu-id="97840-147">If the runbook is currently linked to a schedule, click **Link** at the bottom of the window to access these options.</span></span>
6. <span data-ttu-id="97840-148">Als het runbook parameters heeft, wordt u gevraagd hun waarden.</span><span class="sxs-lookup"><span data-stu-id="97840-148">If the runbook has parameters, you will be prompted for their values.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-portal"></a><span data-ttu-id="97840-149">Een planning koppelen aan een runbook met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="97840-149">To link a schedule to a runbook with the Azure portal</span></span>
1. <span data-ttu-id="97840-150">Klik in de Azure-portal van uw automation-account op de **Runbooks** tegel openen de **Runbooks** blade.</span><span class="sxs-lookup"><span data-stu-id="97840-150">In the Azure portal, from your automation account, click the **Runbooks** tile to open the **Runbooks** blade.</span></span>
2. <span data-ttu-id="97840-151">Klik op de naam van het runbook te plannen.</span><span class="sxs-lookup"><span data-stu-id="97840-151">Click on the name of the runbook to schedule.</span></span>
3. <span data-ttu-id="97840-152">Als het runbook is momenteel niet gekoppeld aan een schema, vervolgens krijgt u de optie voor het maken van een nieuwe planning of een koppeling naar een bestaand schema.</span><span class="sxs-lookup"><span data-stu-id="97840-152">If the runbook is not currently linked to a schedule, then you will be given the option to create a new schedule or link to an existing schedule.</span></span>  
4. <span data-ttu-id="97840-153">Als het runbook parameters heeft, kunt u de optie **instellingen (standaard: Azure) voor uitvoeren wijzigen** en de **Parameters** blade wordt weergegeven waarin u overeenkomstig de gegevens kunt invoeren.</span><span class="sxs-lookup"><span data-stu-id="97840-153">If the runbook has parameters, you can select the option **Modify run settings (Default:Azure)** and the **Parameters** blade is presented where you can enter the information accordingly.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-windows-powershell"></a><span data-ttu-id="97840-154">Een planning aan een runbook met Windows PowerShell koppelen</span><span class="sxs-lookup"><span data-stu-id="97840-154">To link a schedule to a runbook with Windows PowerShell</span></span>
<span data-ttu-id="97840-155">Kunt u de [registreren AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) een planning koppelen aan een klassieke runbook of [registreren AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet voor runbooks in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="97840-155">You can use the [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) to link a schedule to a classic runbook or [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet for runbooks in the Azure portal.</span></span>  <span data-ttu-id="97840-156">U kunt waarden voor het runbook parameters opgeven met de Parameters-parameter.</span><span class="sxs-lookup"><span data-stu-id="97840-156">You can specify values for the runbook’s parameters with the Parameters parameter.</span></span> <span data-ttu-id="97840-157">Zie [een Runbook starten in Azure Automation](automation-starting-a-runbook.md) voor meer informatie over het opgeven van parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="97840-157">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span></span>

<span data-ttu-id="97840-158">De volgende voorbeeldopdrachten laten zien hoe een planning met een Azure-servicebeheer-cmdlet parameters koppelen.</span><span class="sxs-lookup"><span data-stu-id="97840-158">The following sample commands show how to link a schedule using an Azure Service Management cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

<span data-ttu-id="97840-159">De volgende voorbeeldopdrachten laten zien hoe een planning koppelen aan een runbook met een Azure Resource Manager-cmdlet met parameters.</span><span class="sxs-lookup"><span data-stu-id="97840-159">The following sample commands show how to link a schedule to a runbook using an Azure Resource Manager cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a><span data-ttu-id="97840-160">Het uitschakelen van een planning</span><span class="sxs-lookup"><span data-stu-id="97840-160">Disabling a schedule</span></span>
<span data-ttu-id="97840-161">Wanneer u een planning uitschakelt, wordt alle runbooks die zijn gekoppeld niet meer uitgevoerd op die planning.</span><span class="sxs-lookup"><span data-stu-id="97840-161">When you disable a schedule, any runbooks linked to it will no longer run on that schedule.</span></span> <span data-ttu-id="97840-162">U kunt handmatig taakplanning uitschakelen of stel een verlooptijd voor schema's met een frequentie wanneer u deze maakt.</span><span class="sxs-lookup"><span data-stu-id="97840-162">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span></span> <span data-ttu-id="97840-163">Wanneer de verlooptijd is bereikt, wordt het schema uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="97840-163">When the expiration time is reached, the schedule will be disabled.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-classic-portal"></a><span data-ttu-id="97840-164">Uitschakelen van een planning van de klassieke Azure portal</span><span class="sxs-lookup"><span data-stu-id="97840-164">To disable a schedule from the Azure classic portal</span></span>
<span data-ttu-id="97840-165">U kunt een planning in de klassieke Azure portal op de pagina Details van de planning voor de planning uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="97840-165">You can disable a schedule in the Azure classic portal from the Schedule Details page for the schedule.</span></span>

1. <span data-ttu-id="97840-166">In de klassieke Azure portal, selecteer Automation en klik vervolgens de naam van een automation-account.</span><span class="sxs-lookup"><span data-stu-id="97840-166">In the Azure classic portal, select Automation and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="97840-167">Selecteer het tabblad activa.</span><span class="sxs-lookup"><span data-stu-id="97840-167">Select the Assets tab.</span></span>
3. <span data-ttu-id="97840-168">Klik op de naam van een planning te openen, de detailpagina ervan.</span><span class="sxs-lookup"><span data-stu-id="97840-168">Click the name of a schedule to open its detail page.</span></span>
4. <span data-ttu-id="97840-169">Wijziging **ingeschakeld** naar **Nee**.</span><span class="sxs-lookup"><span data-stu-id="97840-169">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-portal"></a><span data-ttu-id="97840-170">Uitschakelen van een planning van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="97840-170">To disable a schedule from the Azure portal</span></span>
1. <span data-ttu-id="97840-171">Klik in de Azure-portal van uw automation-account op de **activa** tegel openen de **activa** blade.</span><span class="sxs-lookup"><span data-stu-id="97840-171">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="97840-172">Klik op de **planningen** tegel openen de **planningen** blade.</span><span class="sxs-lookup"><span data-stu-id="97840-172">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="97840-173">Klik op de naam van een planning om de blade details te openen.</span><span class="sxs-lookup"><span data-stu-id="97840-173">Click the name of a schedule to open the details blade.</span></span>
4. <span data-ttu-id="97840-174">Wijziging **ingeschakeld** naar **Nee**.</span><span class="sxs-lookup"><span data-stu-id="97840-174">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-with-windows-powershell"></a><span data-ttu-id="97840-175">Een planning met Windows PowerShell uitschakelen</span><span class="sxs-lookup"><span data-stu-id="97840-175">To disable a schedule with Windows PowerShell</span></span>
<span data-ttu-id="97840-176">U kunt de [Set AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet om de eigenschappen van een bestaande planning voor een klassieke runbook wijzigen of [Set AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet voor runbooks in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="97840-176">You can use the [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet to change the properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="97840-177">Schakel de planning opgeven **false** voor de **IsEnabled** parameter.</span><span class="sxs-lookup"><span data-stu-id="97840-177">To disable the schedule, specify **false** for the **IsEnabled** parameter.</span></span>

<span data-ttu-id="97840-178">De volgende voorbeeldopdrachten laten zien hoe een schema met de cmdlet Azure Service Management uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="97840-178">The following sample commands show how to disable a schedule using the Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

<span data-ttu-id="97840-179">De volgende voorbeeldopdrachten laten zien hoe een runbook met een cmdlet voor Azure Resource Manager-taakplanning uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="97840-179">The following sample commands show how to disable a schedule for a runbook using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a><span data-ttu-id="97840-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="97840-180">Next steps</span></span>
* <span data-ttu-id="97840-181">Zie voor meer informatie over het werken met schema's, [planning Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span><span class="sxs-lookup"><span data-stu-id="97840-181">To learn more about working with schedules, see [Schedule Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span></span>
* <span data-ttu-id="97840-182">Om te beginnen met runbooks in Azure Automation, Zie [een Runbook starten in Azure Automation](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="97840-182">To get started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span></span> 

