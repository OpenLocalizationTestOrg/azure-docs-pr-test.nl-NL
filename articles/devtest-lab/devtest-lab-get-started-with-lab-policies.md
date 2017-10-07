---
title: basic labbeleidsregels aaaManage in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe tooset aantal basic Hallo-beleid (instellingen) voor een testomgeving in DevTest Labs
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
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="b786b-103">Basic beleid beheren voor een testomgeving in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b786b-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="b786b-104">Azure DevTest Labs kunt u toocontrol kosten en afval in uw labs minimaliseren door het beleid (instellingen) beheren voor elke lab.</span><span class="sxs-lookup"><span data-stu-id="b786b-104">Azure DevTest Labs enables you toocontrol cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="b786b-105">In dit artikel leert u aan de slag met beleid door te leren hoe tooset twee van de meest kritieke beleidsregels Hallo - beperken Hallo aantal virtuele machines (VM) die kan worden gemaakt of door een afzonderlijke gebruiker en automatisch afsluiten configureren geclaimd.</span><span class="sxs-lookup"><span data-stu-id="b786b-105">In this article, you get started with policies by learning how tooset two of hello most critical policies - limiting hello number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="b786b-106">tooview hoe tooset elk beleid lab Zie Hallo artikel [labbeleidsregels definiëren in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b786b-106">tooview how tooset every lab policy, see hello article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="b786b-107">Toegang tot een lab-beleid in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b786b-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="b786b-108">Hallo volgende stappen begeleiden u door het instellen van beleidsregels voor een testomgeving in Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="b786b-108">hello following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="b786b-109">tooview (en wijzigen) Hallo beleidsregels voor een testomgeving, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="b786b-109">tooview (and change) hello policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="b786b-110">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b786b-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="b786b-111">Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="b786b-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="b786b-112">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="b786b-112">From hello list of labs, select hello desired lab.</span></span>   

1. <span data-ttu-id="b786b-113">Selecteer **configuratie en het beleid**.</span><span class="sxs-lookup"><span data-stu-id="b786b-113">Select **Configuration and policies**.</span></span>

    ![Blade beleidsinstellingen](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="b786b-115">Hallo **configuratie en het beleid** blade bevat een menu met instellingen die u kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="b786b-115">hello **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="b786b-116">Dit artikel behandelt alleen Hallo instellingen voor **virtuele machines per gebruiker** en **automatisch afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="b786b-116">This article covers only hello settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="b786b-117">toolearn over Hallo resterende instellingen, Zie [beheren van alle beleidsregels voor een testomgeving in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b786b-117">toolearn about hello remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="b786b-118">Set virtuele machines per gebruiker</span><span class="sxs-lookup"><span data-stu-id="b786b-118">Set virtual machines per user</span></span>
<span data-ttu-id="b786b-119">beleid voor Hallo **virtuele machines per gebruiker** kunt u toospecify Hallo maximum aantal VM's die kunnen worden gemaakt door een afzonderlijke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b786b-119">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="b786b-120">Als een gebruiker probeert toocreate of claim een virtuele machine wanneer Hallo gebruikerslimiet is bereikt, wordt een foutbericht dat Hallo die VM kan niet worden gemaakt/geclaimd aangeeft.</span><span class="sxs-lookup"><span data-stu-id="b786b-120">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="b786b-121">Op de Hallo lab **configuratie en het beleid** selecteert u **virtuele machines per gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="b786b-121">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Virtuele machines per gebruiker](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="b786b-123">Selecteer **Ja** toolimit Hallo aantal virtuele machines per gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b786b-123">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="b786b-124">Als u niet dat toolimit Hallo aantal virtuele machines per gebruiker wilt, schakelt u **Nee**.</span><span class="sxs-lookup"><span data-stu-id="b786b-124">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="b786b-125">Als u selecteert **Ja**, Geef een numerieke waarde die aangeeft Hallo kunt u het maximum aantal VM's die kunnen worden gemaakt of door een gebruiker geclaimd.</span><span class="sxs-lookup"><span data-stu-id="b786b-125">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="b786b-126">Selecteer **Ja** toolimit Hallo aantal virtuele machines met SSD (SSD-schijf).</span><span class="sxs-lookup"><span data-stu-id="b786b-126">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="b786b-127">Als u niet dat toolimit Hallo aantal virtuele machines die SSD gebruiken wilt kunt, selecteert u **Nee**.</span><span class="sxs-lookup"><span data-stu-id="b786b-127">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="b786b-128">Als u selecteert **Ja**, voer een waarde die aangeeft Hallo kunt u het maximum aantal VM's die kunnen worden gemaakt met SSD.</span><span class="sxs-lookup"><span data-stu-id="b786b-128">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="b786b-129">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b786b-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="b786b-130">Stel automatisch afsluiten</span><span class="sxs-lookup"><span data-stu-id="b786b-130">Set auto-shutdown</span></span>
<span data-ttu-id="b786b-131">Hallo automatisch afsluiten beleid helpt toominimize lab afval doordat u toospecify Hallo wanneer dit lab VMs afgesloten.</span><span class="sxs-lookup"><span data-stu-id="b786b-131">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="b786b-132">Op de Hallo lab **configuratie en het beleid** blade Selecteer **automatisch afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="b786b-132">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Automatisch afsluiten](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="b786b-134">Selecteer **op** tooenable dit beleid en **uit** toodisable deze.</span><span class="sxs-lookup"><span data-stu-id="b786b-134">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="b786b-135">Als u dit beleid inschakelt, geef Hallo tijd (en tijdzone) tooshut omlaag alle VM's in de huidige lab Hallo.</span><span class="sxs-lookup"><span data-stu-id="b786b-135">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="b786b-136">Geef **Ja** of **Nee** voor Hallo optie toosend een melding 15 minuten voorafgaande toohello automatisch afsluiten tijd opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b786b-136">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="b786b-137">Als u opgeeft **Ja**, voer een webhook-URL-eindpunt tooreceive Hallo melding.</span><span class="sxs-lookup"><span data-stu-id="b786b-137">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="b786b-138">Zie voor meer informatie over webhooks [maken van een webhook of API-functie voor Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="b786b-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="b786b-139">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b786b-139">Select **Save**.</span></span>

    <span data-ttu-id="b786b-140">Standaard eenmaal is ingeschakeld, geldt dit beleid tooall virtuele machines in de huidige lab Hallo.</span><span class="sxs-lookup"><span data-stu-id="b786b-140">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="b786b-141">Deze instelling van een specifieke virtuele machine, opent u tooremove Hallo van de virtuele machine blade en wijzig de **automatisch afsluiten** instelling</span><span class="sxs-lookup"><span data-stu-id="b786b-141">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="b786b-142">Set automatisch starten</span><span class="sxs-lookup"><span data-stu-id="b786b-142">Set auto-start</span></span>
<span data-ttu-id="b786b-143">Hallo automatisch starten van beleid kunt u toospecify wanneer Hallo virtuele machines in de huidige lab Hallo moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="b786b-143">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="b786b-144">Op het Hallo lab **configuratie en het beleid** blade Selecteer **automatisch starten**.</span><span class="sxs-lookup"><span data-stu-id="b786b-144">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Automatisch starten](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="b786b-146">Selecteer **op** tooenable dit beleid en **uit** toodisable deze.</span><span class="sxs-lookup"><span data-stu-id="b786b-146">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="b786b-147">Als u dit beleid inschakelt, geef Hallo geplande begintijd, tijdzone en Hallo dagen van de week van Hallo welke Hallo tijd van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="b786b-147">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="b786b-148">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b786b-148">Select **Save**.</span></span>

    <span data-ttu-id="b786b-149">Eenmaal is ingeschakeld, dit beleid is niet automatisch toegepast tooany virtuele machines in de huidige lab Hallo.</span><span class="sxs-lookup"><span data-stu-id="b786b-149">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="b786b-150">tooapply deze instelling tooa specifieke virtuele machine, blade van open Hallo van de virtuele machine en wijzig de **automatisch starten** instelling</span><span class="sxs-lookup"><span data-stu-id="b786b-150">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b786b-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b786b-151">Next steps</span></span>

- <span data-ttu-id="b786b-152">[Labbeleidsregels definiëren in Azure DevTest Labs](devtest-lab-set-lab-policy.md) -informatie over hoe toomodify andere labbeleidsregels</span><span class="sxs-lookup"><span data-stu-id="b786b-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how toomodify other lab policies</span></span> 
