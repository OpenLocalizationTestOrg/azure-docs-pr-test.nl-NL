---
title: Azure Advisor kosten aanbevelingen | Microsoft Docs
description: Gebruik Azure Advisor om te optimaliseren van de kosten van uw Azure-implementaties.
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
ms.openlocfilehash: 5eef2116f238b477fa8de46ce7b25728c393739c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="c39f1-103">Advisor kosten aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="c39f1-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="c39f1-104">Advisor helpt u te optimaliseren en reduceren uw algehele Azure hoeven te besteden aan met het vaststellen van niet-actieve- en onderbenutte resources.</span><span class="sxs-lookup"><span data-stu-id="c39f1-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="c39f1-105">U kunt ophalen kosten aanbevelingen van de **kosten** op het dashboard Advisor.</span><span class="sxs-lookup"><span data-stu-id="c39f1-105">You can get cost recommendations from the **Cost** tab on the Advisor dashboard.</span></span>

![Tabblad van Advisor kosten](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="c39f1-107">Optimaliseren door het formaat onderbenutte exemplaren te besteden aan de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c39f1-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="c39f1-108">Hoewel bepaalde toepassingsscenario's leiden minder gebruik standaard tot kunnen, kunt u vaak geld besparen door het beheer van de grootte en het nummer van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c39f1-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing the size and number of your virtual machines.</span></span> <span data-ttu-id="c39f1-109">Advisor bewaakt het gebruik van uw virtuele machine 14 dagen en identificeert dan laag gebruik virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c39f1-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="c39f1-110">Virtuele machines waarvan CPU-gebruik 5 is % of minder en netwerkgebruik is 7 MB of minder voor vier of meer dagen worden beschouwd als laag gebruik virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c39f1-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="c39f1-111">Advisor ziet u de geschatte kosten van u wilt doorgaan met het uitvoeren van uw virtuele machine, zodat u kunt deze afsluiten of het formaat.</span><span class="sxs-lookup"><span data-stu-id="c39f1-111">Advisor shows you the estimated cost of continuing to run your virtual machine, so that you can choose to shut it down or resize it.</span></span>  

![Advisor kosten aanbevelingen voor het vergroten of verkleinen van virtuele machines](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-to-manage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="c39f1-113">Een kostenbesparende oplossing gebruiken voor het beheren van prestatiedoelstellingen van meerdere SQL-databases</span><span class="sxs-lookup"><span data-stu-id="c39f1-113">Use a cost effective solution to manage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="c39f1-114">Advisor identificeert SQL server-exemplaren die u profiteren kunnen van het maken van pools voor elastische databases.</span><span class="sxs-lookup"><span data-stu-id="c39f1-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="c39f1-115">Pools voor elastische databases bieden een eenvoudige, rendabele oplossing voor het beheren van de prestatiedoelstellingen van meerdere databases die verschillende gebruikspatronen hebben.</span><span class="sxs-lookup"><span data-stu-id="c39f1-115">Elastic database pools provide a simple, cost-effective solution to manage the performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="c39f1-116">Zie voor meer informatie over Azure elastische pools [wat is er een Azure elastische pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="c39f1-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Advisor kosten aanbevelingen voor pools voor elastische databases](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-to-access-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="c39f1-118">Toegang tot de aanbevelingen in Azure Advisor kosten</span><span class="sxs-lookup"><span data-stu-id="c39f1-118">How to access cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="c39f1-119">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c39f1-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c39f1-120">Klik in het linkerdeelvenster op **meer services**.</span><span class="sxs-lookup"><span data-stu-id="c39f1-120">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="c39f1-121">Klik in het deelvenster service menu onder **bewaking en beheer**, klikt u op **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="c39f1-121">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="c39f1-122">De Advisor-dashboard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c39f1-122">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="c39f1-123">Klik op het dashboard Advisor de **kosten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c39f1-123">On the Advisor dashboard, click the **Cost** tab.</span></span>

5. <span data-ttu-id="c39f1-124">Selecteer het abonnement waarvoor u wilt ontvangen van aanbevelingen en klik vervolgens op **aanbevelingen krijgen**.</span><span class="sxs-lookup"><span data-stu-id="c39f1-124">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="c39f1-125">Voor toegang tot de aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor.</span><span class="sxs-lookup"><span data-stu-id="c39f1-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="c39f1-126">Een abonnement is geregistreerd als een *abonnement eigenaar* start van de Advisor-dashboard en klikt op de **aanbevelingen krijgen** knop.</span><span class="sxs-lookup"><span data-stu-id="c39f1-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="c39f1-127">Dit is een *eenmalige bewerking*.</span><span class="sxs-lookup"><span data-stu-id="c39f1-127">This is a *one-time operation*.</span></span> <span data-ttu-id="c39f1-128">Nadat het abonnement is geregistreerd, kunt u de aanbevelingen van Advisor als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, resourcegroep of een specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="c39f1-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c39f1-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c39f1-129">Next steps</span></span>

<span data-ttu-id="c39f1-130">Zie voor meer informatie over Advisor aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="c39f1-130">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="c39f1-131">Inleiding tot Advisor</span><span class="sxs-lookup"><span data-stu-id="c39f1-131">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="c39f1-132">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="c39f1-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="c39f1-133">Aanbevelingen van Advisor-prestaties</span><span class="sxs-lookup"><span data-stu-id="c39f1-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="c39f1-134">Hoge beschikbaarheid aanbevelingen Advisor te ontvangen</span><span class="sxs-lookup"><span data-stu-id="c39f1-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="c39f1-135">Aanbevelingen voor beveiliging van Advisor</span><span class="sxs-lookup"><span data-stu-id="c39f1-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
