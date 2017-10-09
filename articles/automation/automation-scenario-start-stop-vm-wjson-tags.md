---
title: aaaUse labels JSON-indeling tooschedule Azure VM-status | Microsoft Docs
description: In dit artikel laat zien hoe toouse JSON tekenreeksen op labels tooautomate Hallo planning van de virtuele machine opstarten en afsluiten.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="549fc-103">Azure Automation-scenario: een planning voor de virtuele machine van Azure opstarten en afsluiten toocreate met behulp van JSON-indeling tags</span><span class="sxs-lookup"><span data-stu-id="549fc-103">Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="549fc-104">Klanten willen vaak tooschedule Hallo opstarten en afsluiten van de virtuele machines toohelp abonnement kosten te verlagen of ondersteuning voor bedrijven en technische vereisten.</span><span class="sxs-lookup"><span data-stu-id="549fc-104">Customers often want tooschedule hello startup and shutdown of virtual machines toohelp reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="549fc-105">Hallo kunt volgende scenario u tooset van geautomatiseerde opstarten en afsluiten van uw virtuele machines met behulp van een label aangeroepen planning op een niveau van de resourcegroep of het niveau van de virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="549fc-105">hello following scenario enables you tooset up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="549fc-106">Dit schema kan worden geconfigureerd vanuit zondag tooSaturday een opstarten en afsluiten.</span><span class="sxs-lookup"><span data-stu-id="549fc-106">This schedule can be configured from Sunday tooSaturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="549fc-107">We hebt enkele out-of-the-box-opties.</span><span class="sxs-lookup"><span data-stu-id="549fc-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="549fc-108">Deze omvatten:</span><span class="sxs-lookup"><span data-stu-id="549fc-108">These include:</span></span>

* <span data-ttu-id="549fc-109">[Virtuele-machineschaalsets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) met instellingen voor automatisch schalen die u in staat stellen tooscale in of uit.</span><span class="sxs-lookup"><span data-stu-id="549fc-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you tooscale in or out.</span></span>
* <span data-ttu-id="549fc-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) -service, die Hallo ingebouwde mogelijkheden is van de planning van bewerkingen voor opstarten en afsluiten.</span><span class="sxs-lookup"><span data-stu-id="549fc-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has hello built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="549fc-111">Deze opties ondersteunen echter alleen specifieke scenario's en kan niet worden toegepast tooinfrastructure-as-a-service (IaaS) virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="549fc-111">However, these options only support specific scenarios and cannot be applied tooinfrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="549fc-112">Wanneer Hallo planning tag toegepaste tooa resourcegroep is, is het ook toegepaste tooall virtuele machines in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="549fc-112">When hello Schedule tag is applied tooa resource group, it's also applied tooall virtual machines inside that resource group.</span></span> <span data-ttu-id="549fc-113">Als een planning ook rechtstreeks toegepaste tooa VM is, hebben Hallo laatste planning voorrang in Hallo volgorde:</span><span class="sxs-lookup"><span data-stu-id="549fc-113">If a schedule is also directly applied tooa VM, hello last schedule takes precedence in hello following order:</span></span>

1. <span data-ttu-id="549fc-114">De resourcegroep toegepaste tooa plannen</span><span class="sxs-lookup"><span data-stu-id="549fc-114">Schedule applied tooa resource group</span></span>
2. <span data-ttu-id="549fc-115">Toegepaste tooa resourcegroep en de virtuele machine in de resourcegroep Hallo plannen</span><span class="sxs-lookup"><span data-stu-id="549fc-115">Schedule applied tooa resource group and virtual machine in hello resource group</span></span>
3. <span data-ttu-id="549fc-116">Planning toegepast tooa virtuele machine</span><span class="sxs-lookup"><span data-stu-id="549fc-116">Schedule applied tooa virtual machine</span></span>

<span data-ttu-id="549fc-117">In dit scenario wordt in wezen een JSON-tekenreeks met de opgegeven notatie en toegevoegd als Hallo-waarde voor een tag schema genoemd.</span><span class="sxs-lookup"><span data-stu-id="549fc-117">This scenario essentially takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="549fc-118">Een runbook wordt vervolgens een lijst met alle resourcegroepen en virtuele machines en identificeert Hallo schema's voor elke virtuele machine op basis van de eerder vermelde Hallo-scenario.</span><span class="sxs-lookup"><span data-stu-id="549fc-118">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each VM based on hello scenarios listed earlier.</span></span> <span data-ttu-id="549fc-119">Vervolgens doorlopen Hallo virtuele machines met's die zijn gekoppeld en welke actie moet worden gehouden evalueert.</span><span class="sxs-lookup"><span data-stu-id="549fc-119">Next it loops through hello VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="549fc-120">Bijvoorbeeld, bepaalt dat door virtuele machines moeten toobe gestopt, afsluiten of genegeerd.</span><span class="sxs-lookup"><span data-stu-id="549fc-120">For example, it determines which VMs need toobe stopped, shut down, or ignored.</span></span>

