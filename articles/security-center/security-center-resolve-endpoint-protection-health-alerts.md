---
title: aaaResolve endpoint protection-status meldingen in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** Endpoint Protection oplossen health waarschuwingen **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="792f4-103">Endpoint protection-status meldingen in Azure Security Center oplossen</span><span class="sxs-lookup"><span data-stu-id="792f4-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="792f4-104">Azure Security Center wordt aanbevolen dat u gedetecteerde endpoint protection-statuswaarschuwingen oplossen.</span><span class="sxs-lookup"><span data-stu-id="792f4-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="792f4-105">Security Center kunt u welke virtuele machines (VM's) endpoint protection storingen en hoeveel hebt toosee.</span><span class="sxs-lookup"><span data-stu-id="792f4-105">Security Center enables you toosee which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="792f4-106">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="792f4-106">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="792f4-107">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="792f4-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="792f4-108">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="792f4-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="792f4-109">In Hallo **blade aanbevelingen**, selecteer **waarschuwingen voor Endpoint Protection oplossen health**.</span><span class="sxs-lookup"><span data-stu-id="792f4-109">In hello **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="792f4-110">![Statusmeldingen endpoint protection oplossen][1]</span><span class="sxs-lookup"><span data-stu-id="792f4-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="792f4-111">Hiermee opent u de blade Hallo **Endpoint Protection fout** die een lijst met virtuele machines met fouten en het aantal mislukte Hallo voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="792f4-111">This opens hello blade **Endpoint Protection failure** which lists VMs with failures and hello number of failures for each VM.</span></span> <span data-ttu-id="792f4-112">Selecteer een virtuele machine in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="792f4-112">Select a VM from hello list.</span></span>
   <span data-ttu-id="792f4-113">![Endpoint protection-fout][2]</span><span class="sxs-lookup"><span data-stu-id="792f4-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="792f4-114">Een **fouten lijst** blade wordt geopend voor Hallo virtuele machine geselecteerde, een lijst met fouten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="792f4-114">A **Failures List** blade opens for hello selected VM, displaying a list of failures.</span></span> <span data-ttu-id="792f4-115">Selecteer een fout in Hallo lijst toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="792f4-115">Select a failure from hello list toolearn more.</span></span> <span data-ttu-id="792f4-116">Dit wordt een blade geopend met informatie over de fout Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="792f4-116">This opens a blade with information about hello selected failure.</span></span>
   <span data-ttu-id="792f4-117">![Lijst met fouten][3]
   ![foutgebeurtenis][4]</span><span class="sxs-lookup"><span data-stu-id="792f4-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="792f4-118">Zie ook</span><span class="sxs-lookup"><span data-stu-id="792f4-118">See also</span></span>
<span data-ttu-id="792f4-119">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="792f4-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="792f4-120">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md)--meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="792f4-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="792f4-121">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md): leer hoe aanbevelingen u helpen uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="792f4-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="792f4-122">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md)--meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="792f4-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="792f4-123">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md)--meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="792f4-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="792f4-124">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="792f4-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="792f4-125">[Veelgestelde vragen over Azure Security Center](security-center-faq.md)--Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="792f4-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="792f4-126">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/)--Hallo nieuwste Azure-beveiliging nieuws en informatie.</span><span class="sxs-lookup"><span data-stu-id="792f4-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
