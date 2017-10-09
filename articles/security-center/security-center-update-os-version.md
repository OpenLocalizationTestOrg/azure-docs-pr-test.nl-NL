---
title: aaaUpdate OS-versie in Azure Security Center | Microsoft Docs
description: Dit artikel laat zien hoe tooimplement hello Azure Security Center aanbeveling ** Update OS-versie **.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: aa372492-ecdb-4368-8fdd-d8ed31e216ee
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: f3497d7266da40d3a965f9cb8e84392d2aaa28f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-os-version-in-azure-security-center"></a><span data-ttu-id="ef49a-103">Bijwerken van de versie van het besturingssysteem in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="ef49a-103">Update OS version in Azure Security Center</span></span>
<span data-ttu-id="ef49a-104">Voor virtuele machines (VM's) in de cloud-services, Azure Security Center beveelt aan dat Hallo-besturingssysteem (OS) worden bijgewerkt als er een recentere versie beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="ef49a-104">For virtual machines (VMs) in cloud services, Azure Security Center will recommend that hello operating system (OS) be updated if there is a more recent version available.</span></span>  <span data-ttu-id="ef49a-105">Alleen cloud services-web- en werkrollen rollen die worden uitgevoerd in de productieomgeving sleuven worden bewaakt.</span><span class="sxs-lookup"><span data-stu-id="ef49a-105">Only cloud services web and worker roles running in production slots are monitored.</span></span>

> [!NOTE]
> <span data-ttu-id="ef49a-106">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="ef49a-106">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="ef49a-107">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="ef49a-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="ef49a-108">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="ef49a-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="ef49a-109">In Hallo **aanbevelingen** blade Selecteer **Update besturingssysteemversie**.</span><span class="sxs-lookup"><span data-stu-id="ef49a-109">In hello **Recommendations** blade, select **Update OS version**.</span></span>
   <span data-ttu-id="ef49a-110">![Besturingssysteemversie bijwerken][1]</span><span class="sxs-lookup"><span data-stu-id="ef49a-110">![Update OS version][1]</span></span>
2. <span data-ttu-id="ef49a-111">Hiermee opent u de blade Hallo **Update besturingssysteemversie**.</span><span class="sxs-lookup"><span data-stu-id="ef49a-111">This opens hello blade **Update OS version**.</span></span> <span data-ttu-id="ef49a-112">Hallo stappen in deze blade tooupdate Hallo OS-versie.</span><span class="sxs-lookup"><span data-stu-id="ef49a-112">Follow hello steps in this blade tooupdate hello OS version.</span></span>

## <a name="see-also"></a><span data-ttu-id="ef49a-113">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ef49a-113">See also</span></span>
<span data-ttu-id="ef49a-114">In dit artikel hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling 'Update OS-versie.</span><span class="sxs-lookup"><span data-stu-id="ef49a-114">This article showed you how tooimplement hello Security Center recommendation "Update OS version."</span></span> <span data-ttu-id="ef49a-115">toolearn meer informatie over cloudservices en bijwerken Hallo OS-versie voor een cloudservice, Zie:</span><span class="sxs-lookup"><span data-stu-id="ef49a-115">toolearn more about cloud services and updating hello OS version for a cloud service, see:</span></span>

* [<span data-ttu-id="ef49a-116">Overzicht van Cloud Services</span><span class="sxs-lookup"><span data-stu-id="ef49a-116">Cloud Services overview</span></span>](../cloud-services/cloud-services-choose-me.md)
* [<span data-ttu-id="ef49a-117">Hoe tooupdate een cloudservice</span><span class="sxs-lookup"><span data-stu-id="ef49a-117">How tooupdate a cloud service</span></span>](../cloud-services/cloud-services-update-azure-service.md)
* [<span data-ttu-id="ef49a-118">Hoe tooConfigure Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="ef49a-118">How tooConfigure Cloud Services</span></span>](../cloud-services/cloud-services-how-to-configure-portal.md)

<span data-ttu-id="ef49a-119">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="ef49a-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="ef49a-120">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="ef49a-120">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ef49a-121">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="ef49a-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ef49a-122">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="ef49a-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="ef49a-123">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="ef49a-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="ef49a-124">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef49a-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="ef49a-125">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="ef49a-125">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="ef49a-126">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Hallo nieuwste Azure-beveiliging nieuws en informatie.</span><span class="sxs-lookup"><span data-stu-id="ef49a-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-update-os-version/update-os-version.png
