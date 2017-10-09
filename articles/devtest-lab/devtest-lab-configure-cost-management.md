---
title: aaaView hello maandelijkse lab geschatte kosten trend in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hello Azure DevTest Labs maandelijkse geschatte kosten trend van grafiek.
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
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="f969a-103">Weergave Hallo maandelijkse lab geschatte kosten trend in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f969a-103">View hello monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="f969a-104">Hallo kostenbeheer functie van DevTest Labs kunt u bijhouden Hallo kosten van uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f969a-104">hello Cost Management feature of DevTest Labs helps you track hello cost of your lab.</span></span> <span data-ttu-id="f969a-105">Dit artikel wordt beschreven hoe toouse hello **maandelijkse geschatte kosten Trend** grafiek tooview Hallo van het huidige kalendermaand geschatte kosten-to-date en de kosten van het verwachte einde van de maand voor Hallo Hallo huidige kalendermaand.</span><span class="sxs-lookup"><span data-stu-id="f969a-105">This article illustrates how toouse hello **Monthly Estimated Cost Trend** chart tooview hello current calendar month's estimated cost-to-date and hello projected end-of-month cost for hello current calendar month.</span></span> <span data-ttu-id="f969a-106">In dit artikel leert u hoe tooview Hallo maandelijkse geschatte kosten trend grafiek in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f969a-106">In this article, you learn how tooview hello monthly estimated cost trend chart in hello Azure portal.</span></span>

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="f969a-107">Hallo maandelijkse geschatte kosten Trend grafiek weergeven</span><span class="sxs-lookup"><span data-stu-id="f969a-107">Viewing hello Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="f969a-108">tooview hello maandelijkse geschatte kosten Trend grafiek, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="f969a-108">tooview hello Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="f969a-109">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f969a-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f969a-110">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="f969a-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="f969a-111">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="f969a-111">From hello list of labs, select hello desired lab.</span></span>   
4. <span data-ttu-id="f969a-112">Selecteer op Hallo van labblade, **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="f969a-112">On hello lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="f969a-113">Op de Hallo lab **instellingen** blade Selecteer **Lab kosten trend**.</span><span class="sxs-lookup"><span data-stu-id="f969a-113">On hello lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="f969a-114">Hallo toont volgende schermafbeelding een voorbeeld van een grafiek kosten.</span><span class="sxs-lookup"><span data-stu-id="f969a-114">hello following screen shot shows an example of a cost chart.</span></span> 
   
    ![Kosten grafiek](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="f969a-116">Hallo **geschatte kosten** waarde is van het huidige kalendermaand geschatte kosten-to-date Hallo.</span><span class="sxs-lookup"><span data-stu-id="f969a-116">hello **Estimated cost** value is hello current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="f969a-117">Hallo **geschatte kosten** hello geschatte kosten voor de hele Hallo huidige kalendermaand berekend met behulp van Hallo labkosten voor Hallo vorige vijf dagen.</span><span class="sxs-lookup"><span data-stu-id="f969a-117">hello **Projected cost** is hello estimated cost for hello entire current calendar month, calculated using hello lab cost for hello previous five days.</span></span>

<span data-ttu-id="f969a-118">Hallo-kosten zijn toohello dichtstbijzijnde gehele getal afgerond.</span><span class="sxs-lookup"><span data-stu-id="f969a-118">hello cost amounts are rounded up toohello next whole number.</span></span> <span data-ttu-id="f969a-119">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f969a-119">For example:</span></span> 

* <span data-ttu-id="f969a-120">5.01 rondt af too6 naar boven</span><span class="sxs-lookup"><span data-stu-id="f969a-120">5.01 rounds up too6</span></span> 
* <span data-ttu-id="f969a-121">5.50 rondt af too6 naar boven</span><span class="sxs-lookup"><span data-stu-id="f969a-121">5.50 rounds up too6</span></span>
* <span data-ttu-id="f969a-122">5.99 rondt af too6 naar boven</span><span class="sxs-lookup"><span data-stu-id="f969a-122">5.99 rounds up too6</span></span>

<span data-ttu-id="f969a-123">Stelt boven Hallo diagram, u in de grafiek Hallo ziet Hallo-kosten zijn *geschatte* via [betalen naar gebruik](https://azure.microsoft.com/offers/ms-azr-0003p/) tarieven aanbieden.</span><span class="sxs-lookup"><span data-stu-id="f969a-123">As it states above hello chart, hello costs you see in hello chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="f969a-124">Bovendien Hallo volgen *niet* opgenomen in Hallo kostenberekening:</span><span class="sxs-lookup"><span data-stu-id="f969a-124">Additionally, hello following are *not* included in hello cost calculation:</span></span>

* <span data-ttu-id="f969a-125">CSP en Dreamspark abonnementen worden momenteel niet ondersteund als Hallo maakt gebruik van Azure DevTest Labs [Azure facturering API's](../billing/billing-usage-rate-card-overview.md) toocalculate Hallo lab kosten, die geen ondersteuning biedt voor CSP of Dreamspark abonnementen.</span><span class="sxs-lookup"><span data-stu-id="f969a-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses hello [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) toocalculate hello lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="f969a-126">De tarieven van de aanbieding.</span><span class="sxs-lookup"><span data-stu-id="f969a-126">Your offer rates.</span></span> <span data-ttu-id="f969a-127">Er zijn momenteel niet kunnen toouse de tarieven van de aanbieding (die wordt weergegeven onder uw abonnement) dat u hebt onderhandeld met Microsoft of Microsoft partners.</span><span class="sxs-lookup"><span data-stu-id="f969a-127">Currently, we are not able toouse your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="f969a-128">We gebruiken de tarieven voor betalen per gebruik.</span><span class="sxs-lookup"><span data-stu-id="f969a-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="f969a-129">Uw belastingen</span><span class="sxs-lookup"><span data-stu-id="f969a-129">Your taxes</span></span>
* <span data-ttu-id="f969a-130">Uw kortingen</span><span class="sxs-lookup"><span data-stu-id="f969a-130">Your discounts</span></span>
* <span data-ttu-id="f969a-131">Uw factureringsvaluta.</span><span class="sxs-lookup"><span data-stu-id="f969a-131">Your billing currency.</span></span> <span data-ttu-id="f969a-132">Op dit moment wordt Hallo labkosten alleen weergegeven in valuta USD.</span><span class="sxs-lookup"><span data-stu-id="f969a-132">Currently, hello lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="f969a-133">Verwante blogberichten</span><span class="sxs-lookup"><span data-stu-id="f969a-133">Related blog posts</span></span>
* [<span data-ttu-id="f969a-134">Twee meer dingen tookeep uw kosten op bijhouden in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f969a-134">Two more things tookeep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="f969a-135">Waarom kosten drempelwaarden?</span><span class="sxs-lookup"><span data-stu-id="f969a-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="f969a-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f969a-136">Next steps</span></span>
<span data-ttu-id="f969a-137">Hier volgen enkele dingen tootry vervolgens:</span><span class="sxs-lookup"><span data-stu-id="f969a-137">Here are some things tootry next:</span></span>

* <span data-ttu-id="f969a-138">[Labbeleidsregels definiëren](devtest-lab-set-lab-policy.md) -informatie over hoe tooset verschillende beleidsregels gebruikt Hallo toogovern hoe uw lab en bijbehorende virtuele machines worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f969a-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how tooset hello various policies used toogovern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="f969a-139">[Maken van aangepaste installatiekopie](devtest-lab-create-template.md) : wanneer u een virtuele machine, maakt u een basis, kan dit een aangepaste installatiekopie of een Marketplace-installatiekopie opgeven.</span><span class="sxs-lookup"><span data-stu-id="f969a-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="f969a-140">In dit artikel ziet u hoe toocreate een aangepaste installatiekopie van een VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="f969a-140">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="f969a-141">[Configureren van installatiekopieën van Marketplace](devtest-lab-configure-marketplace-images.md) - DevTest Labs ondersteunt het maken van virtuele machines op basis van Azure Marketplace-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="f969a-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="f969a-142">Dit artikel wordt beschreven hoe toospecify die, indien aanwezig, Azure Marketplace-installatiekopieën kunnen worden gebruikt bij het maken van virtuele machines in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f969a-142">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="f969a-143">[Een virtuele machine maken in een testomgeving](devtest-lab-add-vm-with-artifacts.md) -ziet u hoe een virtuele machine uit een basisinstallatiekopie toocreate (ofwel aangepaste of Marketplace), en hoe toowork met artefacten in uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f969a-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

