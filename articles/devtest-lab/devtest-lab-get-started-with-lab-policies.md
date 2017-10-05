---
title: Beheer van basic lab-beleid in Azure DevTest Labs | Microsoft Docs
description: Informatie over het aantal basic-beleid (instellingen) voor een testomgeving instellen in DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: ed35d081b191ec41ed9e5970515057a4715c0d59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="2f886-103">Basic beleid beheren voor een testomgeving in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2f886-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="2f886-104">Azure DevTest Labs kunt u kosten te beheren en afval in uw labs minimaliseren door het beleid (instellingen) voor elke lab beheren.</span><span class="sxs-lookup"><span data-stu-id="2f886-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="2f886-105">In dit artikel leert u aan de slag met beleid door leren hoe u kunt twee van de meest kritieke beleidsregels instellen - het aantal virtuele machines (VM) die kan worden gemaakt of door een enkele gebruiker geclaimd beperken en automatisch afsluiten te configureren.</span><span class="sxs-lookup"><span data-stu-id="2f886-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="2f886-106">Om weer te geven hoe elk lab beleid instelt, Zie het artikel [labbeleidsregels definiëren in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="2f886-106">To view how to set every lab policy, see the article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="2f886-107">Toegang tot een lab-beleid in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2f886-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="2f886-108">De volgende stappen begeleiden u bij het instellen van beleidsregels voor een testomgeving in Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="2f886-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="2f886-109">Als u wilt weergeven (en wijzigen) op het beleid voor een testomgeving, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2f886-109">To view (and change) the policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="2f886-110">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2f886-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="2f886-111">Selecteer **Meer services** en selecteer in de lijst vervolgens **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="2f886-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="2f886-112">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="2f886-112">From the list of labs, select the desired lab.</span></span>   

1. <span data-ttu-id="2f886-113">Selecteer **configuratie en het beleid**.</span><span class="sxs-lookup"><span data-stu-id="2f886-113">Select **Configuration and policies**.</span></span>

    ![Blade beleidsinstellingen](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="2f886-115">De **configuratie en het beleid** blade bevat een menu met instellingen die u kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="2f886-115">The **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="2f886-116">Dit artikel behandelt alleen de instellingen voor **virtuele machines per gebruiker** en **automatisch afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="2f886-116">This article covers only the settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="2f886-117">Zie voor meer informatie over de overige instellingen, [beheren van alle beleidsregels voor een testomgeving in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="2f886-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="2f886-118">Set virtuele machines per gebruiker</span><span class="sxs-lookup"><span data-stu-id="2f886-118">Set virtual machines per user</span></span>
<span data-ttu-id="2f886-119">Het beleid voor **virtuele machines per gebruiker** kunt u het maximum aantal VM's die kunnen worden gemaakt door een afzonderlijke gebruiker opgeven.</span><span class="sxs-lookup"><span data-stu-id="2f886-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="2f886-120">Als een gebruiker probeert te maken of een virtuele machine wanneer de gebruikerslimiet is bereikt, wordt een foutbericht geeft aan dat de virtuele machine kan niet gemaakt/geclaimd worden.</span><span class="sxs-lookup"><span data-stu-id="2f886-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="2f886-121">Op de testomgeving **configuratie en het beleid** selecteert u **virtuele machines per gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="2f886-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Virtuele machines per gebruiker](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="2f886-123">Selecteer **Ja** beperken het aantal virtuele machines per gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2f886-123">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="2f886-124">Als u niet beperken het aantal virtuele machines per gebruiker wilt, schakelt u **Nee**.</span><span class="sxs-lookup"><span data-stu-id="2f886-124">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="2f886-125">Als u selecteert **Ja**, Geef een numerieke waarde die aangeeft van het maximum aantal VM's die kunnen worden gemaakt of door een gebruiker geclaimd.</span><span class="sxs-lookup"><span data-stu-id="2f886-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="2f886-126">Selecteer **Ja** beperken het aantal virtuele machines met SSD (SSD-schijf).</span><span class="sxs-lookup"><span data-stu-id="2f886-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="2f886-127">Als u niet wilt beperken het aantal virtuele machines die gebruik van SSD **Nee**.</span><span class="sxs-lookup"><span data-stu-id="2f886-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="2f886-128">Als u selecteert **Ja**, voer een waarde die het maximum aantal VM's die kunnen worden gemaakt met SSD aangeeft.</span><span class="sxs-lookup"><span data-stu-id="2f886-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="2f886-129">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2f886-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="2f886-130">Stel automatisch afsluiten</span><span class="sxs-lookup"><span data-stu-id="2f886-130">Set auto-shutdown</span></span>
<span data-ttu-id="2f886-131">Het beleid voor automatisch afsluiten helpt te minimaliseren lab verspilling doordat u de tijd die dit lab virtuele machines afsluiten opgeven.</span><span class="sxs-lookup"><span data-stu-id="2f886-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="2f886-132">Op de testomgeving **configuratie en het beleid** blade Selecteer **automatisch afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="2f886-132">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Automatisch afsluiten](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="2f886-134">Selecteer **op** waarmee dit beleid en **uit** dat u deze uitschakelt.</span><span class="sxs-lookup"><span data-stu-id="2f886-134">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="2f886-135">Als u dit beleid inschakelt, geef de tijd (en tijdzone) de alle VM's in het huidige lab af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="2f886-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="2f886-136">Geef **Ja** of **Nee** voor de optie een melding te verzenden 15 minuten voordat de tijd opgegeven automatisch afsluiten.</span><span class="sxs-lookup"><span data-stu-id="2f886-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="2f886-137">Als u opgeeft **Ja**, voer een webhook-URL-eindpunt voor het ontvangen van de melding.</span><span class="sxs-lookup"><span data-stu-id="2f886-137">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="2f886-138">Zie voor meer informatie over webhooks [maken van een webhook of API-functie voor Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="2f886-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="2f886-139">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2f886-139">Select **Save**.</span></span>

    <span data-ttu-id="2f886-140">Eenmaal is ingeschakeld, geldt dit beleid voor alle VM's in het huidige lab.</span><span class="sxs-lookup"><span data-stu-id="2f886-140">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="2f886-141">Als deze instelling uit een specifieke virtuele machine verwijderen, de VM-blade open en wijzig de **automatisch afsluiten** instelling</span><span class="sxs-lookup"><span data-stu-id="2f886-141">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="2f886-142">Set automatisch starten</span><span class="sxs-lookup"><span data-stu-id="2f886-142">Set auto-start</span></span>
<span data-ttu-id="2f886-143">Het beleid voor automatisch starten, kunt u opgeven wanneer de virtuele machines in het huidige lab moeten worden gestart.</span><span class="sxs-lookup"><span data-stu-id="2f886-143">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="2f886-144">Op de testomgeving **configuratie en het beleid** blade Selecteer **automatisch starten**.</span><span class="sxs-lookup"><span data-stu-id="2f886-144">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Automatisch starten](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="2f886-146">Selecteer **op** waarmee dit beleid en **uit** dat u deze uitschakelt.</span><span class="sxs-lookup"><span data-stu-id="2f886-146">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="2f886-147">Als u dit beleid inschakelt, geeft u het geplande begintijdstip, tijdzone en de dagen van de week waarop de tijd van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="2f886-147">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="2f886-148">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2f886-148">Select **Save**.</span></span>

    <span data-ttu-id="2f886-149">Eenmaal is ingeschakeld, wordt dit beleid niet automatisch toegepast op alle virtuele machines in het huidige lab.</span><span class="sxs-lookup"><span data-stu-id="2f886-149">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="2f886-150">Als u wilt deze instelling toepast op een specifieke virtuele machine, van de VM-blade open en wijzig de **automatisch starten** instelling</span><span class="sxs-lookup"><span data-stu-id="2f886-150">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2f886-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f886-151">Next steps</span></span>

- <span data-ttu-id="2f886-152">[Labbeleidsregels definiëren in Azure DevTest Labs](devtest-lab-set-lab-policy.md) -informatie over het aanpassen van andere labbeleidsregels</span><span class="sxs-lookup"><span data-stu-id="2f886-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies</span></span> 
