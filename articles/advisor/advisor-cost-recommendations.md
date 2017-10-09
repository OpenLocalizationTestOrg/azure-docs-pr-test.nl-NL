---
title: aaaAzure Advisor kosten aanbevelingen | Microsoft Docs
description: Gebruik Azure Advisor toooptimize Hallo kosten van uw Azure-implementaties.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="5486a-103">Advisor kosten aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="5486a-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="5486a-104">Advisor helpt u te optimaliseren en reduceren uw algehele Azure hoeven te besteden aan met het vaststellen van niet-actieve- en onderbenutte resources.</span><span class="sxs-lookup"><span data-stu-id="5486a-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="5486a-105">U aanbevelingen van Hallo ophalen kost **kosten** tabblad op Hallo Advisor dashboard.</span><span class="sxs-lookup"><span data-stu-id="5486a-105">You can get cost recommendations from hello **Cost** tab on hello Advisor dashboard.</span></span>

![Tabblad van Advisor kosten](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="5486a-107">Optimaliseren door het formaat onderbenutte exemplaren te besteden aan de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="5486a-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="5486a-108">Hoewel bepaalde toepassingsscenario's leiden minder gebruik standaard tot kunnen, kunt u vaak geld besparen door het beheer van Hallo grootte en het aantal van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5486a-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing hello size and number of your virtual machines.</span></span> <span data-ttu-id="5486a-109">Advisor bewaakt het gebruik van uw virtuele machine 14 dagen en identificeert dan laag gebruik virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5486a-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="5486a-110">Virtuele machines waarvan CPU-gebruik 5 is % of minder en netwerkgebruik is 7 MB of minder voor vier of meer dagen worden beschouwd als laag gebruik virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5486a-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="5486a-111">Advisor ziet u Hallo geschatte kosten van continue toorun uw virtuele machine, zodat u tooshut deze omlaag of het formaat kunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="5486a-111">Advisor shows you hello estimated cost of continuing toorun your virtual machine, so that you can choose tooshut it down or resize it.</span></span>  

![Advisor kosten aanbevelingen voor het vergroten of verkleinen van virtuele machines](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="5486a-113">Gebruik een voordelige oplossing toomanage prestatiedoelen van meerdere SQL-databases</span><span class="sxs-lookup"><span data-stu-id="5486a-113">Use a cost effective solution toomanage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="5486a-114">Advisor identificeert SQL server-exemplaren die u profiteren kunnen van het maken van pools voor elastische databases.</span><span class="sxs-lookup"><span data-stu-id="5486a-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="5486a-115">Pools voor elastische databases bieden een eenvoudige en voordelige oplossing toomanage prestatiedoelstellingen Hallo van meerdere databases die verschillende gebruikspatronen hebben.</span><span class="sxs-lookup"><span data-stu-id="5486a-115">Elastic database pools provide a simple, cost-effective solution toomanage hello performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="5486a-116">Zie voor meer informatie over Azure elastische pools [wat is er een Azure elastische pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="5486a-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Advisor kosten aanbevelingen voor pools voor elastische databases](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="5486a-118">Hoe tooaccess aanbevelingen in Azure Advisor kosten</span><span class="sxs-lookup"><span data-stu-id="5486a-118">How tooaccess cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="5486a-119">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5486a-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="5486a-120">Klik in het linkerdeelvenster Hallo **meer services**.</span><span class="sxs-lookup"><span data-stu-id="5486a-120">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="5486a-121">Service in Hallo menu deelvenster onder **bewaking en beheer**, klikt u op **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="5486a-121">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="5486a-122">Hallo Advisor dashboard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5486a-122">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="5486a-123">Klik op Hallo Advisor dashboard Hallo **kosten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="5486a-123">On hello Advisor dashboard, click hello **Cost** tab.</span></span>

5. <span data-ttu-id="5486a-124">Selecteer Hallo abonnement waarvoor u wilt dat tooreceive aanbevelingen en klik vervolgens op **aanbevelingen krijgen**.</span><span class="sxs-lookup"><span data-stu-id="5486a-124">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="5486a-125">tooaccess aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor.</span><span class="sxs-lookup"><span data-stu-id="5486a-125">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="5486a-126">Een abonnement is geregistreerd als een *abonnement eigenaar* gestart Hallo dashboard en klikt op Hallo van Advisor **aanbevelingen krijgen** knop.</span><span class="sxs-lookup"><span data-stu-id="5486a-126">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="5486a-127">Dit is een *eenmalige bewerking*.</span><span class="sxs-lookup"><span data-stu-id="5486a-127">This is a *one-time operation*.</span></span> <span data-ttu-id="5486a-128">Nadat het Hallo-abonnement is geregistreerd, kunt u Advisor aanbevelingen als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, een resourcegroep of een bepaalde resource.</span><span class="sxs-lookup"><span data-stu-id="5486a-128">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5486a-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5486a-129">Next steps</span></span>

<span data-ttu-id="5486a-130">toolearn meer informatie over de aanbevelingen van Advisor, Zie:</span><span class="sxs-lookup"><span data-stu-id="5486a-130">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="5486a-131">Inleiding tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="5486a-131">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="5486a-132">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="5486a-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="5486a-133">Aanbevelingen van Advisor-prestaties</span><span class="sxs-lookup"><span data-stu-id="5486a-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="5486a-134">Hoge beschikbaarheid aanbevelingen Advisor te ontvangen</span><span class="sxs-lookup"><span data-stu-id="5486a-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="5486a-135">Aanbevelingen voor beveiliging van Advisor</span><span class="sxs-lookup"><span data-stu-id="5486a-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
