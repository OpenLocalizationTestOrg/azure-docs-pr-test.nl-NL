---
title: aaaScale quota en limieten in uw lab in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe tooscale een lab in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="a0eb5-103">Schaal quota en limieten in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a0eb5-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="a0eb5-104">Als u in DevTest Labs werkt, kunt u wellicht opgevallen dat er zijn bepaalde limieten standaard toosome Azure-resources, die Hallo DevTest Labs service kunnen beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-104">As you work in DevTest Labs, you might notice that there are certain default limits toosome Azure resources, which can affect hello DevTest Labs service.</span></span> <span data-ttu-id="a0eb5-105">Deze limieten zijn waarnaar wordt verwezen tooas **quota**.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-105">These limits are referred tooas **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="a0eb5-106">Hallo DevTest Labs service kan geen quota's niet opleggen.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-106">hello DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="a0eb5-107">Quota's die u kunt tegenkomen zijn standaardbeperkingen Hallo algemene Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-107">Any quotas you might encounter are default constraints of hello overall Azure subscription.</span></span>

<span data-ttu-id="a0eb5-108">U kunt elke Azure-resource gebruiken totdat u het quotum bereikt.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="a0eb5-109">Elk abonnement heeft een afzonderlijke quota's en gebruik per abonnement wordt bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="a0eb5-110">Elk abonnement heeft bijvoorbeeld een standaardquotum van 20 kernen.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="a0eb5-111">Dus als u virtuele machines in uw testomgeving met vier cores maakt, kunt klikt u vervolgens u alleen maken vijf virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="a0eb5-112">[Azure-abonnement en Servicelimieten](https://docs.microsoft.com/azure/azure-subscription-service-limits) vindt u enkele van de meest voorkomende quota Hallo voor Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of hello most common quotas for Azure resources.</span></span> <span data-ttu-id="a0eb5-113">Hallo bronnen meestal gebruikt in een testomgeving en voor die u kunt tegenkomen quota, VM kernen, openbare IP-adressen, netwerkinterface, beheerde schijven, RBAC roltoewijzing en ExpressRoute-circuits bevatten.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-113">hello resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="a0eb5-114">Uw gebruik en quota's weergeven</span><span class="sxs-lookup"><span data-stu-id="a0eb5-114">View your usage and quotas</span></span>
<span data-ttu-id="a0eb5-115">Deze stappen ziet u hoe de tooview Hallo huidige quota's in uw abonnement voor specifieke Azure-resources en toosee welk percentage van elke quota die u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-115">These steps show you how tooview hello current quotas in your subscription for specific Azure resources, and toosee what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="a0eb5-116">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a0eb5-116">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="a0eb5-117">Selecteer **meer Services**, en selecteer vervolgens **facturering** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-117">Select **More Services**, and then select **Billing** from hello list.</span></span>
1. <span data-ttu-id="a0eb5-118">Selecteer in de blade facturering hello, een abonnement.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-118">In hello Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="a0eb5-119">Selecteer **gebruik + quota**.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-119">Select **Usage + quotas**.</span></span>

   ![Knop voor informatie over het gebruik en quota 's](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="a0eb5-121">Gebruik + quota Hallo blade wordt weergegeven, met verschillende bronnen beschikbaar zijn in het desbetreffende abonnement en Hallo percentage Hallo quota die per resource wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-121">hello Usage + quotas blade appears, listing different resources available in that subscription and hello percentage of hello quota that is being used per resource.</span></span>

   ![Quota's en gebruik](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="a0eb5-123">Aanvragen meer resources in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="a0eb5-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="a0eb5-124">Als u een quotum-limiet bereikt, de standaardlimiet Hallo van een resource in een abonnement kan worden verhoogd van tooa maximumlimiet, zoals beschreven in [Azure-abonnement en Servicelimieten](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="a0eb5-124">If you reach a quota cap, hello default limit of a resource in a subscription can be increased up tooa maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="a0eb5-125">Deze stappen ziet u hoe toorequest een quotum verhogen door Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a0eb5-125">These steps show you how toorequest a quota increase through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="a0eb5-126">Selecteer **meer Services**, selecteer **facturering**, en selecteer vervolgens **gebruik + quota**.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="a0eb5-127">Selecteer in het Hallo gebruik + quota blade Hallo **aanvragen verhogen** knop.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-127">In hello Usage + quotas blade, select hello **Request Increase** button.</span></span>

   ![Knop voor toename van aanvragen](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="a0eb5-129">toocomplete en Hallo aanvraag indienen, vul Hallo vereist op alle drie tabbladen Hallo **nieuw ondersteuningsverzoek** formulier.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-129">toocomplete and submit hello request, fill out hello required information on all three tabs of hello **New support request** form.</span></span>

   ![Toename aanvraagformulier](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="a0eb5-131">[Wat Azure limieten en toeneemt](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) vindt u meer informatie over het contact opnemen met ondersteuning van Azure toorequest een quotum verhogen.</span><span class="sxs-lookup"><span data-stu-id="a0eb5-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support toorequest a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="a0eb5-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0eb5-132">Next steps</span></span>
* <span data-ttu-id="a0eb5-133">Hallo verkennen [DevTest Labs Azure Resource Manager QuickStart sjablonengalerie](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="a0eb5-133">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
