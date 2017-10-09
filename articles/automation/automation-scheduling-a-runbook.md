---
title: een runbook in Azure Automation aaaScheduling | Microsoft Docs
description: Beschrijft hoe een schema in Azure Automation toocreate zodat u automatisch een runbook op een bepaald tijdstip of volgens een terugkerende planning starten kunt.
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
ms.openlocfilehash: c215b7ff6aa200466f3be566facba3c0cffcc924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a><span data-ttu-id="e9ab6-103">Een runbook in Azure Automation plannen</span><span class="sxs-lookup"><span data-stu-id="e9ab6-103">Scheduling a runbook in Azure Automation</span></span>
<span data-ttu-id="e9ab6-104">tooschedule een runbook in Azure Automation toostart op een opgegeven periode, koppelt u het tooone of meer schema's.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-104">tooschedule a runbook in Azure Automation toostart at a specified time, you link it tooone or more schedules.</span></span> <span data-ttu-id="e9ab6-105">Een planning kan geconfigureerde tooeither één keer worden uitgevoerd of volgens een terugkerende planning Uurlijkse of dagelijkse voor runbooks in de klassieke Azure-portal Hallo en voor runbooks in hello Azure-portal kunt u bovendien plannen ze voor wekelijks, maandelijks, specifieke dagen van week Hallo of dagen van Hallo maand of een bepaalde dag van de maand Hallo.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-105">A schedule can be configured tooeither run once or on a reoccurring hourly or daily schedule for runbooks in hello Azure classic portal and for runbooks in hello Azure portal,  you can additionally schedule them for weekly, monthly, specific days of hello week or days of hello month, or a particular day of hello month.</span></span>  <span data-ttu-id="e9ab6-106">Een runbook kan gekoppelde toomultiple schema's en een planning kan meerdere runbooks gekoppeld tooit hebben.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-106">A runbook can be linked toomultiple schedules, and a schedule can have multiple runbooks linked tooit.</span></span>

