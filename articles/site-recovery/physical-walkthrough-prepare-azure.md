---
title: aaaPrepare Azure-resources tooreplicate lokale fysieke servers tooAzure met Azure Site Recovery | Microsoft Docs
description: Beschrijft wat u moet in de Azure voordat u lokale servers tooAzure, repliceren met behulp van hello Azure Site Recovery-service
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b1d008dac278bc7797188a3c9c15f2a3b5fe12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a><span data-ttu-id="60a63-103">Stap 5: Azure-resources voor de fysieke server replicatie tooAzure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="60a63-103">Step 5: Prepare Azure resources for physical server replication tooAzure</span></span>


<span data-ttu-id="60a63-104">Volg Hallo-instructies in dit artikel tooprepare Azure resources zodat u kunt repliceren lokale servers tooAzure Hallo met [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="60a63-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="60a63-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="60a63-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="60a63-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="60a63-106">Before you start</span></span>

<span data-ttu-id="60a63-107">Zorg ervoor dat u hebt Hallo gelezen [vereisten](physical-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="60a63-107">Make sure you've read hello [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="60a63-108">Een Azure-account instellen</span><span class="sxs-lookup"><span data-stu-id="60a63-108">Set up an Azure account</span></span>

- <span data-ttu-id="60a63-109">Ophalen van een [Microsoft Azure-account](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="60a63-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="60a63-110">U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60a63-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="60a63-111">Hallo ondersteunde regio's onder controleren voor de Site Recovery **geografische beschikbaarheid** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="60a63-111">Check hello supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="60a63-112">Meer informatie over [prijzen voor Site Recovery](site-recovery-faq.md#pricing), en krijgt u Hallo [prijsinformatie](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="60a63-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="60a63-113">Een Azure-netwerk instellen</span><span class="sxs-lookup"><span data-stu-id="60a63-113">Set up an Azure network</span></span>

- <span data-ttu-id="60a63-114">Een Azure-netwerk instellen.</span><span class="sxs-lookup"><span data-stu-id="60a63-114">Set up an Azure network.</span></span> <span data-ttu-id="60a63-115">Virtuele machines in Azure worden geplaatst in dit netwerk wanneer ze zijn gemaakt na een failover.</span><span class="sxs-lookup"><span data-stu-id="60a63-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="60a63-116">Site Recovery in hello Azure-portal kunt instellen netwerken [Resource Manager](../resource-manager-deployment-model.md), of in de klassieke modus.</span><span class="sxs-lookup"><span data-stu-id="60a63-116">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="60a63-117">Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="60a63-117">hello network should be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="60a63-118">Meer informatie over [virtueel netwerk prijzen](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="60a63-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="60a63-119">Meer informatie over [Azure VM-connectiviteit](physical-walkthrough-network.md) na een failover.</span><span class="sxs-lookup"><span data-stu-id="60a63-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="60a63-120">Een Azure-opslagaccount instellen</span><span class="sxs-lookup"><span data-stu-id="60a63-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="60a63-121">Site Recovery repliceert lokale servers tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="60a63-121">Site Recovery replicates on-premises servers tooAzure storage.</span></span> <span data-ttu-id="60a63-122">Virtuele machines in Azure worden gemaakt van Hallo opslag nadat de failover plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="60a63-122">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="60a63-123">Instellen van een [Azure storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account) voor gerepliceerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="60a63-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="60a63-124">Site Recovery in hello Azure-portal kunt instellen in Resource Manager, of in de klassieke modus storage-accounts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="60a63-124">Site Recovery in hello Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="60a63-125">Hallo storage-account kan worden standaard of [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="60a63-125">hello storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="60a63-126">Als u een premium-account hebt ingesteld, moet u ook een extra standaardaccount voor logboekgegevens.</span><span class="sxs-lookup"><span data-stu-id="60a63-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="60a63-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="60a63-127">Next steps</span></span>

<span data-ttu-id="60a63-128">Ga te[stap 6: een kluis instellen](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="60a63-128">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>
