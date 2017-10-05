---
title: Azure-resources voor het repliceren van fysieke on-premises servers naar Azure met Azure Site Recovery voorbereiden | Microsoft Docs
description: Beschrijft wat u moet in de Azure voordat u begint met het lokale servers repliceren naar Azure met behulp van de Azure Site Recovery-service
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
ms.openlocfilehash: b7411fa6aba04ffd34f3f4bd03e706ca75afc9c8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-to-azure"></a><span data-ttu-id="5674b-103">Stap 5: Azure-resources voorbereiden voor replicatie van de fysieke server naar Azure</span><span class="sxs-lookup"><span data-stu-id="5674b-103">Step 5: Prepare Azure resources for physical server replication to Azure</span></span>


<span data-ttu-id="5674b-104">Volg de instructies in dit artikel voor het voorbereiden van Azure-resources, zodat u lokale servers naar Azure worden verkregen met repliceren kunt de [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="5674b-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises servers to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="5674b-105">Opmerkingen en vragen plaatsen onder aan dit artikel of op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5674b-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5674b-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="5674b-106">Before you start</span></span>

<span data-ttu-id="5674b-107">Zorg ervoor dat u hebt gelezen de [vereisten](physical-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="5674b-107">Make sure you've read the [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="5674b-108">Een Azure-account instellen</span><span class="sxs-lookup"><span data-stu-id="5674b-108">Set up an Azure account</span></span>

- <span data-ttu-id="5674b-109">Ophalen van een [Microsoft Azure-account](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="5674b-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="5674b-110">U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5674b-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="5674b-111">Controleren van de ondersteunde regio's voor herstel van sites onder **geografische beschikbaarheid** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="5674b-111">Check the supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="5674b-112">Meer informatie over [prijzen voor Site Recovery](site-recovery-faq.md#pricing), en de [prijsinformatie](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="5674b-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="5674b-113">Een Azure-netwerk instellen</span><span class="sxs-lookup"><span data-stu-id="5674b-113">Set up an Azure network</span></span>

- <span data-ttu-id="5674b-114">Een Azure-netwerk instellen.</span><span class="sxs-lookup"><span data-stu-id="5674b-114">Set up an Azure network.</span></span> <span data-ttu-id="5674b-115">Virtuele machines in Azure worden geplaatst in dit netwerk wanneer ze zijn gemaakt na een failover.</span><span class="sxs-lookup"><span data-stu-id="5674b-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="5674b-116">Site Recovery in de Azure portal kunt instellen netwerken [Resource Manager](../resource-manager-deployment-model.md), of in de klassieke modus.</span><span class="sxs-lookup"><span data-stu-id="5674b-116">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="5674b-117">Het netwerk moet zich in dezelfde regio bevinden als de Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="5674b-117">The network should be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="5674b-118">Meer informatie over [virtueel netwerk prijzen](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="5674b-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="5674b-119">Meer informatie over [Azure VM-connectiviteit](physical-walkthrough-network.md) na een failover.</span><span class="sxs-lookup"><span data-stu-id="5674b-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="5674b-120">Een Azure-opslagaccount instellen</span><span class="sxs-lookup"><span data-stu-id="5674b-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="5674b-121">Lokale servers repliceert siteherstel naar Azure storage.</span><span class="sxs-lookup"><span data-stu-id="5674b-121">Site Recovery replicates on-premises servers to Azure storage.</span></span> <span data-ttu-id="5674b-122">Virtuele machines in Azure worden gemaakt van de opslag nadat de failover plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="5674b-122">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="5674b-123">Instellen van een [Azure storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account) voor gerepliceerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="5674b-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="5674b-124">Site Recovery in de Azure portal kunt instellen in Resource Manager, of in de klassieke modus storage-accounts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5674b-124">Site Recovery in the Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="5674b-125">Het opslagaccount kan worden standaard of [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5674b-125">The storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="5674b-126">Als u een premium-account hebt ingesteld, moet u ook een extra standaardaccount voor logboekgegevens.</span><span class="sxs-lookup"><span data-stu-id="5674b-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5674b-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5674b-127">Next steps</span></span>

<span data-ttu-id="5674b-128">Ga naar [stap 6: een kluis instellen](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="5674b-128">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>
