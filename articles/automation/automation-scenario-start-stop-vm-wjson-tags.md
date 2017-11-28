---
title: JSON-indeling codes gebruiken om de status van de virtuele machine van Azure plannen | Microsoft Docs
description: In dit artikel laat zien hoe u van tekenreeksen voor JSON-tags voor het automatiseren van de planning van de virtuele machine opstarten en afsluiten.
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
ms.openlocfilehash: f8d9563318c3afe299cebb7c889874392f114f84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-to-create-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="cda90-103">Azure Automation-scenario: labels JSON-indeling gebruiken voor het maken van een planning voor de virtuele machine van Azure opstarten en afsluiten</span><span class="sxs-lookup"><span data-stu-id="cda90-103">Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="cda90-104">Klanten willen vaak het opstarten en afsluiten van de virtuele machines om abonnement kosten te verlagen of ondersteuning voor bedrijfs- en technische vereisten te plannen.</span><span class="sxs-lookup"><span data-stu-id="cda90-104">Customers often want to schedule the startup and shutdown of virtual machines to help reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="cda90-105">Het volgende scenario kunt u voor het instellen van geautomatiseerde opstarten en afsluiten van uw virtuele machines met behulp van een label aangeroepen planning op een niveau van de resourcegroep of het niveau van de virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="cda90-105">The following scenario enables you to set up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="cda90-106">Dit schema kan worden geconfigureerd van zondag tot zaterdag een opstarten en afsluiten.</span><span class="sxs-lookup"><span data-stu-id="cda90-106">This schedule can be configured from Sunday to Saturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="cda90-107">We hebt enkele out-of-the-box-opties.</span><span class="sxs-lookup"><span data-stu-id="cda90-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="cda90-108">Deze omvatten:</span><span class="sxs-lookup"><span data-stu-id="cda90-108">These include:</span></span>

* <span data-ttu-id="cda90-109">[Virtuele-machineschaalsets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) met automatisch schalen instellingen waarmee u in of uit te schalen.</span><span class="sxs-lookup"><span data-stu-id="cda90-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you to scale in or out.</span></span>
* <span data-ttu-id="cda90-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service met de ingebouwde mogelijkheden van de planning van bewerkingen voor opstarten en afsluiten.</span><span class="sxs-lookup"><span data-stu-id="cda90-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has the built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="cda90-111">Deze opties ondersteunen echter alleen specifieke scenario's en infrastructuur-as-a-service (IaaS) virtuele machines kan niet worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="cda90-111">However, these options only support specific scenarios and cannot be applied to infrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="cda90-112">Wanneer het schema-label wordt toegepast op een resourcegroep, wordt deze ook toegepast op alle virtuele machines in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="cda90-112">When the Schedule tag is applied to a resource group, it's also applied to all virtual machines inside that resource group.</span></span> <span data-ttu-id="cda90-113">Als een schema ook rechtstreeks op een virtuele machine is toegepast, hebben de laatste planning voorrang in de volgende volgorde:</span><span class="sxs-lookup"><span data-stu-id="cda90-113">If a schedule is also directly applied to a VM, the last schedule takes precedence in the following order:</span></span>

1. <span data-ttu-id="cda90-114">Planning toegepast op een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="cda90-114">Schedule applied to a resource group</span></span>
2. <span data-ttu-id="cda90-115">Planning toegepast op een resourcegroep en de virtuele machine in de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="cda90-115">Schedule applied to a resource group and virtual machine in the resource group</span></span>
3. <span data-ttu-id="cda90-116">Planning toegepast op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="cda90-116">Schedule applied to a virtual machine</span></span>

<span data-ttu-id="cda90-117">In dit scenario wordt in wezen een JSON-tekenreeks met de opgegeven notatie en toegevoegd als de waarde voor een tag schema genoemd.</span><span class="sxs-lookup"><span data-stu-id="cda90-117">This scenario essentially takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="cda90-118">Een runbook wordt vervolgens een lijst met alle resourcegroepen en virtuele machines en identificeert de planningen voor elke virtuele machine op basis van de scenario's met de eerder vermelde.</span><span class="sxs-lookup"><span data-stu-id="cda90-118">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each VM based on the scenarios listed earlier.</span></span> <span data-ttu-id="cda90-119">Naast het doorlopen van de virtuele machines met's die zijn gekoppeld en evalueert welke actie moet worden gehouden.</span><span class="sxs-lookup"><span data-stu-id="cda90-119">Next it loops through the VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="cda90-120">Bijvoorbeeld, bepaalt het welke virtuele machines moeten worden gestopt, afsluiten of genegeerd.</span><span class="sxs-lookup"><span data-stu-id="cda90-120">For example, it determines which VMs need to be stopped, shut down, or ignored.</span></span>

