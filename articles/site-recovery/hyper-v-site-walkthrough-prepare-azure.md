---
title: aaaPrepare Azure-resources tooreplicate Hyper-V-machines (zonder de System Center VMM) tooAzure met Azure Site Recovery | Microsoft Docs
description: Beschrijft wat u moet in de Azure voordat u begint met het repliceren van Hyper-V-machines (zonder VMM) tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a><span data-ttu-id="83c1f-103">Stap 5: Azure-resources voor Hyper-V-replicatie tooAzure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="83c1f-103">Step 5: Prepare Azure resources for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="83c1f-104">Gebruik Hallo-instructies in dit artikel tooprepare Azure zodat u kunt repliceren lokale Hyper-V-machines (zonder de System Center VMM) met behulp van Hallo tooAzure [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="83c1f-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="83c1f-105">Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="83c1f-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="83c1f-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="83c1f-106">Before you start</span></span>

<span data-ttu-id="83c1f-107">Zorg ervoor dat u hebt Hallo gelezen [vereisten](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="83c1f-107">Make sure you've read hello [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="83c1f-108">Een Azure-account instellen</span><span class="sxs-lookup"><span data-stu-id="83c1f-108">Set up an Azure account</span></span>

- <span data-ttu-id="83c1f-109">Ophalen van een [Microsoft Azure-account](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="83c1f-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="83c1f-110">U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83c1f-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="83c1f-111">Hallo ondersteunde regio's controleren voor de Site is hersteld, onder geografische beschikbaarheid in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="83c1f-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="83c1f-112">Meer informatie over [prijzen voor Site Recovery](site-recovery-faq.md#pricing), en krijgt u Hallo [prijsinformatie](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="83c1f-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="83c1f-113">Een Azure-netwerk instellen</span><span class="sxs-lookup"><span data-stu-id="83c1f-113">Set up an Azure network</span></span>

- <span data-ttu-id="83c1f-114">Een Azure-netwerk instellen.</span><span class="sxs-lookup"><span data-stu-id="83c1f-114">Set up an Azure network.</span></span> <span data-ttu-id="83c1f-115">Virtuele machines in Azure worden geplaatst in dit netwerk wanneer ze zijn gemaakt na een failover.</span><span class="sxs-lookup"><span data-stu-id="83c1f-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="83c1f-116">Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="83c1f-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="83c1f-117">Site Recovery in hello Azure-portal kunt instellen netwerken [Resource Manager](../resource-manager-deployment-model.md), of in de klassieke modus.</span><span class="sxs-lookup"><span data-stu-id="83c1f-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="83c1f-118">U doet er verstandig aan een netwerk in te stellen voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="83c1f-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="83c1f-119">Als u dat niet doet, moet u toodo tijdens de implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="83c1f-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="83c1f-120">Meer informatie over [virtueel netwerk prijzen](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="83c1f-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="83c1f-121">Een Azure-opslagaccount instellen</span><span class="sxs-lookup"><span data-stu-id="83c1f-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="83c1f-122">Site Recovery repliceert tooAzure opslag voor lokale machines.</span><span class="sxs-lookup"><span data-stu-id="83c1f-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="83c1f-123">Virtuele machines in Azure worden gemaakt van Hallo opslag nadat de failover plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="83c1f-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="83c1f-124">Instellen van een standaard/premium [Azure storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold gegevens gerepliceerd tooAzure.</span><span class="sxs-lookup"><span data-stu-id="83c1f-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="83c1f-125">[Premium-opslag](../storage/common/storage-premium-storage.md) wordt doorgaans gebruikt voor virtuele machines die een consistent hoge i/o-prestaties en lage latentie toohost i/o-intensieve werkbelastingen nodig.</span><span class="sxs-lookup"><span data-stu-id="83c1f-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="83c1f-126">Als u wilt dat toouse een premium account toostore gerepliceerde gegevens, moet u ook een standard-opslag account toostore replicatielogboeken dat vastleggen lopende tooon-premises gegevens is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="83c1f-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="83c1f-127">Afhankelijk van het resourcemodel Hallo gewenste toouse voor failover is uitgevoerd op Azure Virtual machines, instellen van een account in [modus Resource Manager](../storage/common/storage-create-storage-account.md), of [klassieke modus](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="83c1f-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="83c1f-128">Het is raadzaam dat u een opslagaccount instellen voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="83c1f-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="83c1f-129">U moet toodo tijdens de implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="83c1f-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="83c1f-130">Hallo-accounts moeten in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="83c1f-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="83c1f-131">U kunt niet verplaatsen storage-accounts gebruikt door Site Recovery via resourcegroepen binnen Hallo dezelfde abonnement, of tussen verschillende abonnementen behoren.</span><span class="sxs-lookup"><span data-stu-id="83c1f-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="83c1f-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="83c1f-132">Next steps</span></span>

<span data-ttu-id="83c1f-133">Ga te[stap 6: Hyper-V voorbereiden resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="83c1f-133">Go too[Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
