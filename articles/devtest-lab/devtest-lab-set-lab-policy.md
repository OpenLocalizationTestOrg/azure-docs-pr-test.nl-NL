---
title: labbeleidsregels aaaManage in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe toodefine labbeleidsregels zoals VM-groottes, maximum aantal virtuele machines per gebruiker, en automatisering afsluiten.
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
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="c9c39-103">Alle beleidsregels voor een testomgeving in Azure DevTest Labs beheren</span><span class="sxs-lookup"><span data-stu-id="c9c39-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="c9c39-104">Azure DevTest Labs kunt u de kosten te beheren en afval in uw labs minimaliseren door het beleid (instellingen) beheren voor elke lab.</span><span class="sxs-lookup"><span data-stu-id="c9c39-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="c9c39-105">In dit artikel wordt stapsgewijs gedetailleerd uitgelegd hoe tooset elk beleid.</span><span class="sxs-lookup"><span data-stu-id="c9c39-105">This article explains in step-by-step detail how tooset each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="c9c39-106">Set toegestane grootten van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="c9c39-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="c9c39-107">Hallo toegestaan-beleid voor instelling Hallo VM-grootten helpt toominimize lab afval doordat u toospecify welke VM-grootten zijn toegestaan in Hallo lab.</span><span class="sxs-lookup"><span data-stu-id="c9c39-107">hello policy for setting hello allowed VM sizes helps toominimize lab waste by enabling you toospecify which VM sizes are allowed in hello lab.</span></span> <span data-ttu-id="c9c39-108">Als dit beleid is geactiveerd, zijn alleen VM-grootten uit deze lijst gebruikte toocreate virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c9c39-108">If this policy is activated, only VM sizes from this list can be used toocreate VMs.</span></span>

1. <span data-ttu-id="c9c39-109">Op de Hallo lab **configuratie en het beleid** blade Selecteer **toegestane grootten voor virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-109">On hello lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Grootten van de toegestane virtuele machines](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="c9c39-111">Selecteer **op** tooenable dit beleid en **uit** toodisable deze.</span><span class="sxs-lookup"><span data-stu-id="c9c39-111">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="c9c39-112">Als u dit beleid inschakelt, selecteert u een of meer VM-grootten die kunnen worden gemaakt in uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c9c39-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="c9c39-113">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="c9c39-114">Set virtuele machines per gebruiker</span><span class="sxs-lookup"><span data-stu-id="c9c39-114">Set virtual machines per user</span></span>
<span data-ttu-id="c9c39-115">beleid voor Hallo **virtuele machines per gebruiker** kunt u toospecify Hallo maximum aantal VM's die kunnen worden gemaakt door een afzonderlijke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c9c39-115">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="c9c39-116">Als een gebruiker probeert toocreate of claim een virtuele machine wanneer Hallo gebruikerslimiet is bereikt, wordt een foutbericht dat Hallo die VM kan niet worden gemaakt/geclaimd aangeeft.</span><span class="sxs-lookup"><span data-stu-id="c9c39-116">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="c9c39-117">Op de Hallo lab **configuratie en het beleid** selecteert u **virtuele machines per gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-117">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Virtuele machines per gebruiker](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="c9c39-119">Selecteer **Ja** toolimit Hallo aantal virtuele machines per gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c9c39-119">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="c9c39-120">Als u niet dat toolimit Hallo aantal virtuele machines per gebruiker wilt, schakelt u **Nee**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-120">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="c9c39-121">Als u selecteert **Ja**, Geef een numerieke waarde die aangeeft Hallo kunt u het maximum aantal VM's die kunnen worden gemaakt of door een gebruiker geclaimd.</span><span class="sxs-lookup"><span data-stu-id="c9c39-121">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="c9c39-122">Selecteer **Ja** toolimit Hallo aantal virtuele machines met SSD (SSD-schijf).</span><span class="sxs-lookup"><span data-stu-id="c9c39-122">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="c9c39-123">Als u niet dat toolimit Hallo aantal virtuele machines die SSD gebruiken wilt kunt, selecteert u **Nee**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-123">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="c9c39-124">Als u selecteert **Ja**, voer een waarde die aangeeft Hallo kunt u het maximum aantal VM's die kunnen worden gemaakt met SSD.</span><span class="sxs-lookup"><span data-stu-id="c9c39-124">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="c9c39-125">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="c9c39-126">Set virtuele machines per lab</span><span class="sxs-lookup"><span data-stu-id="c9c39-126">Set virtual machines per lab</span></span>
<span data-ttu-id="c9c39-127">beleid voor Hallo **virtuele machines per lab** kunt u toospecify Hallo maximum aantal VM's die kunnen worden gemaakt voor de huidige lab Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9c39-127">hello policy for **Virtual machines per lab** allows you toospecify hello maximum number of VMs that can be created for hello current lab.</span></span> <span data-ttu-id="c9c39-128">Als een gebruiker een virtuele machine toocreate probeert wanneer Hallo lab limiet is bereikt, geeft een foutbericht weergegeven dat Hallo die VM kan niet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c9c39-128">If a user attempts toocreate a VM when hello lab limit has been met, an error message indicates that hello VM cannot be created.</span></span> 

