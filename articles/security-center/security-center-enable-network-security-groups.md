---
title: aaaEnable Netwerkbeveiligingsgroepen in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** inschakelen netwerk beveiliging groepen **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="8abd5-103">Inschakelen van Netwerkbeveiligingsgroepen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="8abd5-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="8abd5-104">Azure Security Center raadt aan dat u een netwerkbeveiligingsgroep (NSG) inschakelen als een nog niet is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8abd5-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="8abd5-105">Nsg's bevatten een lijst met regels voor lijst ACL (Access Control) toestaan of weigeren netwerkverkeer tooyour VM-exemplaren in een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="8abd5-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="8abd5-106">NSG's kunnen worden gekoppeld aan subnetten of afzonderlijke VM-exemplaren in dat subnet.</span><span class="sxs-lookup"><span data-stu-id="8abd5-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="8abd5-107">Wanneer een NSG gekoppeld aan een subnet is, toepassing hello ACL-regels tooall Hallo VM-exemplaren in dat subnet.</span><span class="sxs-lookup"><span data-stu-id="8abd5-107">When an NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="8abd5-108">Bovendien verkeer tooan afzonderlijke VM kan worden beperkt door een NSG koppelen verdere rechtstreeks toothat VM.</span><span class="sxs-lookup"><span data-stu-id="8abd5-108">In addition, traffic tooan individual VM can be restricted further by associating an NSG directly toothat VM.</span></span> <span data-ttu-id="8abd5-109">toolearn Zie meer [wat is er een Netwerkbeveiligingsgroep (NSG)?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="8abd5-109">toolearn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="8abd5-110">Als u geen nsg's is ingeschakeld, Security Center geeft twee aanbevelingen tooyou: schakelen van Netwerkbeveiligingsgroepen op subnetten en inschakelen van Netwerkbeveiligingsgroepen op virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8abd5-110">If you do not have NSGs enabled, Security Center presents two recommendations tooyou: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="8abd5-111">U kiezen welke niveau, subnet of virtuele machine, tooapply nsg's.</span><span class="sxs-lookup"><span data-stu-id="8abd5-111">You choose which level, subnet or VM, tooapply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="8abd5-112">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="8abd5-112">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="8abd5-113">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="8abd5-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="8abd5-114">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="8abd5-114">Implement hello recommendation</span></span>
1. <span data-ttu-id="8abd5-115">In Hallo **aanbevelingen** blade Selecteer **Netwerkbeveiligingsgroepen inschakelen** op subnetten of op virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8abd5-115">In hello **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="8abd5-116">![Netwerkbeveiligingsgroepen inschakelen][1]</span><span class="sxs-lookup"><span data-stu-id="8abd5-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="8abd5-117">Hiermee opent u de blade Hallo **ontbrekende Netwerkbeveiligingsgroepen configureren** voor subnetten of voor virtuele machines, afhankelijk van het Hallo-aanbeveling die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="8abd5-117">This opens hello blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on hello recommendation that you selected.</span></span> <span data-ttu-id="8abd5-118">Selecteer een subnet of een virtuele machine tooconfigure een NSG op.</span><span class="sxs-lookup"><span data-stu-id="8abd5-118">Select a subnet or a virtual machine tooconfigure an NSG on.</span></span>

   ![NSG voor subnet configureren][2]

   ![NSG voor de virtuele machine configureren][3]
3. <span data-ttu-id="8abd5-121">Op Hallo **netwerkbeveiligingsgroep kiezen** blade, selecteer een bestaande NSG of **nieuw** toocreate een NSG.</span><span class="sxs-lookup"><span data-stu-id="8abd5-121">On hello **Choose network security group** blade, select an existing NSG or select **Create new** toocreate an NSG.</span></span>

   ![Netwerkbeveiligingsgroep kiezen][4]

<span data-ttu-id="8abd5-123">Als u een NSG maakt, stappen Hallo in [hoe toomanage nsg's met behulp van Azure-portal Hallo](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate een NSG en stel de beveiligingsregels voor verbindingen.</span><span class="sxs-lookup"><span data-stu-id="8abd5-123">If you create an NSG, follow hello steps in [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="8abd5-124">Zie ook</span><span class="sxs-lookup"><span data-stu-id="8abd5-124">See also</span></span>
<span data-ttu-id="8abd5-125">In dit artikel hebt u gezien hoe tooimplement Hallo Security Center aanbeveling "inschakelen Netwerkbeveiligingsgroepen' voor subnetten of virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8abd5-125">This article showed you how tooimplement hello Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="8abd5-126">toolearn meer informatie over het inschakelen van NSGs, Zie de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="8abd5-126">toolearn more about enabling NSGs, see hello following:</span></span>

* [<span data-ttu-id="8abd5-127">Wat is een netwerkbeveiligingsgroep (NSG)?</span><span class="sxs-lookup"><span data-stu-id="8abd5-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="8abd5-128">Hoe toomanage nsg's met behulp van Azure-portal Hallo</span><span class="sxs-lookup"><span data-stu-id="8abd5-128">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="8abd5-129">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="8abd5-129">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="8abd5-130">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="8abd5-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="8abd5-131">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="8abd5-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="8abd5-132">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="8abd5-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="8abd5-133">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="8abd5-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="8abd5-134">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="8abd5-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="8abd5-135">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="8abd5-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="8abd5-136">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Hallo nieuwste Azure-beveiliging nieuws en informatie.</span><span class="sxs-lookup"><span data-stu-id="8abd5-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
