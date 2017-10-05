---
title: Beheer van lab-beleid in Azure DevTest Labs | Microsoft Docs
description: "Informatie over het lab beleid zoals VM-grootten, maximum aantal virtuele machines per gebruiker en afsluiten automation definiëren."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 328a4d893637d7150807855e118b485a2c3bbfc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="90a81-103">Alle beleidsregels voor een testomgeving in Azure DevTest Labs beheren</span><span class="sxs-lookup"><span data-stu-id="90a81-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="90a81-104">Azure DevTest Labs kunt u de kosten te beheren en afval in uw labs minimaliseren door het beleid (instellingen) beheren voor elke lab.</span><span class="sxs-lookup"><span data-stu-id="90a81-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="90a81-105">In dit artikel stapsgewijze wordt gedetailleerd uitgelegd hoe u elk beleid instelt.</span><span class="sxs-lookup"><span data-stu-id="90a81-105">This article explains in step-by-step detail how to set each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="90a81-106">Set toegestane grootten van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="90a81-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="90a81-107">Het beleid voor het instellen van de toegestane VM-grootten helpt te minimaliseren lab verspilling kunt u opgeven welke VM-grootten zijn toegestaan in de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="90a81-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span></span> <span data-ttu-id="90a81-108">Als dit beleid is geactiveerd, kan alleen VM-grootten uit deze lijst kunnen worden gebruikt voor het maken van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="90a81-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span></span>

