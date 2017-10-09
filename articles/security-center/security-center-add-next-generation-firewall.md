---
title: aaaAdd next generation firewall in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbevelingen ** toevoegen een volgende generatie Firewall ** en ** Route traffice via NGFW alleen **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="5126c-103">Next Generation Firewall toevoegen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="5126c-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="5126c-104">Azure Security Center kan aanbevelen dat u next generation firewall (NGFW) van een Microsoft-partner tooincrease uw beveiligingsinstellingen toevoegt.</span><span class="sxs-lookup"><span data-stu-id="5126c-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> <span data-ttu-id="5126c-105">Dit document vindt u via een voorbeeld van hoe toodo dit.</span><span class="sxs-lookup"><span data-stu-id="5126c-105">This document walks you through an example of how toodo this.</span></span>

> [!NOTE]
> <span data-ttu-id="5126c-106">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="5126c-106">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="5126c-107">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="5126c-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="5126c-108">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="5126c-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="5126c-109">In Hallo **aanbevelingen** blade Selecteer **Next Generation Firewall toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5126c-109">In hello **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="5126c-110">![Een firewall van de volgende generatie toevoegen][1]</span><span class="sxs-lookup"><span data-stu-id="5126c-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="5126c-111">In Hallo **Next Generation Firewall toevoegen** blade, selecteert u een eindpunt.</span><span class="sxs-lookup"><span data-stu-id="5126c-111">In hello **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="5126c-112">![Selecteer een eindpunt][2]</span><span class="sxs-lookup"><span data-stu-id="5126c-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="5126c-113">Een tweede **Next Generation Firewall toevoegen** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="5126c-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="5126c-114">U kunt toouse een bestaande oplossing als beschikbaar of u kunt een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="5126c-114">You can choose toouse an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="5126c-115">In dit voorbeeld zijn er geen bestaande oplossingen beschikbaar, dus we een NGFW maken.</span><span class="sxs-lookup"><span data-stu-id="5126c-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="5126c-116">![Next Generation Firewall maken][3]</span><span class="sxs-lookup"><span data-stu-id="5126c-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="5126c-117">een oplossing toocreate een NGFW selecteren in de lijst Hallo van geïntegreerde partners.</span><span class="sxs-lookup"><span data-stu-id="5126c-117">toocreate an NGFW, select a solution from hello list of integrated partners.</span></span> <span data-ttu-id="5126c-118">In dit voorbeeld selecteren we **Check Point**.</span><span class="sxs-lookup"><span data-stu-id="5126c-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="5126c-119">![Selecteer Next Generation Firewall-oplossing][4]</span><span class="sxs-lookup"><span data-stu-id="5126c-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="5126c-120">Hallo **Check Point** blade wordt geopend zodat u informatie over Hallo partneroplossing.</span><span class="sxs-lookup"><span data-stu-id="5126c-120">hello **Check Point** blade opens providing you information about hello partner solution.</span></span> <span data-ttu-id="5126c-121">Selecteer **maken** Hallo informatie blade.</span><span class="sxs-lookup"><span data-stu-id="5126c-121">Select **Create** in hello information blade.</span></span>
   <span data-ttu-id="5126c-122">![Firewall-informatie-blade][5]</span><span class="sxs-lookup"><span data-stu-id="5126c-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="5126c-123">Hallo **virtuele machine maken** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="5126c-123">hello **Create virtual machine** blade opens.</span></span> <span data-ttu-id="5126c-124">Hier kunt u informatie vereist toospin een virtuele machine (VM) die wordt uitgevoerd Hallo NGFW.</span><span class="sxs-lookup"><span data-stu-id="5126c-124">Here you can enter information required toospin up a virtual machine (VM) that runs hello NGFW.</span></span> <span data-ttu-id="5126c-125">Hallo stappen en bieden Hallo NGFW informatie vereist.</span><span class="sxs-lookup"><span data-stu-id="5126c-125">Follow hello steps and provide hello NGFW information required.</span></span> <span data-ttu-id="5126c-126">Selecteer OK tooapply.</span><span class="sxs-lookup"><span data-stu-id="5126c-126">Select OK tooapply.</span></span>
   <span data-ttu-id="5126c-127">![Virtuele machine toorun NGFW maken][6]</span><span class="sxs-lookup"><span data-stu-id="5126c-127">![Create virtual machine toorun NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="5126c-128">Het verkeer alleen via de NGFW leiden</span><span class="sxs-lookup"><span data-stu-id="5126c-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="5126c-129">Retourneren van toohello **aanbevelingen** blade.</span><span class="sxs-lookup"><span data-stu-id="5126c-129">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="5126c-130">Een nieuwe vermelding is gegenereerd nadat u een NGFW via Security Center, aangeroepen toegevoegd **routeren van verkeer via NGFW**.</span><span class="sxs-lookup"><span data-stu-id="5126c-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="5126c-131">Deze aanbeveling wordt alleen gemaakt als u uw NGFW door Security Center geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5126c-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="5126c-132">Als u internetgerichte eindpunten hebt, raadt Security Center Netwerkbeveiligingsgroep regels waarmee binnenkomend verkeer tooyour VM via uw NGFW forceren te configureren.</span><span class="sxs-lookup"><span data-stu-id="5126c-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic tooyour VM through your NGFW.</span></span>

1. <span data-ttu-id="5126c-133">In Hallo **blade aanbevelingen**, selecteer **routeren van verkeer via NGFW**.</span><span class="sxs-lookup"><span data-stu-id="5126c-133">In hello **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="5126c-134">![Verkeer alleen via NGFW sturen][7]</span><span class="sxs-lookup"><span data-stu-id="5126c-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="5126c-135">Hiermee opent u de blade Hallo **routeren van verkeer via NGFW**, die een lijst met virtuele machines die u kunt het verkeer naar versturen.</span><span class="sxs-lookup"><span data-stu-id="5126c-135">This opens hello blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="5126c-136">Selecteer een virtuele machine in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="5126c-136">Select a VM from hello list.</span></span>
   <span data-ttu-id="5126c-137">![Selecteer een virtuele machine][8]</span><span class="sxs-lookup"><span data-stu-id="5126c-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="5126c-138">Een blade voor Hallo geselecteerd VM geopend waarin gerelateerde regels voor binnenkomende verbindingen.</span><span class="sxs-lookup"><span data-stu-id="5126c-138">A blade for hello selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="5126c-139">Een beschrijving biedt u meer informatie over het mogelijk de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="5126c-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="5126c-140">Selecteer **binnenkomende regels bewerken** tooproceed met een inkomende regel bewerken.</span><span class="sxs-lookup"><span data-stu-id="5126c-140">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span> <span data-ttu-id="5126c-141">Hallo verwachting is dat **bron** is niet ingesteld te**eventuele** voor Hallo internetgerichte eindpunten die zijn gekoppeld aan Hallo NGFW.</span><span class="sxs-lookup"><span data-stu-id="5126c-141">hello expectation is that **Source** is not set too**Any** for hello Internet-facing endpoints linked with hello NGFW.</span></span> <span data-ttu-id="5126c-142">Zie toolearn meer informatie over het Hallo-eigenschappen van inkomende hello-regel [NSG-regels](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="5126c-142">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="5126c-143">![Configureer regels toolimit toegang][9]
   ![binnenkomende regel bewerken][10]</span><span class="sxs-lookup"><span data-stu-id="5126c-143">![Configure rules toolimit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="5126c-144">Zie ook</span><span class="sxs-lookup"><span data-stu-id="5126c-144">See also</span></span>
<span data-ttu-id="5126c-145">Dit document hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling "Toevoegen Next Generation Firewall."</span><span class="sxs-lookup"><span data-stu-id="5126c-145">This document showed you how tooimplement hello Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="5126c-146">toolearn meer informatie over NGFWs en Hallo Check Point-partneroplossing Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="5126c-146">toolearn more about NGFWs and hello Check Point partner solution, see hello following:</span></span>

* [<span data-ttu-id="5126c-147">Next Generation Firewall</span><span class="sxs-lookup"><span data-stu-id="5126c-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="5126c-148">Check Point vSEC</span><span class="sxs-lookup"><span data-stu-id="5126c-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="5126c-149">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="5126c-149">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="5126c-150">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="5126c-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="5126c-151">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="5126c-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="5126c-152">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="5126c-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="5126c-153">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="5126c-153">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="5126c-154">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="5126c-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="5126c-155">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="5126c-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="5126c-156">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="5126c-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
