---
title: Beperken van toegang via internetgerichte eindpunten in Azure Security Center | Microsoft Docs
description: Dit document ziet u hoe de aanbeveling Azure Security Center implementeren ** toegang via Internetgericht eindpunt ** beperken.
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
ms.openlocfilehash: f7309c617f1705205e2c9f1b1b48d141391d45da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="f4e9f-103">Beperken van toegang via internetgerichte eindpunten in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f4e9f-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="f4e9f-104">Azure Security Center wordt aanbevolen dat u de toegang via internetgerichte eindpunten beperken als een van uw Netwerkbeveiligingsgroepen (nsg's) heeft een of meer regels voor binnenkomende verbindingen die toegankelijk is vanaf 'alle' IP-bronadressen.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="f4e9f-105">Toegang tot 'een' te openen, is het mogelijk maken aanvallers voor toegang tot uw resources.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-105">Opening access to “any” may enable attackers to access your resources.</span></span> <span data-ttu-id="f4e9f-106">Security Center beveelt aan dat u deze regels voor binnenkomende verbindingen om toegang te beperken in bron-IP-adressen die daadwerkelijk toegang nodig bewerken.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-106">Security Center will recommend that you edit these inbound rules to restrict access to source IP addresses that actually need access.</span></span>

<span data-ttu-id="f4e9f-107">Deze aanbeveling is voor elke niet--poort dat 'een' als bron gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="f4e9f-108">In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="f4e9f-109">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="f4e9f-110">De aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="f4e9f-110">Implement the recommendation</span></span>
1. <span data-ttu-id="f4e9f-111">In de **blade aanbevelingen**, selecteer **beperken van toegang via Internetgericht eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-111">In the **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Toegang via een internetgericht eindpunt beperken][1]
2. <span data-ttu-id="f4e9f-113">Hiermee opent u de blade **beperken van toegang via Internetgericht eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-113">This opens the blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="f4e9f-114">Deze blade bevat de virtuele machines (VM's) met regels voor binnenkomende verbindingen die een mogelijk beveiligingsprobleem te maken.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-114">This blade lists the virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="f4e9f-115">Selecteer een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-115">Select a VM.</span></span>

   ![Selecteer een virtuele machine][2]
3. <span data-ttu-id="f4e9f-117">De **NSG** blade geeft Netwerkbeveiligingsgroep informatie, gerelateerde regels voor binnenkomende verbindingen, en de bijbehorende virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-117">The **NSG** blade displays Network Security Group information, related inbound rules, and the associated VM.</span></span> <span data-ttu-id="f4e9f-118">Selecteer **binnenkomende regels bewerken** om door te gaan met het bewerken van een inkomende regel.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-118">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span>

   ![Netwerkbeveiligingsgroep-blade][3]
4. <span data-ttu-id="f4e9f-120">Op de **inkomende beveiligingsregels** blade selecteert u de inkomende regel om te bewerken.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-120">On the **Inbound security rules** blade select the inbound rule to edit.</span></span> <span data-ttu-id="f4e9f-121">In dit voorbeeld gaan we selecteren **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Inkomende beveiligingsregels][4]

   <span data-ttu-id="f4e9f-123">Opmerking: u kunt ook selecteren **regels standaard** om te zien van de set met standaardregels die zijn opgenomen in alle nsg's.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-123">Note, you can also select **Default rules** to see the set of default rules contained by all NSGs.</span></span> <span data-ttu-id="f4e9f-124">De standaardregels kunnen niet worden verwijderd, maar omdat ze een lagere prioriteit worden toegewezen, kunnen ze worden overschreven door de regels die u maakt.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-124">The default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by the rules that you create.</span></span> <span data-ttu-id="f4e9f-125">Meer informatie over [regels standaard](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="f4e9f-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Standaardregels][5]
5. <span data-ttu-id="f4e9f-127">Op de **AllowWeb** blade, bewerk de eigenschappen van de binnenkomende regel zodat de **bron** is een IP-adres of een blok IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-127">On the **AllowWeb** blade, edit the properties of the inbound rule so that the **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="f4e9f-128">Zie voor meer informatie over de eigenschappen van de binnenkomende regel, [NSG-regels](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="f4e9f-128">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Regel voor binnenkomende bewerken][6]

## <a name="see-also"></a><span data-ttu-id="f4e9f-130">Zie ook</span><span class="sxs-lookup"><span data-stu-id="f4e9f-130">See also</span></span>
<span data-ttu-id="f4e9f-131">In dit artikel hebt u geleerd hoe u implementeert de aanbeveling Security Center 'Toegang beperken tot en met een internetgericht eindpunt'.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-131">This article showed you how to implement the Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="f4e9f-132">Zie de volgende onderwerpen voor meer informatie over het inschakelen van regels en nsg's:</span><span class="sxs-lookup"><span data-stu-id="f4e9f-132">To learn more about enabling NSGs and rules, see the following:</span></span>

* [<span data-ttu-id="f4e9f-133">Wat is een netwerkbeveiligingsgroep (NSG)?</span><span class="sxs-lookup"><span data-stu-id="f4e9f-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="f4e9f-134">Het nsg's met de Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="f4e9f-134">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="f4e9f-135">Zie de volgende onderwerpen voor meer informatie over het Beveiligingscentrum:</span><span class="sxs-lookup"><span data-stu-id="f4e9f-135">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="f4e9f-136">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md): leer hoe u beveiligingsbeleid voor uw Azure-abonnementen en -resourcegroepen configureert.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f4e9f-137">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md): leer hoe aanbevelingen u helpen uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f4e9f-138">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md): meer informatie over het bewaken van de status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="f4e9f-139">[Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center](security-center-managing-and-responding-alerts.md): leer hoe u beveiligingswaarschuwingen kunt beheren en erop kunt reageren.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-139">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="f4e9f-140">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="f4e9f-141">[Azure Security Center FAQ](security-center-faq.md): raadpleeg veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="f4e9f-142">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) (Azure-beveiligingsblog): hier vindt u het laatste nieuws over Azure-beveiliging en andere informatie.</span><span class="sxs-lookup"><span data-stu-id="f4e9f-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