## <a name="creating-a-schedule"></a><span data-ttu-id="e9ab6-107">Een schema maken</span><span class="sxs-lookup"><span data-stu-id="e9ab6-107">Creating a schedule</span></span>
<span data-ttu-id="e9ab6-108">In de klassieke portal Hallo of met Windows PowerShell, kunt u een nieuw schema voor runbooks in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-108">You can create a new schedule for runbooks in hello Azure portal, in hello classic portal, or with Windows PowerShell.</span></span> <span data-ttu-id="e9ab6-109">U hebt ook Hallo-optie voor het maken van een nieuw schema wanneer u een runbook tooa planning hello Azure classic met een koppeling of Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-109">You also have hello option of creating a new schedule when you link a runbook tooa schedule using hello Azure classic or Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="e9ab6-110">Wanneer u een schema aan een runbook koppelt, wordt Automation Hallo huidige versies van Hallo-modules worden opgeslagen in uw account en koppelt deze toothat planning.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-110">When you associate a schedule with a runbook, Automation stores hello current versions of hello modules in your account and links them toothat schedule.</span></span>  <span data-ttu-id="e9ab6-111">Dit betekent dat als u een module met versie 1.0 in uw account was wanneer u een planning hebt gemaakt en werk vervolgens Hallo module tooversion 2.0, Hallo schema toouse 1.0 blijft.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-111">This means that if you had a module with version 1.0 in your account when you created a schedule and then update hello module tooversion 2.0, hello schedule will continue toouse 1.0.</span></span>  <span data-ttu-id="e9ab6-112">In de volgorde toouse Hallo bijgewerkte moduleversie, moet u een nieuw schema maken.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-112">In order toouse hello updated module version, you must create a new schedule.</span></span> 
> 
> 

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a><span data-ttu-id="e9ab6-113">een nieuw schema in de klassieke Azure-portal Hallo toocreate</span><span class="sxs-lookup"><span data-stu-id="e9ab6-113">toocreate a new schedule in hello Azure classic portal</span></span>
1. <span data-ttu-id="e9ab6-114">In de klassieke Azure-portal Hallo, selecteer Automation en vervolgens selecteert u Hallo-naam van een automation-account.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-114">In hello Azure classic portal, select Automation and then then select hello name of an automation account.</span></span>
2. <span data-ttu-id="e9ab6-115">Selecteer Hallo **activa** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-115">Select hello **Assets** tab.</span></span>
3. <span data-ttu-id="e9ab6-116">Aan de onderkant van de Hallo van Hallo-venster, klikt u op **instelling toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-116">At hello bottom of hello window, click **Add Setting**.</span></span>
4. <span data-ttu-id="e9ab6-117">Klik op **planning toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-117">Click **Add Schedule**.</span></span>
5. <span data-ttu-id="e9ab6-118">Typ een **naam** en optioneel een **beschrijving** voor nieuwe schedule.your Hallo planning wordt uitgevoerd **één keer**, **per uur**, **Dagelijkse**, **wekelijkse**, of **maandelijkse**.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-118">Type a **Name** and optionally a **Description** for hello new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span></span>
6. <span data-ttu-id="e9ab6-119">Geef een **begintijd** en andere opties, afhankelijk van Hallo type schema dat u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-119">Specify a **Start Time** and other options depending on hello type of schedule that you selected.</span></span>

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a><span data-ttu-id="e9ab6-120">toocreate een nieuw schema in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e9ab6-120">toocreate a new schedule in hello Azure portal</span></span>
1. <span data-ttu-id="e9ab6-121">Klik in hello Azure-portal van uw automation-account op Hallo **activa** tegel tooopen hello **activa** blade.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-121">In hello Azure portal, from your automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
2. <span data-ttu-id="e9ab6-122">Klik op Hallo **planningen** tegel tooopen hello **planningen** blade.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-122">Click hello **Schedules** tile tooopen hello **Schedules** blade.</span></span>
3. <span data-ttu-id="e9ab6-123">Klik op **toevoegen van een planning** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-123">Click **Add a schedule** at hello top of hello blade.</span></span>
4. <span data-ttu-id="e9ab6-124">Op Hallo **nieuwe planning** blade, typ een **naam** en optioneel een **beschrijving** voor Hallo nieuwe planning.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-124">On hello **New schedule** blade, type a **Name** and optionally a **Description** for hello new schedule.</span></span>
5. <span data-ttu-id="e9ab6-125">Hallo-planning wordt één keer uitgevoerd of volgens een terugkerende planning selecteren door te selecteren **eenmaal** of **terugkeerpatroon**.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-125">Select whether hello schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span></span>  <span data-ttu-id="e9ab6-126">Als u selecteert **eenmaal** Geef een **begintijd** en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-126">If you select **Once** specify a **Start time** and then click **Create**.</span></span>  <span data-ttu-id="e9ab6-127">Als u selecteert **terugkeerpatroon**, Geef een **begintijd** en frequentie voor hoe vaak Hallo runbook toorepeat - door Hallo **uur**, **dag**, **week**, of door **maand**.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-127">If you select **Recurrence**, specify a **Start time** and hello frequency for how often you want hello runbook toorepeat - by **hour**, **day**, **week**, or by **month**.</span></span>  <span data-ttu-id="e9ab6-128">Als u selecteert **week** of **maand** uit de vervolgkeuzelijst hello, Hallo **terugkeerpatroon optie** wordt weergegeven in de blade Hallo en geselecteerde hello **terugkeerpatroon optie** blade worden weergegeven en kunt u Hallo dag van de week selecteren als u hebt geselecteerd **week**.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-128">If you select **week** or **month** from hello drop-down list, hello **Recurrence option** will appear in hello blade and upon selection, hello **Recurrence option** blade will be presented and you can select hello day of week if you selected **week**.</span></span>  <span data-ttu-id="e9ab6-129">Als u hebt geselecteerd **maand**, kunt u kiezen door **weekdagen** of specifieke dagen van maand op Hallo Hallo agenda en tot slot wilt u toch toorun op Hallo van laatste dag van de maand Hallo of niet, en klik vervolgens op **OK** .</span><span class="sxs-lookup"><span data-stu-id="e9ab6-129">If you selected **month**, you can choose by **week days** or specific days of hello month on hello calendar and finally, do you want toorun it on hello last day of hello month or not and then click **OK**.</span></span>   

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a><span data-ttu-id="e9ab6-130">toocreate een nieuwe planning met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9ab6-130">toocreate a new schedule with Windows PowerShell</span></span>
<span data-ttu-id="e9ab6-131">Kunt u Hallo [nieuw AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet toocreate een nieuw schema in Azure Automation voor klassieke runbooks of [nieuw AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet voor runbooks in hello Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-131">You can use hello [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet toocreate a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet for runbooks in hello Azure portal.</span></span> <span data-ttu-id="e9ab6-132">De begintijd Hallo voor Hallo planning en Hallo frequentie die moet worden uitgevoerd, moet u opgeven.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-132">You must specify hello start time for hello schedule and hello frequency it should run.</span></span>

<span data-ttu-id="e9ab6-133">Hallo volgende voorbeeldopdrachten tonen hoe een nieuw schema toocreate die wordt uitgevoerd elke dag om 3:30 uur op 20 januari 2015 beginnen met een Azure-servicebeheer-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-133">hello following sample commands show how toocreate a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

<span data-ttu-id="e9ab6-134">Hallo volgende voorbeeld opdrachten toont hoe een planning voor Hallo toocreate 15 en 30 van elke maand met een cmdlet voor Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-134">hello following sample commands shows how toocreate a schedule for hello 15th and 30th of every month using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-tooa-runbook"></a><span data-ttu-id="e9ab6-135">Een planning tooa runbook koppelen</span><span class="sxs-lookup"><span data-stu-id="e9ab6-135">Linking a schedule tooa runbook</span></span>
<span data-ttu-id="e9ab6-136">Een runbook kan gekoppelde toomultiple schema's en een planning kan meerdere runbooks gekoppeld tooit hebben.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-136">A runbook can be linked toomultiple schedules, and a schedule can have multiple runbooks linked tooit.</span></span> <span data-ttu-id="e9ab6-137">Als een runbook parameters heeft, kunt u waarden opgeven voor deze.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-137">If a runbook has parameters, then you can provide values for them.</span></span> <span data-ttu-id="e9ab6-138">U moet waarden opgeven voor de verplichte parameters en waarden kan opgeven voor optionele parameters.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-138">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span></span>  <span data-ttu-id="e9ab6-139">Deze waarden wordt telkens Hallo runbook wordt gestart door dit schema worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-139">These values will be used each time hello runbook is started by this schedule.</span></span>  <span data-ttu-id="e9ab6-140">U kunt koppelen Hallo hetzelfde runbook tooanother schema en geef andere parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-140">You can attach hello same runbook tooanother schedule and specify different parameter values.</span></span>

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a><span data-ttu-id="e9ab6-141">toolink een runbook plannen tooa Hello klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e9ab6-141">toolink a schedule tooa runbook with hello Azure classic portal</span></span>
1. <span data-ttu-id="e9ab6-142">Selecteer in de klassieke Azure-portal hello, **Automation** en klik vervolgens op Hallo-naam van een automation-account.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-142">In hello Azure classic portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="e9ab6-143">Selecteer Hallo **Runbooks** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-143">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="e9ab6-144">Klik op de naam Hallo van Hallo runbook tooschedule.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-144">Click on hello name of hello runbook tooschedule.</span></span>
4. <span data-ttu-id="e9ab6-145">Klik op Hallo **planning** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-145">Click hello **Schedule** tab.</span></span>
5. <span data-ttu-id="e9ab6-146">Als Hallo runbook niet op dit moment gekoppelde tooa planning is, dan u de optie hello te krijgt**tooa nieuwe planning koppelen** of **tooan bestaande planning koppelen**.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-146">If hello runbook is not currently linked tooa schedule, then you will be given hello option too**Link tooa New Schedule** or **Link tooan Existing Schedule**.</span></span>  <span data-ttu-id="e9ab6-147">Als het Hallo-runbook is momenteel gekoppelde tooa planning, klikt u op **koppeling** op Hallo onderaan Hallo venster tooaccess deze opties.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-147">If hello runbook is currently linked tooa schedule, click **Link** at hello bottom of hello window tooaccess these options.</span></span>
6. <span data-ttu-id="e9ab6-148">Als Hallo runbook parameters heeft, wordt u gevraagd hun waarden.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-148">If hello runbook has parameters, you will be prompted for their values.</span></span>  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a><span data-ttu-id="e9ab6-149">toolink een runbook plannen tooa Hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e9ab6-149">toolink a schedule tooa runbook with hello Azure portal</span></span>
1. <span data-ttu-id="e9ab6-150">Klik in hello Azure-portal van uw automation-account op Hallo **Runbooks** tegel tooopen hello **Runbooks** blade.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-150">In hello Azure portal, from your automation account, click hello **Runbooks** tile tooopen hello **Runbooks** blade.</span></span>
2. <span data-ttu-id="e9ab6-151">Klik op de naam Hallo van Hallo runbook tooschedule.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-151">Click on hello name of hello runbook tooschedule.</span></span>
3. <span data-ttu-id="e9ab6-152">Als Hallo runbook niet op dit moment gekoppelde tooa planning is, wordt u worden gegeven Hallo optie toocreate een nieuwe planning of tooan bestaande planning koppelen.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-152">If hello runbook is not currently linked tooa schedule, then you will be given hello option toocreate a new schedule or link tooan existing schedule.</span></span>  
4. <span data-ttu-id="e9ab6-153">Als Hallo runbook parameters heeft, kunt u de optie Hallo **instellingen (standaard: Azure) voor uitvoeren wijzigen** en Hallo **Parameters** blade wordt weergegeven waarin u dienovereenkomstig Hallo gegevens kunt invoeren.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-153">If hello runbook has parameters, you can select hello option **Modify run settings (Default:Azure)** and hello **Parameters** blade is presented where you can enter hello information accordingly.</span></span>  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a><span data-ttu-id="e9ab6-154">toolink een planning tooa runbook met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9ab6-154">toolink a schedule tooa runbook with Windows PowerShell</span></span>
<span data-ttu-id="e9ab6-155">Kunt u Hallo [registreren AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink een planning tooa klassieke runbook of [registreren AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet voor runbooks in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-155">You can use hello [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink a schedule tooa classic runbook or [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet for runbooks in hello Azure portal.</span></span>  <span data-ttu-id="e9ab6-156">U kunt waarden voor Hallo runbookparameters met Hallo Parameters parameter opgeven.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-156">You can specify values for hello runbook’s parameters with hello Parameters parameter.</span></span> <span data-ttu-id="e9ab6-157">Zie [een Runbook starten in Azure Automation](automation-starting-a-runbook.md) voor meer informatie over het opgeven van parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-157">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span></span>

<span data-ttu-id="e9ab6-158">Hallo volgende steekproef opdrachten weergeven hoe toolink een schema met behulp van een cmdlet voor Azure-servicebeheer met parameters.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-158">hello following sample commands show how toolink a schedule using an Azure Service Management cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

<span data-ttu-id="e9ab6-159">Hallo volgende steekproef opdrachten weergeven hoe toolink een planning tooa runbook met een Azure Resource Manager-cmdlet met parameters.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-159">hello following sample commands show how toolink a schedule tooa runbook using an Azure Resource Manager cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a><span data-ttu-id="e9ab6-160">Het uitschakelen van een planning</span><span class="sxs-lookup"><span data-stu-id="e9ab6-160">Disabling a schedule</span></span>
<span data-ttu-id="e9ab6-161">Wanneer u een planning uitschakelt, wordt elke tooit runbooks die zijn gekoppeld niet meer uitgevoerd op die planning.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-161">When you disable a schedule, any runbooks linked tooit will no longer run on that schedule.</span></span> <span data-ttu-id="e9ab6-162">U kunt handmatig taakplanning uitschakelen of stel een verlooptijd voor schema's met een frequentie wanneer u deze maakt.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-162">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span></span> <span data-ttu-id="e9ab6-163">Wanneer de verlooptijd van Hallo is bereikt, wordt Hallo schema uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-163">When hello expiration time is reached, hello schedule will be disabled.</span></span>

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a><span data-ttu-id="e9ab6-164">toodisable een planning uit Hallo klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e9ab6-164">toodisable a schedule from hello Azure classic portal</span></span>
<span data-ttu-id="e9ab6-165">U kunt een planning in de klassieke Azure-portal uit Hallo Details van de planning pagina voor de planning Hallo Hallo uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-165">You can disable a schedule in hello Azure classic portal from hello Schedule Details page for hello schedule.</span></span>

1. <span data-ttu-id="e9ab6-166">In de klassieke Azure-portal hello, selecteer Automation en vervolgens klikt u op Hallo naam van een automation-account.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-166">In hello Azure classic portal, select Automation and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="e9ab6-167">Selecteer Hallo activa tabblad.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-167">Select hello Assets tab.</span></span>
3. <span data-ttu-id="e9ab6-168">Klik op Hallo-naam van een planning tooopen de detailpagina ervan.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-168">Click hello name of a schedule tooopen its detail page.</span></span>
4. <span data-ttu-id="e9ab6-169">Wijziging **ingeschakeld** te**Nee**.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-169">Change **Enabled** too**No**.</span></span>

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a><span data-ttu-id="e9ab6-170">toodisable een planning uit hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e9ab6-170">toodisable a schedule from hello Azure portal</span></span>
1. <span data-ttu-id="e9ab6-171">Klik in hello Azure-portal van uw automation-account op Hallo **activa** tegel tooopen hello **activa** blade.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-171">In hello Azure portal, from your automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
2. <span data-ttu-id="e9ab6-172">Klik op Hallo **planningen** tegel tooopen hello **planningen** blade.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-172">Click hello **Schedules** tile tooopen hello **Schedules** blade.</span></span>
3. <span data-ttu-id="e9ab6-173">Klik op Hallo-naam van een planning tooopen Hallo-blade met meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-173">Click hello name of a schedule tooopen hello details blade.</span></span>
4. <span data-ttu-id="e9ab6-174">Wijziging **ingeschakeld** te**Nee**.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-174">Change **Enabled** too**No**.</span></span>

### <a name="toodisable-a-schedule-with-windows-powershell"></a><span data-ttu-id="e9ab6-175">toodisable een planning met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9ab6-175">toodisable a schedule with Windows PowerShell</span></span>
<span data-ttu-id="e9ab6-176">U kunt Hallo [Set AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet toochange Hallo eigenschappen van een bestaande planning voor een klassieke runbook of [Set AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet voor runbooks in hello Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-176">You can use hello [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet toochange hello properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet for runbooks in hello Azure portal.</span></span> <span data-ttu-id="e9ab6-177">Hallo toodisable plannen, geef **false** voor Hallo **IsEnabled** parameter.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-177">toodisable hello schedule, specify **false** for hello **IsEnabled** parameter.</span></span>

<span data-ttu-id="e9ab6-178">Hallo volgende voorbeeldopdrachten laten zien hoe een planning met toodisable Hallo Azure Service Management-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-178">hello following sample commands show how toodisable a schedule using hello Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

<span data-ttu-id="e9ab6-179">Hallo volgende steekproef opdrachten weergeven hoe toodisable een planning voor een runbook met een cmdlet voor Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9ab6-179">hello following sample commands show how toodisable a schedule for a runbook using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a><span data-ttu-id="e9ab6-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9ab6-180">Next steps</span></span>
* <span data-ttu-id="e9ab6-181">toolearn meer informatie over het werken met planningen, Zie [planning Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span><span class="sxs-lookup"><span data-stu-id="e9ab6-181">toolearn more about working with schedules, see [Schedule Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span></span>
* <span data-ttu-id="e9ab6-182">Zie tooget gestart met runbooks in Azure Automation [een Runbook starten in Azure Automation](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="e9ab6-182">tooget started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span></span> 