1. <span data-ttu-id="c9c39-129">Op de Hallo lab **configuratie en het beleid** selecteert u **virtuele machines per lab**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-129">On hello lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Virtuele machines per lab](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="c9c39-131">Selecteer **Ja** toolimit Hallo aantal virtuele machines per lab.</span><span class="sxs-lookup"><span data-stu-id="c9c39-131">Select **Yes** toolimit hello number of VMs per lab.</span></span> <span data-ttu-id="c9c39-132">Als u niet dat toolimit Hallo aantal virtuele machines per lab wilt, selecteert u **Nee**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-132">If you do not want toolimit hello number of VMs per lab, select **No**.</span></span> <span data-ttu-id="c9c39-133">Als u selecteert **Ja**, Geef een numerieke waarde die aangeeft Hallo kunt u het maximum aantal VM's die kunnen worden gemaakt of door een gebruiker geclaimd.</span><span class="sxs-lookup"><span data-stu-id="c9c39-133">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="c9c39-134">Selecteer **Ja** toolimit Hallo aantal virtuele machines met SSD (SSD-schijf).</span><span class="sxs-lookup"><span data-stu-id="c9c39-134">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="c9c39-135">Als u niet dat toolimit Hallo aantal virtuele machines die SSD gebruiken wilt kunt, selecteert u **Nee**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-135">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="c9c39-136">Als u selecteert **Ja**, voer een waarde die aangeeft Hallo kunt u het maximum aantal VM's die kunnen worden gemaakt met SSD.</span><span class="sxs-lookup"><span data-stu-id="c9c39-136">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="c9c39-137">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="c9c39-138">Stel automatisch afsluiten</span><span class="sxs-lookup"><span data-stu-id="c9c39-138">Set auto-shutdown</span></span>
<span data-ttu-id="c9c39-139">Hallo automatisch afsluiten beleid helpt toominimize lab afval doordat u toospecify Hallo wanneer dit lab VMs afgesloten.</span><span class="sxs-lookup"><span data-stu-id="c9c39-139">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="c9c39-140">Op de Hallo lab **configuratie en het beleid** blade Selecteer **automatisch afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-140">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Automatisch afsluiten](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="c9c39-142">Selecteer **op** tooenable dit beleid en **uit** toodisable deze.</span><span class="sxs-lookup"><span data-stu-id="c9c39-142">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="c9c39-143">Als u dit beleid inschakelt, geef Hallo tijd (en tijdzone) tooshut omlaag alle VM's in de huidige lab Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9c39-143">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="c9c39-144">Geef **Ja** of **Nee** voor Hallo optie toosend een melding 15 minuten voorafgaande toohello automatisch afsluiten tijd opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c9c39-144">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="c9c39-145">Als u opgeeft **Ja**, voer een webhook-URL-eindpunt tooreceive Hallo melding.</span><span class="sxs-lookup"><span data-stu-id="c9c39-145">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="c9c39-146">Zie voor meer informatie over webhooks [maken van een webhook of API-functie voor Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="c9c39-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="c9c39-147">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-147">Select **Save**.</span></span>

    <span data-ttu-id="c9c39-148">Standaard eenmaal is ingeschakeld, geldt dit beleid tooall virtuele machines in de huidige lab Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9c39-148">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="c9c39-149">Deze instelling van een specifieke virtuele machine, opent u tooremove Hallo van de virtuele machine blade en wijzig de **automatisch afsluiten** instelling</span><span class="sxs-lookup"><span data-stu-id="c9c39-149">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="c9c39-150">Set automatisch starten</span><span class="sxs-lookup"><span data-stu-id="c9c39-150">Set auto-start</span></span>
