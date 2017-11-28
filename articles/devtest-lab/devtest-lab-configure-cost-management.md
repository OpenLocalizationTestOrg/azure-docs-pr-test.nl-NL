---
title: De maandelijkse trend in de testomgeving geschatte kosten weergeven in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over de Azure DevTest Labs maandelijkse geschatte kosten trend van grafiek.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: b3ad1ead522908d4b41b7cca98d20ac91664998e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="view-the-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="d888d-103">De maandelijkse trend in de testomgeving geschatte kosten weergeven in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="d888d-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="d888d-104">De beheerfunctie van kosten van DevTest Labs helpt u bij de kosten van uw testomgeving bijhouden.</span><span class="sxs-lookup"><span data-stu-id="d888d-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span></span> <span data-ttu-id="d888d-105">In dit artikel laat zien hoe u de **maandelijkse geschatte kosten Trend** grafiek voor de huidige kalendermaand geschatte kosten-to-date en de geschatte kosten van de laatste van de maand van de huidige kalendermaand weergeven.</span><span class="sxs-lookup"><span data-stu-id="d888d-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span></span> <span data-ttu-id="d888d-106">In dit artikel leert u hoe de maandelijkse geschatte kosten trend grafiek weergeven in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d888d-106">In this article, you learn how to view the monthly estimated cost trend chart in the Azure portal.</span></span>

