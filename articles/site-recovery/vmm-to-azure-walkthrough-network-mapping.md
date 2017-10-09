---
title: de netwerktoewijzing aaaConfigure voor het repliceren van Hyper-V-machines in VMM-clouds tooAzure met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe netwerktoewijzing tooconfigure bij het repliceren van Hyper-V-machines in VMM tooAzure met Azure Site Recovery clouds
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="93b7a-103">Stap 9: Netwerktoewijzing voor Hyper-V-replicatie (met VMM) tooAzure configureren</span><span class="sxs-lookup"><span data-stu-id="93b7a-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="93b7a-104">Na het instellen van Hallo [bron- en replicatie-instellingen](vmm-to-azure-walkthrough-source-target.md), in dit artikel tooconfigure netwerk toewijzing toomap tussen on-premises VMM VM-netwerken en Azure-netwerken gebruiken.</span><span class="sxs-lookup"><span data-stu-id="93b7a-104">After you set up hello [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article tooconfigure network mapping toomap between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="93b7a-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="93b7a-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="93b7a-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="93b7a-106">Before you start</span></span>

- <span data-ttu-id="93b7a-107">Meer informatie over [netwerktoewijzing](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="93b7a-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="93b7a-108">[VMM voorbereiden op netwerktoewijzing](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="93b7a-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="93b7a-109">Verifieer dat de virtuele machines op Hallo VMM-server verbonden tooa VM-netwerk zijn en dat u ten minste één virtuele Azure-netwerk hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="93b7a-109">Verify that virtual machines on hello VMM server are connected tooa VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="93b7a-110">Meerdere VM-netwerken kunnen worden toegewezen tooa één Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="93b7a-110">Multiple VM networks can be mapped tooa single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="93b7a-111">Toewijzing configureren</span><span class="sxs-lookup"><span data-stu-id="93b7a-111">Configure mapping</span></span>

<span data-ttu-id="93b7a-112">Configureer het toewijzen als volgt:</span><span class="sxs-lookup"><span data-stu-id="93b7a-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="93b7a-113">In **Site Recovery-infrastructuur** > **Netwerktoewijzingen** > **netwerktoewijzing**, klikt u op Hallo **+ netwerktoewijzing**  pictogram.</span><span class="sxs-lookup"><span data-stu-id="93b7a-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click hello **+Network Mapping** icon.</span></span>

    ![Netwerktoewijzing](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="93b7a-115">In **netwerktoewijzing toevoegen**, selecteer Hallo bron-VMM-server, en **Azure** als Hallo doel.</span><span class="sxs-lookup"><span data-stu-id="93b7a-115">In **Add network mapping**, select hello source VMM server, and **Azure** as hello target.</span></span>
3. <span data-ttu-id="93b7a-116">Controleer of u Hallo-abonnement en Hallo implementatiemodel na een failover.</span><span class="sxs-lookup"><span data-stu-id="93b7a-116">Verify hello subscription and hello deployment model after failover.</span></span>
4. <span data-ttu-id="93b7a-117">In **Bronnetwerk**, selecteer Hallo bron on-premises VM-netwerk gewenste toomap uit die zijn gekoppeld aan de VMM-server Hallo Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="93b7a-117">In **Source network**, select hello source on-premises VM network you want toomap from hello list associated with hello VMM server.</span></span>
5. <span data-ttu-id="93b7a-118">In **doelnetwerk**, selecteer hello Azure-netwerk in welke replica virtuele Azure-machines geplaatst worden moeten nadat ze zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="93b7a-118">In **Target network**, select hello Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="93b7a-119">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="93b7a-119">Then click **OK**.</span></span>

    ![Netwerktoewijzing](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="93b7a-121">Dit is wat er gebeurt wanneer er netwerktoewijzing wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="93b7a-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="93b7a-122">Bestaande virtuele machines op Hallo bron VM-netwerk zijn verbonden toohello doelnetwerk bij toewijzing begint.</span><span class="sxs-lookup"><span data-stu-id="93b7a-122">Existing VMs on hello source VM network are connected toohello target network when mapping begins.</span></span> <span data-ttu-id="93b7a-123">Nieuwe virtuele machines verbonden toohello bron VM-netwerk zijn verbonden toohello toegewezen Azure-netwerk wanneer er replicatie plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="93b7a-123">New VMs connected toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="93b7a-124">Als u een bestaande netwerktoewijzing wijzigt, gerepliceerde virtuele machines verbinding maken met behulp van de nieuwe instellingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="93b7a-124">If you modify an existing network mapping, replica virtual machines connect using hello new settings.</span></span>
* <span data-ttu-id="93b7a-125">Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten Hallo heeft dezelfde naam als het subnet waarop Hallo bron virtuele machine zich bevindt en vervolgens Hallo replica virtuele machine verbindt toothat Doelsubnet na een failover.</span><span class="sxs-lookup"><span data-stu-id="93b7a-125">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
* <span data-ttu-id="93b7a-126">Als er geen Doelsubnet met een overeenkomende naam, verbindt Hallo virtuele machine toohello eerste subnet in het Hallo-netwerk.</span><span class="sxs-lookup"><span data-stu-id="93b7a-126">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="93b7a-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93b7a-127">Next steps</span></span>

<span data-ttu-id="93b7a-128">Ga te[stap 10: een replicatiebeleid maken](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="93b7a-128">Go too[Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