<span data-ttu-id="cda90-121">Deze runbooks verifiëren met behulp van de [Azure uitvoeren als-account](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="cda90-121">These runbooks authenticate by using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-the-runbooks-for-the-scenario"></a><span data-ttu-id="cda90-122">Downloaden van de runbooks voor het scenario</span><span class="sxs-lookup"><span data-stu-id="cda90-122">Download the runbooks for the scenario</span></span>
<span data-ttu-id="cda90-123">Dit scenario bestaat uit vier PowerShell Workflow-runbooks die u van downloaden kunt de [TechNet-galerie](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) of de [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) opslagplaats voor dit project.</span><span class="sxs-lookup"><span data-stu-id="cda90-123">This scenario consists of four PowerShell Workflow runbooks that you can download from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or the [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="cda90-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="cda90-124">Runbook</span></span> | <span data-ttu-id="cda90-125">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cda90-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cda90-126">Test ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="cda90-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="cda90-127">Controleert de planning van elke virtuele machine en wordt afgesloten of opgestart, afhankelijk van de planning wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cda90-127">Checks each virtual machine schedule and performs shutdown or startup depending on the schedule.</span></span> |
| <span data-ttu-id="cda90-128">Voeg ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="cda90-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="cda90-129">Voegt de schema-tag toe aan een groep VM of de resource.</span><span class="sxs-lookup"><span data-stu-id="cda90-129">Adds the Schedule tag to a VM or resource group.</span></span> |
| <span data-ttu-id="cda90-130">Update ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="cda90-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="cda90-131">Hiermee wijzigt u de tag planning door deze te vervangen door een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="cda90-131">Modifies the existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="cda90-132">Verwijder ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="cda90-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="cda90-133">Hiermee verwijdert u de schema-code uit een groep VM of de resource.</span><span class="sxs-lookup"><span data-stu-id="cda90-133">Removes the Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="cda90-134">Dit scenario installeren en configureren</span><span class="sxs-lookup"><span data-stu-id="cda90-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-the-runbooks"></a><span data-ttu-id="cda90-135">De runbooks installeren en publiceren</span><span class="sxs-lookup"><span data-stu-id="cda90-135">Install and publish the runbooks</span></span>
<span data-ttu-id="cda90-136">Na het downloaden van de runbooks, kunt u deze importeren met behulp van de procedure in [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="cda90-136">After downloading the runbooks, you can import them by using the procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="cda90-137">Elk runbook gepubliceerd nadat deze is geïmporteerd in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="cda90-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-to-the-test-resourceschedule-runbook"></a><span data-ttu-id="cda90-138">Toevoegen van een planning aan het runbook testen ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="cda90-138">Add a schedule to the Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="cda90-139">Volg deze stappen voor de planning voor het runbook testen ResourceSchedule inschakelt.</span><span class="sxs-lookup"><span data-stu-id="cda90-139">Follow these steps to enable the schedule for the Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="cda90-140">Dit is het runbook dat controleert of welke virtuele machines moet worden gestart, afsluiten of ongewijzigd worden gelaten.</span><span class="sxs-lookup"><span data-stu-id="cda90-140">This is the runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="cda90-141">Open uw Automation-account van de Azure-portal en klik vervolgens op de **Runbooks** tegel.</span><span class="sxs-lookup"><span data-stu-id="cda90-141">From the Azure portal, open your Automation account, and then click the **Runbooks** tile.</span></span>
2. <span data-ttu-id="cda90-142">Op de **Test ResourceSchedule** blade, klikt u op de **planningen** tegel.</span><span class="sxs-lookup"><span data-stu-id="cda90-142">On the **Test-ResourceSchedule** blade, click the **Schedules** tile.</span></span>
3. <span data-ttu-id="cda90-143">Op de **planningen** blade, klikt u op **toevoegen van een planning**.</span><span class="sxs-lookup"><span data-stu-id="cda90-143">On the **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="cda90-144">Op de **planningen** blade Selecteer **een planning aan uw runbook koppelen**.</span><span class="sxs-lookup"><span data-stu-id="cda90-144">On the **Schedules** blade, select **Link a schedule to your runbook**.</span></span> <span data-ttu-id="cda90-145">Selecteer vervolgens **Maak een nieuwe planning**.</span><span class="sxs-lookup"><span data-stu-id="cda90-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="cda90-146">Op de **nieuwe planning** blade, typ de naam van dit schema, bijvoorbeeld: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="cda90-146">On the **New schedule** blade, type in the name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="cda90-147">Voor de planning **Start**, de starttijd instellen op een reeks uur.</span><span class="sxs-lookup"><span data-stu-id="cda90-147">For the schedule **Start**, set the start time to an hour increment.</span></span>
7. <span data-ttu-id="cda90-148">Selecteer **terugkeerpatroon**, en vervolgens voor **herhaald elke interval**, selecteer **1 uur**.</span><span class="sxs-lookup"><span data-stu-id="cda90-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="cda90-149">Controleer **instellen dat verlopen** is ingesteld op **Nee**, en klik vervolgens op **maken** om op te slaan van het nieuwe schema.</span><span class="sxs-lookup"><span data-stu-id="cda90-149">Verify that **Set expiration** is set to **No**, and then click **Create** to save your new schedule.</span></span>
9. <span data-ttu-id="cda90-150">Op de **planning Runbook** Selecteer opties blade **Parameters en uitvoerinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="cda90-150">On the **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="cda90-151">In de Test-ResourceSchedule **Parameters** blade, voer de naam van uw abonnement in de **SubscriptionName** veld.</span><span class="sxs-lookup"><span data-stu-id="cda90-151">In the Test-ResourceSchedule **Parameters** blade, enter the name of your subscription in the **SubscriptionName** field.</span></span>  <span data-ttu-id="cda90-152">Dit is de enige parameter die zijn voor het runbook vereist.</span><span class="sxs-lookup"><span data-stu-id="cda90-152">This is the only parameter that's required for the runbook.</span></span>  <span data-ttu-id="cda90-153">Wanneer u klaar bent, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cda90-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="cda90-154">De planning van het runbook moet eruitzien als in het volgende wanneer dit voltooid:</span><span class="sxs-lookup"><span data-stu-id="cda90-154">The runbook schedule should look like the following when it's completed:</span></span>

![Geconfigureerde Test ResourceSchedule runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-the-json-string"></a><span data-ttu-id="cda90-156">De JSON-tekenreeks voor opmaak</span><span class="sxs-lookup"><span data-stu-id="cda90-156">Format the JSON string</span></span>
<span data-ttu-id="cda90-157">Deze oplossing in feite duurt een JSON-tekenreeks met de opgegeven notatie en toegevoegd als de waarde voor een label aangeroepen planning.</span><span class="sxs-lookup"><span data-stu-id="cda90-157">This solution basically takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="cda90-158">Een runbook wordt vervolgens een lijst met alle resourcegroepen en virtuele machines en identificeert de planningen voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="cda90-158">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each virtual machine.</span></span>

<span data-ttu-id="cda90-159">Het runbook wordt via de virtuele machines met's die zijn gekoppeld en controleert welke acties moeten worden genomen.</span><span class="sxs-lookup"><span data-stu-id="cda90-159">The runbook loops over the virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="cda90-160">Hier volgt een voorbeeld van hoe de oplossingen moeten worden opgemaakt:</span><span class="sxs-lookup"><span data-stu-id="cda90-160">The following is an example of how the solutions should be formatted:</span></span>

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

<span data-ttu-id="cda90-161">Hier volgt een aantal gedetailleerde informatie over deze structuur:</span><span class="sxs-lookup"><span data-stu-id="cda90-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="cda90-162">De indeling van dit JSON-structuur is geoptimaliseerd voor het omzeilen van de beperking van 256 tekens van de waarde van een enkel label in Azure.</span><span class="sxs-lookup"><span data-stu-id="cda90-162">The format of this JSON structure is optimized to work around the 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="cda90-163">*TzId* vertegenwoordigt de tijdzone van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="cda90-163">*TzId* represents the time zone of the virtual machine.</span></span> <span data-ttu-id="cda90-164">Deze ID kan worden verkregen met behulp van de TimeZoneInfo .NET-klasse in een PowerShell-sessie--**[System.TimeZoneInfo]:: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="cda90-164">This ID can be obtained by using the TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones in PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="cda90-166">Weekdagen worden aangeduid met een numerieke waarde van nul tot en met zes.</span><span class="sxs-lookup"><span data-stu-id="cda90-166">Weekdays are represented with a numeric value of zero to six.</span></span> <span data-ttu-id="cda90-167">De waarde nul is gelijk aan zondag.</span><span class="sxs-lookup"><span data-stu-id="cda90-167">The value zero equals Sunday.</span></span>
   * <span data-ttu-id="cda90-168">De begintijd wordt weergegeven met de **S** kenmerk en de waarde ervan zich in een 24-uurs notatie.</span><span class="sxs-lookup"><span data-stu-id="cda90-168">The start time is represented with the **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="cda90-169">De tijd worden afgesloten of end wordt weergegeven met de **E** kenmerk en de waarde ervan zich in een 24-uurs notatie.</span><span class="sxs-lookup"><span data-stu-id="cda90-169">The end or shutdown time is represented with the **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="cda90-170">Als de **S** en **E** kenmerken elke hebben een waarde van nul (0), de virtuele machine blijft in zijn huidige staat op het moment van evaluatie.</span><span class="sxs-lookup"><span data-stu-id="cda90-170">If the **S** and **E** attributes each have a value of zero (0), the virtual machine will be left in its present state at the time of evaluation.</span></span>
3. <span data-ttu-id="cda90-171">Als u overslaan van de evaluatie voor een specifieke dag van de week wilt, niet een sectie toevoegen voor die dag van de week.</span><span class="sxs-lookup"><span data-stu-id="cda90-171">If you want to skip evaluation for a specific day of the week, don’t add a section for that day of the week.</span></span> <span data-ttu-id="cda90-172">In het volgende voorbeeld wordt alleen maandag wordt geëvalueerd en worden genegeerd, de andere dagen van de week:</span><span class="sxs-lookup"><span data-stu-id="cda90-172">In the following example, only Monday is evaluated, and the other days of the week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="cda90-173">Tag-resourcegroepen of VM 's</span><span class="sxs-lookup"><span data-stu-id="cda90-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="cda90-174">Als u wilt afsluiten virtuele machines, moet u code van de virtuele machines of de resourcegroepen waar ze zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="cda90-174">To shut down VMs, you need to tag either the VMs or the resource groups in which they're located.</span></span> <span data-ttu-id="cda90-175">Virtuele machines waarvoor geen een label voor de planning worden niet geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="cda90-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="cda90-176">Ze zijn niet daarom gestart of afgesloten.</span><span class="sxs-lookup"><span data-stu-id="cda90-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="cda90-177">Er zijn twee manieren aan resourcegroepen label of VM's met deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="cda90-177">There are two ways to tag resource groups or VMs with this solution.</span></span> <span data-ttu-id="cda90-178">U kunt dit doen rechtstreeks vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="cda90-178">You can do it directly from the portal.</span></span> <span data-ttu-id="cda90-179">Of u kunt de toevoegen ResourceSchedule, Update-ResourceSchedule en verwijder ResourceSchedule runbooks.</span><span class="sxs-lookup"><span data-stu-id="cda90-179">Or you can use the Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-the-portal"></a><span data-ttu-id="cda90-180">Tag via de portal</span><span class="sxs-lookup"><span data-stu-id="cda90-180">Tag through the portal</span></span>
<span data-ttu-id="cda90-181">Volg deze stappen voor het labelen van een virtuele machine of de resourcegroep op de portal:</span><span class="sxs-lookup"><span data-stu-id="cda90-181">Follow these steps to tag a virtual machine or resource group in the portal:</span></span>

1. <span data-ttu-id="cda90-182">De JSON-tekenreeks plat en controleer of er geen spaties.</span><span class="sxs-lookup"><span data-stu-id="cda90-182">Flatten the JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="cda90-183">Uw JSON-tekenreeks moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="cda90-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="cda90-184">Selecteer de **Tag** pictogram voor een groep VM of de resource toe te passen van dit schema.</span><span class="sxs-lookup"><span data-stu-id="cda90-184">Select the **Tag** icon for a VM or resource group to apply this schedule.</span></span>

   ![Optie voor VM-tag](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="cda90-186">Labels zijn gedefinieerd een sleutel-waardepaar te volgen.</span><span class="sxs-lookup"><span data-stu-id="cda90-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="cda90-187">Type **planning** in de **sleutel** veld en plak de JSON-tekenreeks in de **waarde** veld.</span><span class="sxs-lookup"><span data-stu-id="cda90-187">Type **Schedule** in the **Key** field, and then paste the JSON string into the **Value** field.</span></span> <span data-ttu-id="cda90-188">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cda90-188">Click **Save**.</span></span> <span data-ttu-id="cda90-189">Uw nieuwe code wordt nu weergegeven in de lijst met labels voor uw resource.</span><span class="sxs-lookup"><span data-stu-id="cda90-189">Your new tag should now appear in the list of tags for your resource.</span></span>

   ![VM planning label](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="cda90-191">Label van PowerShell</span><span class="sxs-lookup"><span data-stu-id="cda90-191">Tag from PowerShell</span></span>
<span data-ttu-id="cda90-192">Alle geïmporteerde runbooks bevatten help-informatie aan het begin van het script dat wordt beschreven hoe u de runbooks rechtstreeks vanuit PowerShell uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cda90-192">All imported runbooks contain help information at the beginning of the script that describes how to execute the runbooks directly from PowerShell.</span></span> <span data-ttu-id="cda90-193">U kunt de toevoegen ScheduleResource en Update ScheduleResource runbooks aanroepen vanuit PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cda90-193">You can call the Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="cda90-194">U doen dit door de vereiste parameters waarmee u kunt maken of bijwerken van de schema-code op een groep VM of de resource buiten de portal wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="cda90-194">You do this by passing required parameters that enable you to create or update the Schedule tag on a VM or resource group outside of the portal.</span></span>

<span data-ttu-id="cda90-195">Als u wilt maken, toevoegen en verwijderen van de labels via PowerShell, moet u eerst [uw PowerShell-omgeving instellen voor Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cda90-195">To create, add, and delete tags through PowerShell, you first need to [set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="cda90-196">Nadat u de installatie hebt voltooid, kunt u doorgaan met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="cda90-196">After you complete the setup, you can proceed with the following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="cda90-197">Een label schema maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="cda90-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="cda90-198">Open een PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="cda90-198">Open a PowerShell session.</span></span> <span data-ttu-id="cda90-199">Gebruik vervolgens het volgende voorbeeld om te verifiëren met uw uitvoeren als-account en om op te geven van een abonnement:</span><span class="sxs-lookup"><span data-stu-id="cda90-199">Then use the following example to authenticate with your Run As account and to specify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="cda90-200">Definieer de planning hash-tabel.</span><span class="sxs-lookup"><span data-stu-id="cda90-200">Define a schedule hash table.</span></span> <span data-ttu-id="cda90-201">Hier volgt een voorbeeld van hoe moet worden opgebouwd:</span><span class="sxs-lookup"><span data-stu-id="cda90-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="cda90-202">Definieer de parameters die voor het runbook vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="cda90-202">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="cda90-203">In het volgende voorbeeld wordt een virtuele machine ontwikkelt:</span><span class="sxs-lookup"><span data-stu-id="cda90-203">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="cda90-204">Als u een resourcegroep bent tagging, verwijdert u de *VMName* parameter van de hash $params tabel als volgt:</span><span class="sxs-lookup"><span data-stu-id="cda90-204">If you’re tagging a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="cda90-205">Voer het runbook toevoegen ResourceSchedule met de volgende parameters om de schema-tag te maken:</span><span class="sxs-lookup"><span data-stu-id="cda90-205">Run the Add-ResourceSchedule runbook with the following parameters to create the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="cda90-206">Voor het bijwerken van een resourcegroep of code van de virtuele machine uitvoeren van de **Update ResourceSchedule** runbook met de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="cda90-206">To update a resource group or virtual machine tag, execute the **Update-ResourceSchedule** runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="cda90-207">Verwijderen van een label planning met PowerShell</span><span class="sxs-lookup"><span data-stu-id="cda90-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="cda90-208">Open een PowerShell-sessie en voer de volgende om te verifiëren met uw uitvoeren als-account en te selecteren en een abonnement opgeven:</span><span class="sxs-lookup"><span data-stu-id="cda90-208">Open a PowerShell session and run the following to authenticate with your Run As account and to select and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="cda90-209">Definieer de parameters die voor het runbook vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="cda90-209">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="cda90-210">In het volgende voorbeeld wordt een virtuele machine ontwikkelt:</span><span class="sxs-lookup"><span data-stu-id="cda90-210">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="cda90-211">Als u een label van een resourcegroep verwijderen wilt, verwijdert u de *VMName* parameter van de hash $params tabel als volgt:</span><span class="sxs-lookup"><span data-stu-id="cda90-211">If you’re removing a tag from a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="cda90-212">Uitvoeren van het runbook verwijderen ResourceSchedule om de code van de planning te verwijderen:</span><span class="sxs-lookup"><span data-stu-id="cda90-212">Execute the Remove-ResourceSchedule runbook to remove the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="cda90-213">Uitvoeren voor het bijwerken van een resourcegroep of code van de virtuele machine, het runbook verwijderen ResourceSchedule met de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="cda90-213">To update a resource group or virtual machine tag, execute the Remove-ResourceSchedule runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="cda90-214">We raden aan dat u proactief bewaken deze runbooks (en de status van de virtuele machines) om te controleren of uw virtuele machines wordt afgesloten omlaag en dienovereenkomstig gestart.</span><span class="sxs-lookup"><span data-stu-id="cda90-214">We recommend that you proactively monitor these runbooks (and the virtual machine states) to verify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="cda90-215">Om de details van de Test-ResourceSchedule runbooktaak weergeven in de Azure portal, selecteer de **taken** tegel van het runbook.</span><span class="sxs-lookup"><span data-stu-id="cda90-215">To view the details of the Test-ResourceSchedule runbook job in the Azure portal, select the **Jobs** tile of the runbook.</span></span> <span data-ttu-id="cda90-216">Het taakoverzicht geeft de invoerparameters en de uitvoerstroom weer, naast algemene informatie over de taak en eventuele uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="cda90-216">The job summary displays the input parameters and the output stream, in addition to general information about the job and any exceptions if they occurred.</span></span>

<span data-ttu-id="cda90-217">Het **Taakoverzicht** bevat berichten van de uitvoer-, waarschuwings- en foutstromen.</span><span class="sxs-lookup"><span data-stu-id="cda90-217">The **Job Summary** includes messages from the output, warning, and error streams.</span></span> <span data-ttu-id="cda90-218">Selecteer de tegel **Uitvoer** om gedetailleerde resultaten van de uitvoering van het runbook weer te geven.</span><span class="sxs-lookup"><span data-stu-id="cda90-218">Select the **Output** tile to view detailed results from the runbook execution.</span></span>

![Test ResourceSchedule uitvoer](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="cda90-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cda90-220">Next steps</span></span>
* <span data-ttu-id="cda90-221">Zie [Mijn eerste PowerShell Workflow-runbook](automation-first-runbook-textual.md) om aan de slag te gaan met PowerShell Workflow-runbooks</span><span class="sxs-lookup"><span data-stu-id="cda90-221">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="cda90-222">Zie voor meer informatie over runbooktypen, en hun voordelen en beperkingen, [Azure Automation-runbooktypen](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="cda90-222">To learn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="cda90-223">Zie voor meer informatie over PowerShell-script ondersteuningsfuncties [systeemeigen PowerShell-scriptondersteuning in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span><span class="sxs-lookup"><span data-stu-id="cda90-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="cda90-224">Zie voor meer informatie over logboekregistratie van runbook- en uitvoer, [Runbook uitvoer en berichten in Azure Automation](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="cda90-224">To learn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="cda90-225">Zie voor meer informatie over een Azure uitvoeren als-account en uw runbooks verifiëren met behulp van deze [runbooks met Azure uitvoeren als-account verifiëren](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="cda90-225">To learn more about an Azure Run As account and how to authenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
