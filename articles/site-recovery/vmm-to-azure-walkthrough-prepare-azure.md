---
title: Azure-resources voor de virtuele Hyper-V-machines (met System Center VMM) repliceren naar Azure met Azure Site Recovery voorbereiden | Microsoft Docs
description: Beschrijft wat u moet in de Azure voordat u begint met Hyper-V-machines (met VMM) repliceren naar Azure met behulp van Azure Site Recovery
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
ms.openlocfilehash: 63b005f37ab5e15e8a1b4645446d65f1529f1bbd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-to-azure"></a><span data-ttu-id="712a3-103">Stap 5: Azure-resources voorbereiden voor Hyper-V-replicatie (met VMM) naar Azure</span><span class="sxs-lookup"><span data-stu-id="712a3-103">Step 5: Prepare Azure resources for Hyper-V replication (with VMM) to Azure</span></span>

<span data-ttu-id="712a3-104">Nadat u hebt gecontroleerd [vereisten](vmm-to-azure-walkthrough-network.md), volg de instructies in dit artikel voor het voorbereiden van Azure-resources, zodat u kunt lokale Hyper-V-machines in System Center Virtual Machine Manager (VMM)-clouds repliceren naar Azure met behulp van de [ Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="712a3-104">After verifying [network requirements](vmm-to-azure-walkthrough-network.md), use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="712a3-105">Na het lezen van dit artikel, eventuele opmerkingen posten onder of technische vragen op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="712a3-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-an-azure-account"></a><span data-ttu-id="712a3-106">Een Azure-account instellen</span><span class="sxs-lookup"><span data-stu-id="712a3-106">Set up an Azure account</span></span>

- <span data-ttu-id="712a3-107">Ophalen van een [Microsoft Azure-account](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="712a3-107">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="712a3-108">U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="712a3-108">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="712a3-109">Controleer de ondersteunde regio's voor herstel van sites, onder geografische beschikbaarheid in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="712a3-109">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="712a3-110">Meer informatie over [prijzen voor Site Recovery](site-recovery-faq.md#pricing), en de [prijsinformatie](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="712a3-110">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="712a3-111">Zorg ervoor dat uw Azure-account de juiste [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)Azure virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="712a3-111">Make sure your Azure account has the correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)to create Azure VMs.</span></span> <span data-ttu-id="712a3-112">[Meer informatie](../active-directory/role-based-access-built-in-roles.md) over op rollen gebaseerd toegangsbeheer van Azure.</span><span class="sxs-lookup"><span data-stu-id="712a3-112">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="712a3-113">Een Azure-netwerk instellen</span><span class="sxs-lookup"><span data-stu-id="712a3-113">Set up an Azure network</span></span>

- <span data-ttu-id="712a3-114">Instellen van een [Azure-netwerk](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="712a3-114">Set up an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span></span> <span data-ttu-id="712a3-115">Virtuele machines in Azure worden geplaatst in dit netwerk wanneer ze zijn gemaakt na een failover.</span><span class="sxs-lookup"><span data-stu-id="712a3-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="712a3-116">Het netwerk moet zich in dezelfde regio bevinden als de Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="712a3-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="712a3-117">Site Recovery in de Azure portal kunt instellen netwerken [Resource Manager](../resource-manager-deployment-model.md), of in de klassieke modus.</span><span class="sxs-lookup"><span data-stu-id="712a3-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="712a3-118">U doet er verstandig aan een netwerk in te stellen voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="712a3-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="712a3-119">Anders moet u dit doen tijdens de implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="712a3-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="712a3-120">Meer informatie over [virtueel netwerk prijzen](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="712a3-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="712a3-121">Een Azure-opslagaccount instellen</span><span class="sxs-lookup"><span data-stu-id="712a3-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="712a3-122">Lokale-machines van de site Recovery worden gerepliceerd naar Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="712a3-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="712a3-123">Virtuele machines in Azure worden gemaakt van de opslag nadat de failover plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="712a3-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="712a3-124">Instellen van een standaard/premium [Azure storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account) voor gegevens gerepliceerd naar Azure.</span><span class="sxs-lookup"><span data-stu-id="712a3-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="712a3-125">[Premium-opslag](../storage/common/storage-premium-storage.md) wordt doorgaans gebruikt voor virtuele machines die een consistent hoge i/o-prestaties en lage latentie host i/o-intensieve werkbelastingen nodig.</span><span class="sxs-lookup"><span data-stu-id="712a3-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="712a3-126">Als u een Premium-account wilt gebruiken om gerepliceerde gegevens op te slaan, hebt u ook een Standard-opslagaccount nodig om replicatielogboeken op te slaan waarin de doorlopende wijzigingen in uw on-premises gegevens worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="712a3-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="712a3-127">Afhankelijk van het resourcemodel dat u wilt gebruiken voor failover is uitgevoerd op Azure Virtual machines, instellen van een account in [modus Resource Manager](../storage/common/storage-create-storage-account.md), of [klassieke modus](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="712a3-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="712a3-128">Het is raadzaam dat u een opslagaccount instellen voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="712a3-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="712a3-129">U moet dit doen tijdens de implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="712a3-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="712a3-130">De accounts moeten in dezelfde regio bevinden als de Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="712a3-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="712a3-131">U kunt de storage-accounts die zijn gebruikt door Site Recovery via resourcegroepen binnen hetzelfde abonnement of via verschillende abonnementen niet verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="712a3-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="712a3-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="712a3-132">Next steps</span></span>

<span data-ttu-id="712a3-133">Ga naar [stap 6: VMM voorbereiden](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="712a3-133">Go to [Step 6: Prepare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>
