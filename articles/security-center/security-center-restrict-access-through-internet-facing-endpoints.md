---
title: aaaRestrict toegang via internetgerichte eindpunten in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** toegang via Internetgericht eindpunt ** beperken.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="7ecde-103">Beperken van toegang via internetgerichte eindpunten in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="7ecde-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="7ecde-104">Azure Security Center wordt aanbevolen dat u de toegang via internetgerichte eindpunten beperken als een van uw Netwerkbeveiligingsgroepen (nsg's) heeft een of meer regels voor binnenkomende verbindingen die toegankelijk is vanaf 'alle' IP-bronadressen.</span><span class="sxs-lookup"><span data-stu-id="7ecde-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="7ecde-105">Openstellen te 'any' mogelijkheid aanvallers tooaccess uw resources.</span><span class="sxs-lookup"><span data-stu-id="7ecde-105">Opening access too“any” may enable attackers tooaccess your resources.</span></span> <span data-ttu-id="7ecde-106">Security Center beveelt aan dat u deze regels voor binnenkomende verbindingen toorestrict toegang toosource IP-adressen die daadwerkelijk toegang nodig bewerken.</span><span class="sxs-lookup"><span data-stu-id="7ecde-106">Security Center will recommend that you edit these inbound rules toorestrict access toosource IP addresses that actually need access.</span></span>

<span data-ttu-id="7ecde-107">Deze aanbeveling is voor elke niet--poort dat 'een' als bron gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="7ecde-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="7ecde-108">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="7ecde-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="7ecde-109">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="7ecde-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="7ecde-110">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="7ecde-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="7ecde-111">In Hallo **blade aanbevelingen**, selecteer **beperken van toegang via Internetgericht eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="7ecde-111">In hello **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Toegang via een internetgericht eindpunt beperken][1]
2. <span data-ttu-id="7ecde-113">Hiermee opent u de blade Hallo **beperken van toegang via Internetgericht eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="7ecde-113">This opens hello blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="7ecde-114">Deze blade bevat Hallo virtuele machines (VM's) met regels voor binnenkomende verbindingen die een mogelijk beveiligingsprobleem te maken.</span><span class="sxs-lookup"><span data-stu-id="7ecde-114">This blade lists hello virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="7ecde-115">Selecteer een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7ecde-115">Select a VM.</span></span>

   ![Selecteer een virtuele machine][2]
3. <span data-ttu-id="7ecde-117">Hallo **NSG** blade Netwerkbeveiligingsgroep wordt informatie weergegeven, gerelateerde binnenkomende regels en Hallo VM gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="7ecde-117">hello **NSG** blade displays Network Security Group information, related inbound rules, and hello associated VM.</span></span> <span data-ttu-id="7ecde-118">Selecteer **binnenkomende regels bewerken** tooproceed met een inkomende regel bewerken.</span><span class="sxs-lookup"><span data-stu-id="7ecde-118">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span>

   ![Netwerkbeveiligingsgroep-blade][3]
4. <span data-ttu-id="7ecde-120">Op Hallo **inkomende beveiligingsregels** blade Selecteer Hallo binnenkomende regel tooedit.</span><span class="sxs-lookup"><span data-stu-id="7ecde-120">On hello **Inbound security rules** blade select hello inbound rule tooedit.</span></span> <span data-ttu-id="7ecde-121">In dit voorbeeld gaan we selecteren **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="7ecde-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Inkomende beveiligingsregels][4]

   <span data-ttu-id="7ecde-123">Opmerking: u kunt ook selecteren **regels standaard** toosee Hallo set met standaardregels die zijn opgenomen in alle nsg's.</span><span class="sxs-lookup"><span data-stu-id="7ecde-123">Note, you can also select **Default rules** toosee hello set of default rules contained by all NSGs.</span></span> <span data-ttu-id="7ecde-124">Hallo-standaardregels kunnen niet worden verwijderd, maar omdat ze een lagere prioriteit worden toegewezen, kunnen ze worden overschreven door het Hallo-regels die u maakt.</span><span class="sxs-lookup"><span data-stu-id="7ecde-124">hello default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by hello rules that you create.</span></span> <span data-ttu-id="7ecde-125">Meer informatie over [regels standaard](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="7ecde-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Standaardregels][5]
5. <span data-ttu-id="7ecde-127">Op Hallo **AllowWeb** blade Hallo-eigenschappen bewerken van Hallo binnenkomende regel zodat die Hallo **bron** is een IP-adres of een blok IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="7ecde-127">On hello **AllowWeb** blade, edit hello properties of hello inbound rule so that hello **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="7ecde-128">Zie toolearn meer informatie over het Hallo-eigenschappen van inkomende hello-regel [NSG-regels](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="7ecde-128">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Regel voor binnenkomende bewerken][6]

## <a name="see-also"></a><span data-ttu-id="7ecde-130">Zie ook</span><span class="sxs-lookup"><span data-stu-id="7ecde-130">See also</span></span>
<span data-ttu-id="7ecde-131">In dit artikel hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling 'toegang beperken tot en met een Internetgericht eindpunt."</span><span class="sxs-lookup"><span data-stu-id="7ecde-131">This article showed you how tooimplement hello Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="7ecde-132">toolearn meer informatie over het inschakelen van regels, en nsg's ziet Hallo:</span><span class="sxs-lookup"><span data-stu-id="7ecde-132">toolearn more about enabling NSGs and rules, see hello following:</span></span>

* [<span data-ttu-id="7ecde-133">Wat is een netwerkbeveiligingsgroep (NSG)?</span><span class="sxs-lookup"><span data-stu-id="7ecde-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="7ecde-134">Hoe toomanage nsg's met behulp van Azure-portal Hallo</span><span class="sxs-lookup"><span data-stu-id="7ecde-134">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="7ecde-135">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="7ecde-135">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="7ecde-136">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md)--meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="7ecde-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="7ecde-137">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md): leer hoe aanbevelingen u helpen uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="7ecde-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="7ecde-138">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md)--meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="7ecde-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="7ecde-139">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md)--meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="7ecde-139">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="7ecde-140">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ecde-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="7ecde-141">[Veelgestelde vragen over Azure Security Center](security-center-faq.md)--Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="7ecde-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="7ecde-142">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/)--Hallo nieuwste Azure-beveiliging nieuws en informatie.</span><span class="sxs-lookup"><span data-stu-id="7ecde-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