<span data-ttu-id="c9c39-151">Hallo automatisch starten van beleid kunt u toospecify wanneer Hallo virtuele machines in de huidige lab Hallo moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="c9c39-151">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="c9c39-152">Op het Hallo lab **configuratie en het beleid** blade Selecteer **automatisch starten**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-152">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Automatisch starten](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="c9c39-154">Selecteer **op** tooenable dit beleid en **uit** toodisable deze.</span><span class="sxs-lookup"><span data-stu-id="c9c39-154">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="c9c39-155">Als u dit beleid inschakelt, geef Hallo geplande begintijd, tijdzone en Hallo dagen van de week van Hallo welke Hallo tijd van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="c9c39-155">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="c9c39-156">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c9c39-156">Select **Save**.</span></span>

    <span data-ttu-id="c9c39-157">Eenmaal is ingeschakeld, dit beleid is niet automatisch toegepast tooany virtuele machines in de huidige lab Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9c39-157">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="c9c39-158">tooapply deze instelling tooa specifieke virtuele machine, blade van open Hallo van de virtuele machine en wijzig de **automatisch starten** instelling</span><span class="sxs-lookup"><span data-stu-id="c9c39-158">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="c9c39-159">Verloopdatum instellen</span><span class="sxs-lookup"><span data-stu-id="c9c39-159">Set expiration date</span></span>
<span data-ttu-id="c9c39-160">U kunt een vervaldatum instellen datum wanneer u [Hallo VM maken](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="c9c39-160">You can set an expiration date when you [create hello VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="c9c39-161">In **geavanceerde instellingen**, kies Hallo kalender pictogram toospecify een datum waarop Hallo VM automatisch worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c9c39-161">In **Advanced settings**, choose hello calendar icon toospecify a date on which hello VM will be automatically deleted.</span></span>  <span data-ttu-id="c9c39-162">Standaard Hallo VM nooit verloopt.</span><span class="sxs-lookup"><span data-stu-id="c9c39-162">By default, hello VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="c9c39-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9c39-163">Next steps</span></span>
<span data-ttu-id="c9c39-164">Zodra u hebt gedefinieerd en toegepast Hallo van verschillende instellingen voor virtuele machine voor uw testomgeving, Hier vindt u enkele dingen tootry volgende:</span><span class="sxs-lookup"><span data-stu-id="c9c39-164">Once you've defined and applied hello various VM policy settings for your lab, here are some things tootry next:</span></span>

* <span data-ttu-id="c9c39-165">[Gedeelde IP-adressen begrijpen](devtest-lab-shared-ip.md) -wordt uitgelegd hoe gedeelde IP adressen worden gebruikt in DevTest Labs toominimize Hallo aantal openbare IP-adressen vereist tooconnect tooyour lab virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c9c39-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs toominimize hello number of public IP addresses required tooconnect tooyour lab VMs.</span></span>
* <span data-ttu-id="c9c39-166">[Kostenbeheer van configureren](devtest-lab-configure-cost-management.md) -illustreert hoe toouse hello **maandelijkse geschatte kosten Trend** grafiek</span><span class="sxs-lookup"><span data-stu-id="c9c39-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how toouse hello **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="c9c39-167">tooview Hallo maand geschatte kosten-to-date en Hallo geprojecteerd einde van de maand kosten.</span><span class="sxs-lookup"><span data-stu-id="c9c39-167">tooview hello current month's estimated cost-to-date and hello projected end-of-month cost.</span></span>
* <span data-ttu-id="c9c39-168">[Maken van aangepaste installatiekopie](devtest-lab-create-template.md) : wanneer u een virtuele machine, maakt u een basis, kan dit een aangepaste installatiekopie of een Marketplace-installatiekopie opgeven.</span><span class="sxs-lookup"><span data-stu-id="c9c39-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="c9c39-169">In dit artikel ziet u hoe toocreate een aangepaste installatiekopie van een VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="c9c39-169">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="c9c39-170">[Configureren van installatiekopieën van Marketplace](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs ondersteunt het maken van virtuele machines op basis van Azure Marketplace-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="c9c39-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="c9c39-171">Dit artikel wordt beschreven hoe toospecify die, indien aanwezig, Azure Marketplace-installatiekopieën kunnen worden gebruikt bij het maken van virtuele machines in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c9c39-171">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="c9c39-172">[Een virtuele machine maken in een testomgeving](devtest-lab-add-vm-with-artifacts.md) -ziet u hoe een virtuele machine uit een basisinstallatiekopie toocreate (ofwel aangepaste of Marketplace), en hoe toowork met artefacten in uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c9c39-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