## <a name="viewing-the-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="d888d-107">De grafiek maandelijkse geschatte kosten Trend weergeven</span><span class="sxs-lookup"><span data-stu-id="d888d-107">Viewing the Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="d888d-108">Als u wilt weergeven van de grafiek maandelijkse geschatte kosten Trend, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d888d-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="d888d-109">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d888d-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="d888d-110">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="d888d-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="d888d-111">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="d888d-111">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="d888d-112">Selecteer op de labblade **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="d888d-112">On the lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="d888d-113">Op de testomgeving **instellingen** blade Selecteer **Lab kosten trend**.</span><span class="sxs-lookup"><span data-stu-id="d888d-113">On the lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="d888d-114">De volgende Schermafbeelding toont een voorbeeld van een grafiek kosten.</span><span class="sxs-lookup"><span data-stu-id="d888d-114">The following screen shot shows an example of a cost chart.</span></span> 
   
    ![Kosten grafiek](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="d888d-116">De **geschatte kosten** waarde is de huidige kalendermaand geschatte kosten-to-date.</span><span class="sxs-lookup"><span data-stu-id="d888d-116">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="d888d-117">De **geschatte kosten** de geschatte kosten voor de hele huidige kalendermaand is berekend met behulp van de kosten van het testlab voor de afgelopen vijf dagen.</span><span class="sxs-lookup"><span data-stu-id="d888d-117">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span></span>

<span data-ttu-id="d888d-118">De kosten zijn afgerond naar het dichtstbijzijnde gehele getal.</span><span class="sxs-lookup"><span data-stu-id="d888d-118">The cost amounts are rounded up to the next whole number.</span></span> <span data-ttu-id="d888d-119">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d888d-119">For example:</span></span> 

* <span data-ttu-id="d888d-120">5.01 Rondt maximaal 6</span><span class="sxs-lookup"><span data-stu-id="d888d-120">5.01 rounds up to 6</span></span> 
* <span data-ttu-id="d888d-121">5.50 Rondt maximaal 6</span><span class="sxs-lookup"><span data-stu-id="d888d-121">5.50 rounds up to 6</span></span>
* <span data-ttu-id="d888d-122">5.99 Rondt maximaal 6</span><span class="sxs-lookup"><span data-stu-id="d888d-122">5.99 rounds up to 6</span></span>

<span data-ttu-id="d888d-123">Als deze boven het diagram, raken de kosten die u in de grafiek ziet worden *geschatte* via [betalen naar gebruik](https://azure.microsoft.com/offers/ms-azr-0003p/) tarieven aanbieden.</span><span class="sxs-lookup"><span data-stu-id="d888d-123">As it states above the chart, the costs you see in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="d888d-124">Daarnaast volgen *niet* opgenomen in de kostenberekening:</span><span class="sxs-lookup"><span data-stu-id="d888d-124">Additionally, the following are *not* included in the cost calculation:</span></span>

* <span data-ttu-id="d888d-125">CSP en Dreamspark abonnementen worden momenteel niet ondersteund als Azure DevTest Labs gebruikt de [Azure facturering API's](../billing/billing-usage-rate-card-overview.md) voor het berekenen van de testomgeving kosten, die geen ondersteuning biedt voor CSP of Dreamspark abonnementen.</span><span class="sxs-lookup"><span data-stu-id="d888d-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="d888d-126">De tarieven van de aanbieding.</span><span class="sxs-lookup"><span data-stu-id="d888d-126">Your offer rates.</span></span> <span data-ttu-id="d888d-127">Op dit moment kunnen kunnen we geen gebruik van de tarieven van de aanbieding (die wordt weergegeven onder uw abonnement) dat u hebt onderhandeld met Microsoft of Microsoft partners.</span><span class="sxs-lookup"><span data-stu-id="d888d-127">Currently, we are not able to use your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="d888d-128">We gebruiken de tarieven voor betalen per gebruik.</span><span class="sxs-lookup"><span data-stu-id="d888d-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="d888d-129">Uw belastingen</span><span class="sxs-lookup"><span data-stu-id="d888d-129">Your taxes</span></span>
* <span data-ttu-id="d888d-130">Uw kortingen</span><span class="sxs-lookup"><span data-stu-id="d888d-130">Your discounts</span></span>
* <span data-ttu-id="d888d-131">Uw factureringsvaluta.</span><span class="sxs-lookup"><span data-stu-id="d888d-131">Your billing currency.</span></span> <span data-ttu-id="d888d-132">Op dit moment wordt de kosten van het testlab alleen weergegeven in valuta USD.</span><span class="sxs-lookup"><span data-stu-id="d888d-132">Currently, the lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="d888d-133">Verwante blogberichten</span><span class="sxs-lookup"><span data-stu-id="d888d-133">Related blog posts</span></span>
* [<span data-ttu-id="d888d-134">Twee meer dingen te houden van uw kosten op bijhouden in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="d888d-134">Two more things to keep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="d888d-135">Waarom kosten drempelwaarden?</span><span class="sxs-lookup"><span data-stu-id="d888d-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="d888d-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d888d-136">Next steps</span></span>
<span data-ttu-id="d888d-137">Hier volgen enkele dingen om te proberen het volgende:</span><span class="sxs-lookup"><span data-stu-id="d888d-137">Here are some things to try next:</span></span>

* <span data-ttu-id="d888d-138">[Labbeleidsregels definiëren](devtest-lab-set-lab-policy.md) -informatie over het instellen van de verschillende beleidsregels gebruikt om te bepalen hoe uw lab en bijbehorende virtuele machines worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d888d-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="d888d-139">[Maken van aangepaste installatiekopie](devtest-lab-create-template.md) : wanneer u een virtuele machine, maakt u een basis, kan dit een aangepaste installatiekopie of een Marketplace-installatiekopie opgeven.</span><span class="sxs-lookup"><span data-stu-id="d888d-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="d888d-140">In dit artikel laat zien hoe een aangepaste installatiekopie maken van een VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="d888d-140">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="d888d-141">[Configureren van installatiekopieën van Marketplace](devtest-lab-configure-marketplace-images.md) - DevTest Labs ondersteunt het maken van virtuele machines op basis van Azure Marketplace-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="d888d-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="d888d-142">Dit artikel wordt beschreven hoe u kunt opgeven die, indien aanwezig, Azure Marketplace-installatiekopieën kunnen worden gebruikt bij het maken van virtuele machines in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d888d-142">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="d888d-143">[Een virtuele machine maken in een testomgeving](devtest-lab-add-vm-with-artifacts.md) -ziet u hoe u een virtuele machine maken van een basisinstallatiekopie (een aangepaste of Marketplace), en het werken met artefacten in uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d888d-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