1. <span data-ttu-id="90a81-109">Op de testomgeving **configuratie en het beleid** blade Selecteer **toegestane grootten voor virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="90a81-109">On the lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Grootten van de toegestane virtuele machines](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="90a81-111">Selecteer **op** waarmee dit beleid en **uit** dat u deze uitschakelt.</span><span class="sxs-lookup"><span data-stu-id="90a81-111">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="90a81-112">Als u dit beleid inschakelt, selecteert u een of meer VM-grootten die kunnen worden gemaakt in uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="90a81-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="90a81-113">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="90a81-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="90a81-114">Set virtuele machines per gebruiker</span><span class="sxs-lookup"><span data-stu-id="90a81-114">Set virtual machines per user</span></span>
<span data-ttu-id="90a81-115">Het beleid voor **virtuele machines per gebruiker** kunt u het maximum aantal VM's die kunnen worden gemaakt door een afzonderlijke gebruiker opgeven.</span><span class="sxs-lookup"><span data-stu-id="90a81-115">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="90a81-116">Als een gebruiker probeert te maken of een virtuele machine wanneer de gebruikerslimiet is bereikt, wordt een foutbericht geeft aan dat de virtuele machine kan niet gemaakt/geclaimd worden.</span><span class="sxs-lookup"><span data-stu-id="90a81-116">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="90a81-117">Op de testomgeving **configuratie en het beleid** selecteert u **virtuele machines per gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="90a81-117">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Virtuele machines per gebruiker](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="90a81-119">Selecteer **Ja** beperken het aantal virtuele machines per gebruiker.</span><span class="sxs-lookup"><span data-stu-id="90a81-119">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="90a81-120">Als u niet beperken het aantal virtuele machines per gebruiker wilt, schakelt u **Nee**.</span><span class="sxs-lookup"><span data-stu-id="90a81-120">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="90a81-121">Als u selecteert **Ja**, Geef een numerieke waarde die aangeeft van het maximum aantal VM's die kunnen worden gemaakt of door een gebruiker geclaimd.</span><span class="sxs-lookup"><span data-stu-id="90a81-121">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="90a81-122">Selecteer **Ja** beperken het aantal virtuele machines met SSD (SSD-schijf).</span><span class="sxs-lookup"><span data-stu-id="90a81-122">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="90a81-123">Als u niet wilt beperken het aantal virtuele machines die gebruik van SSD **Nee**.</span><span class="sxs-lookup"><span data-stu-id="90a81-123">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="90a81-124">Als u selecteert **Ja**, voer een waarde die het maximum aantal VM's die kunnen worden gemaakt met SSD aangeeft.</span><span class="sxs-lookup"><span data-stu-id="90a81-124">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="90a81-125">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="90a81-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="90a81-126">Set virtuele machines per lab</span><span class="sxs-lookup"><span data-stu-id="90a81-126">Set virtual machines per lab</span></span>
<span data-ttu-id="90a81-127">Het beleid voor **virtuele machines per lab** kunt u het maximum aantal VM's die kunnen worden gemaakt voor het huidige lab opgeven.</span><span class="sxs-lookup"><span data-stu-id="90a81-127">The policy for **Virtual machines per lab** allows you to specify the maximum number of VMs that can be created for the current lab.</span></span> <span data-ttu-id="90a81-128">Als een gebruiker een virtuele machine maken probeert wanneer de limiet van het lab is voldaan, wordt een foutbericht geeft aan dat de virtuele machine kan niet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="90a81-128">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span></span> 

1. <span data-ttu-id="90a81-129">Op de testomgeving **configuratie en het beleid** selecteert u **virtuele machines per lab**.</span><span class="sxs-lookup"><span data-stu-id="90a81-129">On the lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Virtuele machines per lab](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="90a81-131">Selecteer **Ja** beperken het aantal virtuele machines per lab.</span><span class="sxs-lookup"><span data-stu-id="90a81-131">Select **Yes** to limit the number of VMs per lab.</span></span> <span data-ttu-id="90a81-132">Als u niet beperken het aantal virtuele machines per lab wilt, selecteert u **Nee**.</span><span class="sxs-lookup"><span data-stu-id="90a81-132">If you do not want to limit the number of VMs per lab, select **No**.</span></span> <span data-ttu-id="90a81-133">Als u selecteert **Ja**, Geef een numerieke waarde die aangeeft van het maximum aantal VM's die kunnen worden gemaakt of door een gebruiker geclaimd.</span><span class="sxs-lookup"><span data-stu-id="90a81-133">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="90a81-134">Selecteer **Ja** beperken het aantal virtuele machines met SSD (SSD-schijf).</span><span class="sxs-lookup"><span data-stu-id="90a81-134">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="90a81-135">Als u niet wilt beperken het aantal virtuele machines die gebruik van SSD **Nee**.</span><span class="sxs-lookup"><span data-stu-id="90a81-135">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="90a81-136">Als u selecteert **Ja**, voer een waarde die het maximum aantal VM's die kunnen worden gemaakt met SSD aangeeft.</span><span class="sxs-lookup"><span data-stu-id="90a81-136">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="90a81-137">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="90a81-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="90a81-138">Stel automatisch afsluiten</span><span class="sxs-lookup"><span data-stu-id="90a81-138">Set auto-shutdown</span></span>
<span data-ttu-id="90a81-139">Het beleid voor automatisch afsluiten helpt te minimaliseren lab verspilling doordat u de tijd die dit lab virtuele machines afsluiten opgeven.</span><span class="sxs-lookup"><span data-stu-id="90a81-139">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="90a81-140">Op de testomgeving **configuratie en het beleid** blade Selecteer **automatisch afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="90a81-140">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Automatisch afsluiten](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="90a81-142">Selecteer **op** waarmee dit beleid en **uit** dat u deze uitschakelt.</span><span class="sxs-lookup"><span data-stu-id="90a81-142">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="90a81-143">Als u dit beleid inschakelt, geef de tijd (en tijdzone) de alle VM's in het huidige lab af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="90a81-143">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="90a81-144">Geef **Ja** of **Nee** voor de optie een melding te verzenden 15 minuten voordat de tijd opgegeven automatisch afsluiten.</span><span class="sxs-lookup"><span data-stu-id="90a81-144">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="90a81-145">Als u opgeeft **Ja**, voer een webhook-URL-eindpunt voor het ontvangen van de melding.</span><span class="sxs-lookup"><span data-stu-id="90a81-145">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="90a81-146">Zie voor meer informatie over webhooks [maken van een webhook of API-functie voor Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="90a81-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="90a81-147">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="90a81-147">Select **Save**.</span></span>

    <span data-ttu-id="90a81-148">Eenmaal is ingeschakeld, geldt dit beleid voor alle VM's in het huidige lab.</span><span class="sxs-lookup"><span data-stu-id="90a81-148">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="90a81-149">Als deze instelling uit een specifieke virtuele machine verwijderen, de VM-blade open en wijzig de **automatisch afsluiten** instelling</span><span class="sxs-lookup"><span data-stu-id="90a81-149">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="90a81-150">Set automatisch starten</span><span class="sxs-lookup"><span data-stu-id="90a81-150">Set auto-start</span></span>
<span data-ttu-id="90a81-151">Het beleid voor automatisch starten, kunt u opgeven wanneer de virtuele machines in het huidige lab moeten worden gestart.</span><span class="sxs-lookup"><span data-stu-id="90a81-151">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="90a81-152">Op de testomgeving **configuratie en het beleid** blade Selecteer **automatisch starten**.</span><span class="sxs-lookup"><span data-stu-id="90a81-152">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Automatisch starten](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="90a81-154">Selecteer **op** waarmee dit beleid en **uit** dat u deze uitschakelt.</span><span class="sxs-lookup"><span data-stu-id="90a81-154">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="90a81-155">Als u dit beleid inschakelt, geeft u het geplande begintijdstip, tijdzone en de dagen van de week waarop de tijd van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="90a81-155">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="90a81-156">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="90a81-156">Select **Save**.</span></span>

    <span data-ttu-id="90a81-157">Eenmaal is ingeschakeld, wordt dit beleid niet automatisch toegepast op alle virtuele machines in het huidige lab.</span><span class="sxs-lookup"><span data-stu-id="90a81-157">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="90a81-158">Als u wilt deze instelling toepast op een specifieke virtuele machine, van de VM-blade open en wijzig de **automatisch starten** instelling</span><span class="sxs-lookup"><span data-stu-id="90a81-158">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="90a81-159">Verloopdatum instellen</span><span class="sxs-lookup"><span data-stu-id="90a81-159">Set expiration date</span></span>
<span data-ttu-id="90a81-160">U kunt een vervaldatum instellen datum wanneer u [de virtuele machine maken](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="90a81-160">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="90a81-161">In **geavanceerde instellingen**, kies het pictogram Agenda om op te geven van een datum op waarop de virtuele machine automatisch worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="90a81-161">In **Advanced settings**, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="90a81-162">Standaard wordt de virtuele machine nooit verlopen.</span><span class="sxs-lookup"><span data-stu-id="90a81-162">By default, the VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="90a81-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="90a81-163">Next steps</span></span>
<span data-ttu-id="90a81-164">Nadat u hebt gedefinieerd en de verschillende VM-beleidsinstellingen worden toegepast op uw lab, zijn hier proberen het volgende:</span><span class="sxs-lookup"><span data-stu-id="90a81-164">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span></span>

* <span data-ttu-id="90a81-165">[Gedeelde IP-adressen begrijpen](devtest-lab-shared-ip.md) -wordt uitgelegd hoe gedeelde IP adressen worden gebruikt in DevTest Labs om het aantal openbare IP-adressen die zijn vereist om verbinding met uw lab VM's te minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="90a81-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span></span>
* <span data-ttu-id="90a81-166">[Kostenbeheer van configureren](devtest-lab-configure-cost-management.md) -laat zien hoe u de **maandelijkse geschatte kosten Trend** grafiek</span><span class="sxs-lookup"><span data-stu-id="90a81-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="90a81-167">Als u wilt weergeven van de huidige maand de geschatte kosten-to-date en de geschatte kosten van de laatste van de maand.</span><span class="sxs-lookup"><span data-stu-id="90a81-167">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span></span>
* <span data-ttu-id="90a81-168">[Maken van aangepaste installatiekopie](devtest-lab-create-template.md) : wanneer u een virtuele machine, maakt u een basis, kan dit een aangepaste installatiekopie of een Marketplace-installatiekopie opgeven.</span><span class="sxs-lookup"><span data-stu-id="90a81-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="90a81-169">In dit artikel laat zien hoe een aangepaste installatiekopie maken van een VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="90a81-169">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="90a81-170">[Configureren van installatiekopieën van Marketplace](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs ondersteunt het maken van virtuele machines op basis van Azure Marketplace-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="90a81-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="90a81-171">Dit artikel wordt beschreven hoe u kunt opgeven die, indien aanwezig, Azure Marketplace-installatiekopieën kunnen worden gebruikt bij het maken van virtuele machines in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="90a81-171">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="90a81-172">[Een virtuele machine maken in een testomgeving](devtest-lab-add-vm-with-artifacts.md) -ziet u hoe u een virtuele machine maken van een basisinstallatiekopie (een aangepaste of Marketplace), en het werken met artefacten in uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="90a81-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

