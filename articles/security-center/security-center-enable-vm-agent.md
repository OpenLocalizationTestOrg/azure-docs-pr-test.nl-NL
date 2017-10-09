---
title: aaaEnable VM-Agent in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** inschakelen VM Agent **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="546a8-103">VM-Agent in Azure Security Center inschakelen</span><span class="sxs-lookup"><span data-stu-id="546a8-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="546a8-104">Hallo VM-Agent moet worden geïnstalleerd op virtuele machines (VM's) in de volgorde te[gegevensverzameling inschakelen](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="546a8-104">hello VM Agent must be installed on virtual machines (VMs) in order too[enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="546a8-105">Hiermee schakelt u Azure Security Center u toosee waarvoor VMs Hallo VM-Agent en wordt u het beste inschakelen Hallo VM-Agent op deze virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="546a8-105">Azure Security Center enables you toosee which VMs require hello VM Agent and will recommend that you enable hello VM Agent on those VMs.</span></span>

<span data-ttu-id="546a8-106">Hallo VM-Agent wordt standaard geïnstalleerd voor virtuele machines die vanuit Azure Marketplace Hallo worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="546a8-106">hello VM Agent is installed by default for VMs that are deployed from hello Azure Marketplace.</span></span> <span data-ttu-id="546a8-107">Hallo artikel [VM-Agent en -extensies – deel 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) bevat informatie over hoe tooinstall Hallo VM-Agent.</span><span class="sxs-lookup"><span data-stu-id="546a8-107">hello article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how tooinstall hello VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="546a8-108">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="546a8-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="546a8-109">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="546a8-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="546a8-110">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="546a8-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="546a8-111">In Hallo **blade aanbevelingen**, selecteer **VM-Agent inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="546a8-111">In hello **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="546a8-112">![VM-agent inschakelen][1]</span><span class="sxs-lookup"><span data-stu-id="546a8-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="546a8-113">Hiermee opent u de blade Hallo **VM-Agent ontbreekt of niet reageert**.</span><span class="sxs-lookup"><span data-stu-id="546a8-113">This opens hello blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="546a8-114">Deze blade bevat Hallo virtuele machines waarvoor Hallo VM-Agent.</span><span class="sxs-lookup"><span data-stu-id="546a8-114">This blade lists hello VMs that require hello VM Agent.</span></span> <span data-ttu-id="546a8-115">Hallo instructies op Hallo blade tooinstall Hallo VM-agent.</span><span class="sxs-lookup"><span data-stu-id="546a8-115">Follow hello instructions on hello blade tooinstall hello VM agent.</span></span>
   <span data-ttu-id="546a8-116">![VM-Agent ontbreekt.][2]</span><span class="sxs-lookup"><span data-stu-id="546a8-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="546a8-117">Zie ook</span><span class="sxs-lookup"><span data-stu-id="546a8-117">See also</span></span>
<span data-ttu-id="546a8-118">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="546a8-118">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="546a8-119">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md)--meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="546a8-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="546a8-120">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md): leer hoe aanbevelingen u helpen uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="546a8-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="546a8-121">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md)--meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="546a8-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="546a8-122">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md)--meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="546a8-122">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="546a8-123">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="546a8-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="546a8-124">[Veelgestelde vragen over Azure Security Center](security-center-faq.md)--Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="546a8-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="546a8-125">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/)--Hallo nieuwste Azure-beveiliging nieuws en informatie.</span><span class="sxs-lookup"><span data-stu-id="546a8-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
