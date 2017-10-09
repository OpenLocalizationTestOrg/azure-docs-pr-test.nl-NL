---
title: aaaPrepare Azure-resources tooreplicate Hyper-V-machines (met System Center VMM) tooAzure met Azure Site Recovery | Microsoft Docs
description: Beschrijft wat u moet in de Azure voordat u begint Hyper-V-machines (met VMM)-tooAzure repliceren met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1568bdc3-e767-477b-b040-f13699ab5644
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 86bfbab7722fe5bd5b93b92e398d1d441505d3b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="83348-103">Stap 5: Voorbereiden op Azure-resources tooAzure voor Hyper-V-replicatie (met VMM)</span><span class="sxs-lookup"><span data-stu-id="83348-103">Step 5: Prepare Azure resources for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="83348-104">Nadat u hebt gecontroleerd [vereisten voor de](vmm-to-azure-walkthrough-network.md), volg Hallo-instructies in dit artikel tooprepare Azure resources met behulp van zodat u lokale Hyper-V-machines in System Center Virtual Machine Manager (VMM) clouds tooAzure repliceren kunt, Hallo [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="83348-104">After verifying [network requirements](vmm-to-azure-walkthrough-network.md), use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="83348-105">Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="83348-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-an-azure-account"></a><span data-ttu-id="83348-106">Een Azure-account instellen</span><span class="sxs-lookup"><span data-stu-id="83348-106">Set up an Azure account</span></span>

- <span data-ttu-id="83348-107">Ophalen van een [Microsoft Azure-account](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="83348-107">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="83348-108">U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83348-108">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="83348-109">Hallo ondersteunde regio's controleren voor de Site is hersteld, onder geografische beschikbaarheid in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="83348-109">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="83348-110">Meer informatie over [prijzen voor Site Recovery](site-recovery-faq.md#pricing), en krijgt u Hallo [prijsinformatie](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="83348-110">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="83348-111">Zorg ervoor dat uw Azure-account juist Hallo [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate virtuele Azure-machines.</span><span class="sxs-lookup"><span data-stu-id="83348-111">Make sure your Azure account has hello correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure VMs.</span></span> <span data-ttu-id="83348-112">[Meer informatie](../active-directory/role-based-access-built-in-roles.md) over op rollen gebaseerd toegangsbeheer van Azure.</span><span class="sxs-lookup"><span data-stu-id="83348-112">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="83348-113">Een Azure-netwerk instellen</span><span class="sxs-lookup"><span data-stu-id="83348-113">Set up an Azure network</span></span>

- <span data-ttu-id="83348-114">Instellen van een [Azure-netwerk](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="83348-114">Set up an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span></span> <span data-ttu-id="83348-115">Virtuele machines in Azure worden geplaatst in dit netwerk wanneer ze zijn gemaakt na een failover.</span><span class="sxs-lookup"><span data-stu-id="83348-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="83348-116">Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="83348-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="83348-117">Site Recovery in hello Azure-portal kunt instellen netwerken [Resource Manager](../resource-manager-deployment-model.md), of in de klassieke modus.</span><span class="sxs-lookup"><span data-stu-id="83348-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="83348-118">U doet er verstandig aan een netwerk in te stellen voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="83348-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="83348-119">Als u dat niet doet, moet u toodo tijdens de implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="83348-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="83348-120">Meer informatie over [virtueel netwerk prijzen](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="83348-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="83348-121">Een Azure-opslagaccount instellen</span><span class="sxs-lookup"><span data-stu-id="83348-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="83348-122">Site Recovery repliceert tooAzure opslag voor lokale machines.</span><span class="sxs-lookup"><span data-stu-id="83348-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="83348-123">Virtuele machines in Azure worden gemaakt van Hallo opslag nadat de failover plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="83348-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="83348-124">Instellen van een standaard/premium [Azure storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold gegevens gerepliceerd tooAzure.</span><span class="sxs-lookup"><span data-stu-id="83348-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="83348-125">[Premium-opslag](../storage/common/storage-premium-storage.md) wordt doorgaans gebruikt voor virtuele machines die een consistent hoge i/o-prestaties en lage latentie toohost i/o-intensieve werkbelastingen nodig.</span><span class="sxs-lookup"><span data-stu-id="83348-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="83348-126">Als u wilt dat toouse een premium account toostore gerepliceerde gegevens, moet u ook een standard-opslag account toostore replicatielogboeken dat vastleggen lopende tooon-premises gegevens is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="83348-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="83348-127">Afhankelijk van het resourcemodel Hallo gewenste toouse voor failover is uitgevoerd op Azure Virtual machines, instellen van een account in [modus Resource Manager](../storage/common/storage-create-storage-account.md), of [klassieke modus](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="83348-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="83348-128">Het is raadzaam dat u een opslagaccount instellen voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="83348-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="83348-129">U moet toodo tijdens de implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="83348-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="83348-130">Hallo-accounts moeten in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="83348-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="83348-131">U kunt niet verplaatsen storage-accounts gebruikt door Site Recovery via resourcegroepen binnen Hallo dezelfde abonnement, of tussen verschillende abonnementen behoren.</span><span class="sxs-lookup"><span data-stu-id="83348-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="83348-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="83348-132">Next steps</span></span>

<span data-ttu-id="83348-133">Ga te[stap 6: VMM voorbereiden](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="83348-133">Go too[Step 6: Prepare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>
