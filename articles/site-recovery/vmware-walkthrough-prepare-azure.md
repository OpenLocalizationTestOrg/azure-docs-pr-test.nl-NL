---
title: aaaPrepare Azure-resources tooreplicate lokale virtuele VMware-machines tooAzure met Azure Site Recovery | Microsoft Docs
description: Beschrijft wat u moet in de Azure voordat u begint met het repliceren van de lokale virtuele VMware-machines tooAzure met Azure Site Recovery
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
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ac72fff0593783add789408ecfeb1812d70108b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-tooazure"></a><span data-ttu-id="efdcc-103">Stap 5: Azure-resources voor VMWare replicatie tooAzure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="efdcc-103">Step 5: Prepare Azure resources for VMWare replication tooAzure</span></span>


<span data-ttu-id="efdcc-104">Volg Hallo-instructies in dit artikel tooprepare Azure resources zodat u kunt repliceren lokale machines tooAzure Hallo met [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="efdcc-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises machines tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="efdcc-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="efdcc-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="efdcc-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="efdcc-106">Before you start</span></span>

<span data-ttu-id="efdcc-107">Zorg ervoor dat u hebt Hallo gelezen [vereisten](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="efdcc-107">Make sure you've read hello [prerequisites](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="efdcc-108">Een Azure-account instellen</span><span class="sxs-lookup"><span data-stu-id="efdcc-108">Set up an Azure account</span></span>

- <span data-ttu-id="efdcc-109">Ophalen van een [Microsoft Azure-account](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="efdcc-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="efdcc-110">U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="efdcc-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="efdcc-111">Hallo ondersteunde regio's controleren voor de Site is hersteld, onder geografische beschikbaarheid in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="efdcc-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="efdcc-112">Meer informatie over [prijzen voor Site Recovery](site-recovery-faq.md#pricing), en krijgt u Hallo [prijsinformatie](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="efdcc-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="efdcc-113">Een Azure-netwerk instellen</span><span class="sxs-lookup"><span data-stu-id="efdcc-113">Set up an Azure network</span></span>

- <span data-ttu-id="efdcc-114">Een Azure-netwerk instellen.</span><span class="sxs-lookup"><span data-stu-id="efdcc-114">Set up an Azure network.</span></span> <span data-ttu-id="efdcc-115">Virtuele machines in Azure worden geplaatst in dit netwerk wanneer ze zijn gemaakt na een failover.</span><span class="sxs-lookup"><span data-stu-id="efdcc-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="efdcc-116">Site Recovery in hello Azure-portal kunt instellen netwerken [Resource Manager](../resource-manager-deployment-model.md), of in de klassieke modus.</span><span class="sxs-lookup"><span data-stu-id="efdcc-116">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="efdcc-117">Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="efdcc-117">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="efdcc-118">Meer informatie over [virtueel netwerk prijzen](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="efdcc-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="efdcc-119">Meer informatie over [Azure VM-connectiviteit](site-recovery-network-design.md) na een failover.</span><span class="sxs-lookup"><span data-stu-id="efdcc-119">Learn more about [Azure VM connectivity](site-recovery-network-design.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="efdcc-120">Een Azure-opslagaccount instellen</span><span class="sxs-lookup"><span data-stu-id="efdcc-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="efdcc-121">Site Recovery repliceert tooAzure opslag voor lokale machines.</span><span class="sxs-lookup"><span data-stu-id="efdcc-121">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="efdcc-122">Virtuele machines in Azure worden gemaakt van Hallo opslag nadat de failover plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="efdcc-122">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="efdcc-123">Instellen van een [Azure storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account) voor gerepliceerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="efdcc-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="efdcc-124">Site Recovery in hello Azure-portal kunt instellen in Resource Manager, of in de klassieke modus storage-accounts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="efdcc-124">Site Recovery in hello Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="efdcc-125">Hallo storage-account kan worden standaard of [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="efdcc-125">hello storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="efdcc-126">Als u een premium-account hebt ingesteld, moet u ook een extra standaardaccount voor logboekgegevens.</span><span class="sxs-lookup"><span data-stu-id="efdcc-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="efdcc-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="efdcc-127">Next steps</span></span>

<span data-ttu-id="efdcc-128">Ga te[stap 6: VMware voorbereiden resources](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="efdcc-128">Go too[Step 6: Prepare VMware resources](vmware-walkthrough-prepare-vmware.md)</span></span>
