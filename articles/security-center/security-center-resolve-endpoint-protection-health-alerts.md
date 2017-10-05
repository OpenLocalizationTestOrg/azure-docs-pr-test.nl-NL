---
title: Endpoint protection-status meldingen in Azure Security Center oplossen | Microsoft Docs
description: Dit document ziet u hoe de aanbeveling Azure Security Center implementeren ** Endpoint Protection oplossen health waarschuwingen **.
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
ms.openlocfilehash: 5e6b136d6bd3b11fb82126d104fd0cb149255118
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="9f8d5-103">Endpoint protection-status meldingen in Azure Security Center oplossen</span><span class="sxs-lookup"><span data-stu-id="9f8d5-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="9f8d5-104">Azure Security Center wordt aanbevolen dat u gedetecteerde endpoint protection-statuswaarschuwingen oplossen.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="9f8d5-105">Security Center kunt u zien welke virtuele machines (VM's) hebt endpoint protection storingen en hoeveel.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-105">Security Center enables you to see which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="9f8d5-106">In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-106">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="9f8d5-107">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="9f8d5-108">De aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="9f8d5-108">Implement the recommendation</span></span>
1. <span data-ttu-id="9f8d5-109">In de **blade aanbevelingen**, selecteer **waarschuwingen voor Endpoint Protection oplossen health**.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-109">In the **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="9f8d5-110">![Statusmeldingen endpoint protection oplossen][1]</span><span class="sxs-lookup"><span data-stu-id="9f8d5-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="9f8d5-111">Hiermee opent u de blade **Endpoint Protection fout** die een lijst met virtuele machines met fouten en het aantal fouten voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-111">This opens the blade **Endpoint Protection failure** which lists VMs with failures and the number of failures for each VM.</span></span> <span data-ttu-id="9f8d5-112">Selecteer een virtuele machine in de lijst.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-112">Select a VM from the list.</span></span>
   <span data-ttu-id="9f8d5-113">![Endpoint protection-fout][2]</span><span class="sxs-lookup"><span data-stu-id="9f8d5-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="9f8d5-114">Een **fouten lijst** er wordt een blade geopend voor de geselecteerde virtuele machine met een lijst van fouten.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-114">A **Failures List** blade opens for the selected VM, displaying a list of failures.</span></span> <span data-ttu-id="9f8d5-115">Selecteer een fout in de lijst voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-115">Select a failure from the list to learn more.</span></span> <span data-ttu-id="9f8d5-116">Dit wordt een blade geopend met informatie over de geselecteerde fout.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-116">This opens a blade with information about the selected failure.</span></span>
   <span data-ttu-id="9f8d5-117">![Lijst met fouten][3]
   ![foutgebeurtenis][4]</span><span class="sxs-lookup"><span data-stu-id="9f8d5-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="9f8d5-118">Zie ook</span><span class="sxs-lookup"><span data-stu-id="9f8d5-118">See also</span></span>
<span data-ttu-id="9f8d5-119">Zie de volgende onderwerpen voor meer informatie over het Beveiligingscentrum:</span><span class="sxs-lookup"><span data-stu-id="9f8d5-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="9f8d5-120">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md): leer hoe u beveiligingsbeleid voor uw Azure-abonnementen en -resourcegroepen configureert.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="9f8d5-121">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md): leer hoe aanbevelingen u helpen uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="9f8d5-122">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md): meer informatie over het bewaken van de status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="9f8d5-123">[Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center](security-center-managing-and-responding-alerts.md): leer hoe u beveiligingswaarschuwingen kunt beheren en erop kunt reageren.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="9f8d5-124">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="9f8d5-125">[Azure Security Center FAQ](security-center-faq.md): raadpleeg veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="9f8d5-126">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) (Azure-beveiligingsblog): hier vindt u het laatste nieuws over Azure-beveiliging en andere informatie.</span><span class="sxs-lookup"><span data-stu-id="9f8d5-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
