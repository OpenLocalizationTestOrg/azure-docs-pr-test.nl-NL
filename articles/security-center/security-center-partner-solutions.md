---
title: partneroplossingen aaaManaging in Azure Security Center | Microsoft Docs
description: "Dit document leert u hoe Azure Security Center u monitor in een oogopslag Hallo gezondheidsstatus van de partneroplossingen die zijn geïntegreerd met uw Azure-abonnement kunt."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="2e726-103">Partneroplossingen bewaken met Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="2e726-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="2e726-104">Dit document begeleidt u bij hoe toomonitor Hallo gezondheidsstatus van uw partneroplossingen in Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="2e726-104">This document walks you through how toomonitor hello health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="2e726-105">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="2e726-105">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="2e726-106">Dit document is niet een stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="2e726-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="2e726-107">Partneroplossingen bewaken</span><span class="sxs-lookup"><span data-stu-id="2e726-107">Monitoring partner solutions</span></span>
<span data-ttu-id="2e726-108">Hallo **partneroplossingen** tegel op Hallo **Security Center** blade kunt u controleren in een oogopslag Hallo gezondheidsstatus van de partneroplossingen die zijn geïntegreerd met uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2e726-108">hello **Partner solutions** tile on hello **Security Center** blade lets you monitor at a glance hello health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![Tegel Partneroplossingen][1]

<span data-ttu-id="2e726-110">Hallo **partneroplossingen** tegel Hallo aantal partneroplossingen die zijn geïntegreerd met uw abonnement wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2e726-110">hello **Partner solutions** tile displays hello number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="2e726-111">Als er geen oplossingen geïntegreerd, geeft Hallo tegel Hallo cijfer nul.</span><span class="sxs-lookup"><span data-stu-id="2e726-111">If there are no solutions integrated, hello tile displays hello number zero.</span></span>

<span data-ttu-id="2e726-112">tooview hello status van uw partneroplossingen:</span><span class="sxs-lookup"><span data-stu-id="2e726-112">tooview hello health of your partner solutions:</span></span>

1. <span data-ttu-id="2e726-113">Selecteer Hallo **partneroplossingen** tegel.</span><span class="sxs-lookup"><span data-stu-id="2e726-113">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="2e726-114">Hallo **partneroplossingen** blade wordt geopend met een lijst van uw partneroplossingen verbonden tooSecurity Center.</span><span class="sxs-lookup"><span data-stu-id="2e726-114">hello **Partner solutions** blade opens displaying a list of your partner solutions connected tooSecurity Center.</span></span>

   ![Partneroplossingen][3]

   <span data-ttu-id="2e726-116">Hallo-status van een partneroplossing kan zijn:</span><span class="sxs-lookup"><span data-stu-id="2e726-116">hello status of a partner solution can be:</span></span>

   * <span data-ttu-id="2e726-117">Beveiligd (groen): er is geen probleem met de status.</span><span class="sxs-lookup"><span data-stu-id="2e726-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="2e726-118">Niet in orde (rood): er is een probleem met de status waarvoor onmiddellijke aandacht is vereist.</span><span class="sxs-lookup"><span data-stu-id="2e726-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="2e726-119">Gestopte reporting (oranje): Hallo-oplossing is gestopt melden van de status.</span><span class="sxs-lookup"><span data-stu-id="2e726-119">Stopped reporting (orange) - hello solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="2e726-120">Onbekende beveiligingsstatus (oranje): Hallo-status van het Hallo-oplossing is onbekend op dit moment vanwege tooa is mislukt-proces voor het toevoegen van een nieuwe resource toohello bestaande oplossing.</span><span class="sxs-lookup"><span data-stu-id="2e726-120">Unknown protection status (orange) - hello health of hello solution is unknown at this time due tooa failed process of adding a new resource toohello existing solution.</span></span>
   * <span data-ttu-id="2e726-121">Niet gerapporteerd (grijs) - Hallo-oplossing heeft gerapporteerd iets nog een oplossing status is mogelijk omdat als deze onlangs verbonden is en nog steeds implementeert.</span><span class="sxs-lookup"><span data-stu-id="2e726-121">Not reported (gray) - hello solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="2e726-122">Selecteer een partneroplossing.</span><span class="sxs-lookup"><span data-stu-id="2e726-122">Select a partner solution.</span></span> <span data-ttu-id="2e726-123">In dit voorbeeld kunt u selecteren Hallo **Qualys** oplossing.</span><span class="sxs-lookup"><span data-stu-id="2e726-123">In this example, lets select hello **Qualys** solution.</span></span>  <span data-ttu-id="2e726-124">Er wordt een blade geopend met de gekoppelde resources Hallo status van de partneroplossing Hallo en Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="2e726-124">A blade opens showing you hello status of hello partner solution and hello solution's associated resources.</span></span> <span data-ttu-id="2e726-125">Selecteer **oplossingenconsole** tooopen Hallo partner management ervaring voor deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="2e726-125">Select **Solution console** tooopen hello partner management experience for this solution.</span></span>

   ![Details van partneroplossingen][4]
3. <span data-ttu-id="2e726-127">Ga terug toohello **Qualys** blade en selecteer **koppeling VM**.</span><span class="sxs-lookup"><span data-stu-id="2e726-127">Go back toohello **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="2e726-128">Hallo **toepassingen koppelen** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="2e726-128">hello **Link Applications** blade opens.</span></span> <span data-ttu-id="2e726-129">Hier kunt u resources toohello partneroplossing.</span><span class="sxs-lookup"><span data-stu-id="2e726-129">Here you can connect resources toohello partner solution.</span></span>

   ![Koppeling resources toopartner oplossing][5]

## <a name="next-steps"></a><span data-ttu-id="2e726-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e726-131">Next steps</span></span>
<span data-ttu-id="2e726-132">In dit document zijn u geïntroduceerd toohello **partneroplossingen** -tegel in Security Center.</span><span class="sxs-lookup"><span data-stu-id="2e726-132">In this document, you were introduced toohello **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="2e726-133">toolearn meer informatie over Security Center, Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2e726-133">toolearn more about Security Center, see hello following articles:</span></span>

* <span data-ttu-id="2e726-134">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) : meer informatie hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="2e726-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="2e726-135">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) : Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="2e726-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="2e726-136">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) : meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="2e726-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="2e726-137">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) : meer informatie hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="2e726-137">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="2e726-138">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="2e726-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="2e726-139">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) : Hallo nieuwste Azure-beveiliging nieuws en informatie.</span><span class="sxs-lookup"><span data-stu-id="2e726-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
