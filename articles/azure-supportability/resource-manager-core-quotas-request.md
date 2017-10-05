---
title: Azure Resource Manager core quotum verhogen aanvragen | Microsoft Docs
description: Azure Resource Manager core quotum verhogen aanvragen
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a><span data-ttu-id="8a6d8-103">Resource Manager core quotum verhogen aanvragen</span><span class="sxs-lookup"><span data-stu-id="8a6d8-103">Resource Manager core quota increase requests</span></span>

<span data-ttu-id="8a6d8-104">Resource Manager core quota worden afgedwongen op het regioniveau en de SKU-familie niveau.</span><span class="sxs-lookup"><span data-stu-id="8a6d8-104">Resource Manager core quotas are enforced at the region level and SKU family level.</span></span>
<span data-ttu-id="8a6d8-105">Meer informatie over hoe quota's worden toegepast op de [Azure-abonnement en Servicelimieten](http://aka.ms/quotalimits) pagina.</span><span class="sxs-lookup"><span data-stu-id="8a6d8-105">Learn more about how quotas are enforced on the [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="8a6d8-106">Voor meer informatie over de SKU-Families, kunt u kosten en prestaties vergelijken op de [prijzen van virtuele Machines](http://aka.ms/pricingcompute) pagina.</span><span class="sxs-lookup"><span data-stu-id="8a6d8-106">To learn more about SKU Families, you may compare cost and performance on the [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="8a6d8-107">Voor een verhoging aanvragen, maakt u een ondersteuningsaanvraag quotum voor kernen in de Azure portal [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8a6d8-107">To request an increase, create a Quota support case for Cores in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="8a6d8-108">Meer informatie over hoe [Maak een ondersteuningsaanvraag](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="8a6d8-108">Learn how to [create a support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in the Azure portal</span></span>

1. <span data-ttu-id="8a6d8-109">Selecteer type probleem als 'Target' en quotumtype als 'Kernen' op de pagina nieuwe ondersteuning aanvraag.</span><span class="sxs-lookup"><span data-stu-id="8a6d8-109">On the new support request page, select Issue type as "Quota" and Quota type as "Cores".</span></span>

    ![De blade grondbeginselen quotum](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. <span data-ttu-id="8a6d8-111">Selecteer implementatiemodel als 'Resource Manager' en selecteer een locatie.</span><span class="sxs-lookup"><span data-stu-id="8a6d8-111">Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![Quota voor probleem-blade](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="8a6d8-113">Selecteer de SKU-Families waarvoor verhogen.</span><span class="sxs-lookup"><span data-stu-id="8a6d8-113">Select the SKU Families that require an increase.</span></span>

    ![SKU-serie geselecteerd](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="8a6d8-115">Voer de nieuwe beperkingen die u wilt dat op het abonnement.</span><span class="sxs-lookup"><span data-stu-id="8a6d8-115">Enter the new limits you would like on the subscription.</span></span>

    ![Nieuwe quotumaanvraag SKU](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="8a6d8-117">Een regel verwijderen, schakelt u de SKU van de SKU-familie dropdown of klik op het pictogram 'x' negeren.</span><span class="sxs-lookup"><span data-stu-id="8a6d8-117">To remove a line, uncheck the SKU from the SKU family dropdown or click the discard "x" icon.</span></span>
<span data-ttu-id="8a6d8-118">Na het invoeren van de gewenste quota voor elke SKU-serie, klikt u op 'Volgende' op de pagina probleem stap om door te gaan met het maken van de aanvraag voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="8a6d8-118">After entering the desired quota for each SKU family, click "Next" on the Problem step page to continue with the support request creation.</span></span>