<span data-ttu-id="549fc-121">Deze runbooks verifiëren met behulp van Hallo [Azure uitvoeren als-account](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="549fc-121">These runbooks authenticate by using hello [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-hello-runbooks-for-hello-scenario"></a><span data-ttu-id="549fc-122">Hallo runbooks voor Hallo scenario downloaden</span><span class="sxs-lookup"><span data-stu-id="549fc-122">Download hello runbooks for hello scenario</span></span>
<span data-ttu-id="549fc-123">Dit scenario bestaat uit vier PowerShell Workflow-runbooks die u van Hallo downloaden kunt [TechNet-galerie](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) of Hallo [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) opslagplaats voor dit project.</span><span class="sxs-lookup"><span data-stu-id="549fc-123">This scenario consists of four PowerShell Workflow runbooks that you can download from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="549fc-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="549fc-124">Runbook</span></span> | <span data-ttu-id="549fc-125">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="549fc-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="549fc-126">Test ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="549fc-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="549fc-127">Controleert de planning van elke virtuele machine en afsluiten of opstarten, afhankelijk van het Hallo-planning wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="549fc-127">Checks each virtual machine schedule and performs shutdown or startup depending on hello schedule.</span></span> |
| <span data-ttu-id="549fc-128">Voeg ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="549fc-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="549fc-129">Hallo planning tag tooa VM of de resource wordt groep toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="549fc-129">Adds hello Schedule tag tooa VM or resource group.</span></span> |
| <span data-ttu-id="549fc-130">Update ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="549fc-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="549fc-131">Hallo bestaande planning tag wijzigt door deze te vervangen door een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="549fc-131">Modifies hello existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="549fc-132">Verwijder ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="549fc-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="549fc-133">Hallo planning tag verwijdert uit een groep VM of de resource.</span><span class="sxs-lookup"><span data-stu-id="549fc-133">Removes hello Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="549fc-134">Dit scenario installeren en configureren</span><span class="sxs-lookup"><span data-stu-id="549fc-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-hello-runbooks"></a><span data-ttu-id="549fc-135">Installeren en Hallo runbooks publiceren</span><span class="sxs-lookup"><span data-stu-id="549fc-135">Install and publish hello runbooks</span></span>
<span data-ttu-id="549fc-136">Na het downloaden van Hallo runbooks, kunt u deze importeren met behulp van Hallo-procedure in [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="549fc-136">After downloading hello runbooks, you can import them by using hello procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="549fc-137">Elk runbook gepubliceerd nadat deze is geïmporteerd in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="549fc-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a><span data-ttu-id="549fc-138">Een planning toohello Test ResourceSchedule runbook toevoegen</span><span class="sxs-lookup"><span data-stu-id="549fc-138">Add a schedule toohello Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="549fc-139">Volg deze stappen tooenable Hallo planning voor Hallo Test ResourceSchedule runbook.</span><span class="sxs-lookup"><span data-stu-id="549fc-139">Follow these steps tooenable hello schedule for hello Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="549fc-140">Dit is het Hallo runbook die controleert van welke virtuele machines moet worden gestart, afsluiten, of leeg is.</span><span class="sxs-lookup"><span data-stu-id="549fc-140">This is hello runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="549fc-141">Open uw Automation-account van hello Azure-portal, en klik vervolgens op Hallo **Runbooks** tegel.</span><span class="sxs-lookup"><span data-stu-id="549fc-141">From hello Azure portal, open your Automation account, and then click hello **Runbooks** tile.</span></span>
2. <span data-ttu-id="549fc-142">Op Hallo **Test ResourceSchedule** blade, klikt u op Hallo **planningen** tegel.</span><span class="sxs-lookup"><span data-stu-id="549fc-142">On hello **Test-ResourceSchedule** blade, click hello **Schedules** tile.</span></span>
3. <span data-ttu-id="549fc-143">Op Hallo **planningen** blade, klikt u op **toevoegen van een planning**.</span><span class="sxs-lookup"><span data-stu-id="549fc-143">On hello **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="549fc-144">Op Hallo **planningen** blade Selecteer **koppelen van een planning tooyour runbook**.</span><span class="sxs-lookup"><span data-stu-id="549fc-144">On hello **Schedules** blade, select **Link a schedule tooyour runbook**.</span></span> <span data-ttu-id="549fc-145">Selecteer vervolgens **Maak een nieuwe planning**.</span><span class="sxs-lookup"><span data-stu-id="549fc-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="549fc-146">Op Hallo **nieuwe planning** blade, typt u Hallo-naam van dit schema, bijvoorbeeld: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="549fc-146">On hello **New schedule** blade, type in hello name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="549fc-147">Voor de planning Hallo **Start**, Hallo start tooan uur tijdsinterval instellen.</span><span class="sxs-lookup"><span data-stu-id="549fc-147">For hello schedule **Start**, set hello start time tooan hour increment.</span></span>
7. <span data-ttu-id="549fc-148">Selecteer **terugkeerpatroon**, en vervolgens voor **herhaald elke interval**, selecteer **1 uur**.</span><span class="sxs-lookup"><span data-stu-id="549fc-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="549fc-149">Controleer **instellen dat verlopen** te is ingesteld,**Nee**, en klik vervolgens op **maken** toosave het nieuwe schema.</span><span class="sxs-lookup"><span data-stu-id="549fc-149">Verify that **Set expiration** is set too**No**, and then click **Create** toosave your new schedule.</span></span>
9. <span data-ttu-id="549fc-150">Op Hallo **planning Runbook** Selecteer opties blade **Parameters en uitvoerinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="549fc-150">On hello **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="549fc-151">In Hallo Test ResourceSchedule **Parameters** blade Voer Hallo-naam van uw abonnement in Hallo **SubscriptionName** veld.</span><span class="sxs-lookup"><span data-stu-id="549fc-151">In hello Test-ResourceSchedule **Parameters** blade, enter hello name of your subscription in hello **SubscriptionName** field.</span></span>  <span data-ttu-id="549fc-152">Dit is alleen Hallo-parameter die zijn voor het Hallo-runbook vereist.</span><span class="sxs-lookup"><span data-stu-id="549fc-152">This is hello only parameter that's required for hello runbook.</span></span>  <span data-ttu-id="549fc-153">Wanneer u klaar bent, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="549fc-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="549fc-154">Hallo runbookschema moet eruitzien als volgende Hallo wanneer dit voltooid:</span><span class="sxs-lookup"><span data-stu-id="549fc-154">hello runbook schedule should look like hello following when it's completed:</span></span>

![Geconfigureerde Test ResourceSchedule runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a><span data-ttu-id="549fc-156">Indeling Hallo JSON-tekenreeks</span><span class="sxs-lookup"><span data-stu-id="549fc-156">Format hello JSON string</span></span>
<span data-ttu-id="549fc-157">Deze oplossing in feite duurt een JSON tekenreeks met de opgegeven notatie en toegevoegd als waarde voor een label Hallo aangeroepen planning.</span><span class="sxs-lookup"><span data-stu-id="549fc-157">This solution basically takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="549fc-158">Een runbook wordt vervolgens een lijst met alle resourcegroepen en virtuele machines en identificeert Hallo schema's voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="549fc-158">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each virtual machine.</span></span>

<span data-ttu-id="549fc-159">Hallo runbook worden doorlopen via Hallo virtuele machines met schema's die zijn gekoppeld en controleert welke acties moeten worden genomen.</span><span class="sxs-lookup"><span data-stu-id="549fc-159">hello runbook loops over hello virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="549fc-160">Hallo Hieronder volgt een voorbeeld van hoe Hallo oplossingen moeten worden opgemaakt:</span><span class="sxs-lookup"><span data-stu-id="549fc-160">hello following is an example of how hello solutions should be formatted:</span></span>

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

<span data-ttu-id="549fc-161">Hier volgt een aantal gedetailleerde informatie over deze structuur:</span><span class="sxs-lookup"><span data-stu-id="549fc-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="549fc-162">Hallo-indeling van dit JSON-structuur is geoptimaliseerd toowork Hallo 256 tekens beperking weg te nemen van de waarde van een enkel label in Azure.</span><span class="sxs-lookup"><span data-stu-id="549fc-162">hello format of this JSON structure is optimized toowork around hello 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="549fc-163">*TzId* vertegenwoordigt Hallo tijdzone van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="549fc-163">*TzId* represents hello time zone of hello virtual machine.</span></span> <span data-ttu-id="549fc-164">Deze ID kan worden verkregen met behulp van Hallo TimeZoneInfo .NET-klasse in een PowerShell-sessie--**[System.TimeZoneInfo]:: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="549fc-164">This ID can be obtained by using hello TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones in PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="549fc-166">Weekdagen worden aangeduid met een numerieke waarde van nul toosix.</span><span class="sxs-lookup"><span data-stu-id="549fc-166">Weekdays are represented with a numeric value of zero toosix.</span></span> <span data-ttu-id="549fc-167">Hallo waarde nul is gelijk aan zondag.</span><span class="sxs-lookup"><span data-stu-id="549fc-167">hello value zero equals Sunday.</span></span>
   * <span data-ttu-id="549fc-168">Hallo begintijd vertegenwoordigd door Hallo **S** kenmerk en de waarde ervan zich in een 24-uurs notatie.</span><span class="sxs-lookup"><span data-stu-id="549fc-168">hello start time is represented with hello **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="549fc-169">Hallo wordt afgesloten of end tijd vertegenwoordigd Hello **E** kenmerk en de waarde ervan zich in een 24-uurs notatie.</span><span class="sxs-lookup"><span data-stu-id="549fc-169">hello end or shutdown time is represented with hello **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="549fc-170">Als hello **S** en **E** kenmerken elke hebben een waarde van nul (0), Hallo virtuele machine blijft in de huidige status op Hallo moment van evaluatie.</span><span class="sxs-lookup"><span data-stu-id="549fc-170">If hello **S** and **E** attributes each have a value of zero (0), hello virtual machine will be left in its present state at hello time of evaluation.</span></span>
3. <span data-ttu-id="549fc-171">Als u tooskip evaluatie voor een specifieke dag van week hello wilt, niet een sectie toevoegen voor die dag van week Hallo.</span><span class="sxs-lookup"><span data-stu-id="549fc-171">If you want tooskip evaluation for a specific day of hello week, don’t add a section for that day of hello week.</span></span> <span data-ttu-id="549fc-172">In Hallo na bijvoorbeeld alleen maandag wordt geëvalueerd en hello andere dagen van week Hallo worden genegeerd:</span><span class="sxs-lookup"><span data-stu-id="549fc-172">In hello following example, only Monday is evaluated, and hello other days of hello week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="549fc-173">Tag-resourcegroepen of VM 's</span><span class="sxs-lookup"><span data-stu-id="549fc-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="549fc-174">tooshut omlaag virtuele machines, moet u tootag Hallo virtuele machines of Hallo resourcegroepen waar ze zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="549fc-174">tooshut down VMs, you need tootag either hello VMs or hello resource groups in which they're located.</span></span> <span data-ttu-id="549fc-175">Virtuele machines waarvoor geen een label voor de planning worden niet geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="549fc-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="549fc-176">Ze zijn niet daarom gestart of afgesloten.</span><span class="sxs-lookup"><span data-stu-id="549fc-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="549fc-177">Er zijn twee manieren tootag resourcegroepen of VM's met deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="549fc-177">There are two ways tootag resource groups or VMs with this solution.</span></span> <span data-ttu-id="549fc-178">U kunt dit doen rechtstreeks vanuit Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="549fc-178">You can do it directly from hello portal.</span></span> <span data-ttu-id="549fc-179">Of u kunt Hallo toevoegen ResourceSchedule, Update-ResourceSchedule en verwijder ResourceSchedule runbooks.</span><span class="sxs-lookup"><span data-stu-id="549fc-179">Or you can use hello Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-hello-portal"></a><span data-ttu-id="549fc-180">Tag via Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="549fc-180">Tag through hello portal</span></span>
<span data-ttu-id="549fc-181">Volg deze stappen tootag een virtuele machine of de resourcegroep in Hallo-portal:</span><span class="sxs-lookup"><span data-stu-id="549fc-181">Follow these steps tootag a virtual machine or resource group in hello portal:</span></span>

1. <span data-ttu-id="549fc-182">Hallo JSON-tekenreeks plat en controleer of er geen spaties.</span><span class="sxs-lookup"><span data-stu-id="549fc-182">Flatten hello JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="549fc-183">Uw JSON-tekenreeks moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="549fc-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="549fc-184">Selecteer Hallo **Tag** pictogram voor een virtuele machine of de resource groep tooapply dit schema.</span><span class="sxs-lookup"><span data-stu-id="549fc-184">Select hello **Tag** icon for a VM or resource group tooapply this schedule.</span></span>

   ![Optie voor VM-tag](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="549fc-186">Labels zijn gedefinieerd een sleutel-waardepaar te volgen.</span><span class="sxs-lookup"><span data-stu-id="549fc-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="549fc-187">Type **planning** in Hallo **sleutel** veld en plak Hallo JSON-tekenreeks in Hallo **waarde** veld.</span><span class="sxs-lookup"><span data-stu-id="549fc-187">Type **Schedule** in hello **Key** field, and then paste hello JSON string into hello **Value** field.</span></span> <span data-ttu-id="549fc-188">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="549fc-188">Click **Save**.</span></span> <span data-ttu-id="549fc-189">Uw nieuwe code wordt nu weergegeven in de lijst Hallo van codes voor uw resource.</span><span class="sxs-lookup"><span data-stu-id="549fc-189">Your new tag should now appear in hello list of tags for your resource.</span></span>

   ![VM planning label](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="549fc-191">Label van PowerShell</span><span class="sxs-lookup"><span data-stu-id="549fc-191">Tag from PowerShell</span></span>
<span data-ttu-id="549fc-192">Alle geïmporteerde runbooks bevatten help-informatie aan begin Hallo van Hallo-script dat wordt beschreven hoe tooexecute runbooks rechtstreeks vanuit PowerShell Hallo.</span><span class="sxs-lookup"><span data-stu-id="549fc-192">All imported runbooks contain help information at hello beginning of hello script that describes how tooexecute hello runbooks directly from PowerShell.</span></span> <span data-ttu-id="549fc-193">U kunt Hallo toevoegen ScheduleResource en Update ScheduleResource runbooks aanroepen vanuit PowerShell.</span><span class="sxs-lookup"><span data-stu-id="549fc-193">You can call hello Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="549fc-194">U doen dit door het doorgeven van de vereiste parameters die u in staat stellen tag Hallo toocreate of update voor een groep VM of de resource buiten Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="549fc-194">You do this by passing required parameters that enable you toocreate or update hello Schedule tag on a VM or resource group outside of hello portal.</span></span>

<span data-ttu-id="549fc-195">toocreate, toevoegen en verwijderen van de labels via PowerShell, moet u eerst te[uw PowerShell-omgeving instellen voor Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="549fc-195">toocreate, add, and delete tags through PowerShell, you first need too[set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="549fc-196">Nadat het Hallo-installatie is voltooid, kunt u doorgaan met de Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="549fc-196">After you complete hello setup, you can proceed with hello following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="549fc-197">Een label schema maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="549fc-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="549fc-198">Open een PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="549fc-198">Open a PowerShell session.</span></span> <span data-ttu-id="549fc-199">Gebruik vervolgens Hallo tooauthenticate voorbeeld met het Run As-account en uw toospecify een abonnement te volgen:</span><span class="sxs-lookup"><span data-stu-id="549fc-199">Then use hello following example tooauthenticate with your Run As account and toospecify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="549fc-200">Definieer de planning hash-tabel.</span><span class="sxs-lookup"><span data-stu-id="549fc-200">Define a schedule hash table.</span></span> <span data-ttu-id="549fc-201">Hier volgt een voorbeeld van hoe moet worden opgebouwd:</span><span class="sxs-lookup"><span data-stu-id="549fc-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="549fc-202">Hallo-parameters die door Hallo runbook vereist zijn definiëren.</span><span class="sxs-lookup"><span data-stu-id="549fc-202">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="549fc-203">In de Hallo voorbeeld te volgen, zijn we die gericht is op een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="549fc-203">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="549fc-204">Als u een resourcegroep bent tagging, verwijdert u Hallo *VMName* parameter van Hallo $params hash-tabel als volgt:</span><span class="sxs-lookup"><span data-stu-id="549fc-204">If you’re tagging a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="549fc-205">Voer Hallo toevoegen ResourceSchedule runbook met Hallo parameters toocreate Hallo planning tag te volgen:</span><span class="sxs-lookup"><span data-stu-id="549fc-205">Run hello Add-ResourceSchedule runbook with hello following parameters toocreate hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="549fc-206">een code van de groep of virtuele machine voor resource, tooupdate uitvoeren Hallo **Update ResourceSchedule** runbook met de Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="549fc-206">tooupdate a resource group or virtual machine tag, execute hello **Update-ResourceSchedule** runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="549fc-207">Verwijderen van een label planning met PowerShell</span><span class="sxs-lookup"><span data-stu-id="549fc-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="549fc-208">Open een PowerShell-sessie en Hallo na tooauthenticate met het Run As-account en uw tooselect uitvoeren en een abonnement opgeven:</span><span class="sxs-lookup"><span data-stu-id="549fc-208">Open a PowerShell session and run hello following tooauthenticate with your Run As account and tooselect and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="549fc-209">Hallo-parameters die door Hallo runbook vereist zijn definiëren.</span><span class="sxs-lookup"><span data-stu-id="549fc-209">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="549fc-210">In de Hallo voorbeeld te volgen, zijn we die gericht is op een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="549fc-210">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="549fc-211">Als u een label van een resourcegroep verwijderen wilt, verwijdert u Hallo *VMName* parameter van Hallo $params hash-tabel als volgt:</span><span class="sxs-lookup"><span data-stu-id="549fc-211">If you’re removing a tag from a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="549fc-212">Hallo verwijderen ResourceSchedule runbook tooremove Hallo planning tag uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="549fc-212">Execute hello Remove-ResourceSchedule runbook tooremove hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="549fc-213">Hallo verwijderen ResourceSchedule runbook tooupdate een code van de groep of virtuele machine voor resource, uitvoeren met Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="549fc-213">tooupdate a resource group or virtual machine tag, execute hello Remove-ResourceSchedule runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="549fc-214">We raden u proactief deze runbooks (en status van de virtuele machines Hallo) tooverify die uw virtuele machines worden afgesloten bewaken en dienovereenkomstig gestart.</span><span class="sxs-lookup"><span data-stu-id="549fc-214">We recommend that you proactively monitor these runbooks (and hello virtual machine states) tooverify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="549fc-215">tooview hello details van Hallo Test ResourceSchedule runbook taak hello Azure-portal, selecteer Hallo **taken** tegel van Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="549fc-215">tooview hello details of hello Test-ResourceSchedule runbook job in hello Azure portal, select hello **Jobs** tile of hello runbook.</span></span> <span data-ttu-id="549fc-216">Hallo taak overzicht Hallo invoerparameters en Hallo uitvoer streamen, Daarnaast toogeneral informatie over het Hallo-taak en eventuele uitzonderingen als ze zich heeft voorgedaan.</span><span class="sxs-lookup"><span data-stu-id="549fc-216">hello job summary displays hello input parameters and hello output stream, in addition toogeneral information about hello job and any exceptions if they occurred.</span></span>

<span data-ttu-id="549fc-217">Hallo **taakoverzicht** berichten van de uitvoer, waarschuwingen en fouten streams Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="549fc-217">hello **Job Summary** includes messages from hello output, warning, and error streams.</span></span> <span data-ttu-id="549fc-218">Selecteer Hallo **uitvoer** tooview tegel gedetailleerde resultaten van Hallo runbook-uitvoering.</span><span class="sxs-lookup"><span data-stu-id="549fc-218">Select hello **Output** tile tooview detailed results from hello runbook execution.</span></span>

![Test ResourceSchedule uitvoer](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="549fc-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="549fc-220">Next steps</span></span>
* <span data-ttu-id="549fc-221">tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="549fc-221">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="549fc-222">toolearn meer informatie over runbooktypen, en hun voordelen en beperkingen, Zie [Azure Automation-runbooktypen](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="549fc-222">toolearn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="549fc-223">Zie voor meer informatie over PowerShell-script ondersteuningsfuncties [systeemeigen PowerShell-scriptondersteuning in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span><span class="sxs-lookup"><span data-stu-id="549fc-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="549fc-224">toolearn meer informatie over logboekregistratie van runbook- en uitvoer, Zie [Runbook uitvoer en berichten in Azure Automation](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="549fc-224">toolearn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="549fc-225">meer informatie over een Azure uitvoeren als-account en hoe tooauthenticate uw runbooks met behulp van, Zie toolearn [runbooks met Azure uitvoeren als-account verifiëren](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="549fc-225">toolearn more about an Azure Run As account and how tooauthenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
