---
title: aaaMap netwerken voor virtuele machine van Hyper-V-replicatie tooa secundaire site met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe toomap netwerken bij het repliceren van Hyper-V-machines tooa secundaire VMM-site met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a><span data-ttu-id="f7d65-103">Stap 7: De netwerken voor virtuele machine van Hyper-V-replicatie tooa secundaire site toewijzen</span><span class="sxs-lookup"><span data-stu-id="f7d65-103">Step 7: Map networks for Hyper-V VM replication tooa secondary site</span></span>


<span data-ttu-id="f7d65-104">Na het instellen van [bron en doel instellingen](vmm-to-vmm-walkthrough-source-target.md) gebruiken voor het repliceren van Hyper-V virtuele machines (VM's) tooa secundaire System Center Virtual Machine Manager (VMM)-site, in dit artikel tooconfigure netwerktoewijzing voor virtuele Hyper-V machine (VM) replicatie tooa secundaire site, met behulp van [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7d65-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) tooa secondary System Center Virtual Machine Manager (VMM) site, use this article tooconfigure network mapping for Hyper-V virtual machine (VM) replication tooa secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="f7d65-105">Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f7d65-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="f7d65-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f7d65-106">Before you start</span></span>

- <span data-ttu-id="f7d65-107">Meer informatie over [netwerktoewijzing](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="f7d65-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="f7d65-108">Controleer of de virtuele machines op de VMM-servers zijn verbonden tooa VM-netwerk.</span><span class="sxs-lookup"><span data-stu-id="f7d65-108">Verify that virtual machines on VMM servers are connected tooa VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="f7d65-109">Netwerktoewijzing configureren</span><span class="sxs-lookup"><span data-stu-id="f7d65-109">Configure network mapping</span></span>

1. <span data-ttu-id="f7d65-110">In **netwerktoewijzing** > **Netwerktoewijzingen**, klikt u op **+ netwerktoewijzing**.</span><span class="sxs-lookup"><span data-stu-id="f7d65-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="f7d65-111">In **netwerktoewijzing toevoegen** tabblad, selecteert u Hallo bron en doel van de VMM-servers.</span><span class="sxs-lookup"><span data-stu-id="f7d65-111">In **Add network mapping** tab, select hello source and target VMM servers.</span></span> <span data-ttu-id="f7d65-112">Hallo VM-netwerken die zijn gekoppeld aan de VMM-servers Hallo worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="f7d65-112">hello VM networks associated with hello VMM servers are retrieved.</span></span>
3. <span data-ttu-id="f7d65-113">In **Bronnetwerk**, selecteer toouse uit Hallo lijst met VM-netwerken die zijn gekoppeld aan de primaire VMM-server Hallo gewenste Hallo-netwerk.</span><span class="sxs-lookup"><span data-stu-id="f7d65-113">In **Source network**, select hello network you want toouse from hello list of VM networks associated with hello primary VMM server.</span></span>
4. <span data-ttu-id="f7d65-114">In **doelnetwerk**, selecteer Hallo netwerk gewenste toouse op Hallo secundaire VMM-server.</span><span class="sxs-lookup"><span data-stu-id="f7d65-114">In **Target network**, select hello network you want toouse on hello secondary VMM server.</span></span> <span data-ttu-id="f7d65-115">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7d65-115">Then click **OK**.</span></span>

    ![Netwerktoewijzing](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="f7d65-117">Dit is wat er gebeurt wanneer er netwerktoewijzing wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="f7d65-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="f7d65-118">Alle bestaande gerepliceerde virtuele machines die overeenkomen met toohello bron-VM-netwerk is verbonden toohello doel VM-netwerk.</span><span class="sxs-lookup"><span data-stu-id="f7d65-118">Any existing replica virtual machines that correspond toohello source VM network will be connected toohello target VM network.</span></span>
* <span data-ttu-id="f7d65-119">Nieuwe virtuele machines die verbonden toohello bron-VM-netwerk zijn worden toegewezen doelnetwerk verbonden toohello na de replicatie.</span><span class="sxs-lookup"><span data-stu-id="f7d65-119">New virtual machines that are connected toohello source VM network will be connected toohello target mapped network after replication.</span></span>
* <span data-ttu-id="f7d65-120">Als u een bestaande toewijzing met een nieuw netwerk wijzigt, worden gerepliceerde virtuele machines verbonden met de nieuwe instellingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7d65-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using hello new settings.</span></span>
* <span data-ttu-id="f7d65-121">Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten Hallo heeft dezelfde naam als het subnet waarop Hallo bron virtual machine zich bevindt, wordt Hallo replica virtuele machine na een failover worden verbonden toothat Doelsubnet.</span><span class="sxs-lookup"><span data-stu-id="f7d65-121">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="f7d65-122">Als er geen Doelsubnet met een overeenkomende naam, wordt de Hallo virtuele machine verbonden toohello eerste subnet in het Hallo-netwerk zijn.</span><span class="sxs-lookup"><span data-stu-id="f7d65-122">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="f7d65-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f7d65-123">Next steps</span></span>

<span data-ttu-id="f7d65-124">Ga te[stap 8: Configureer een beleid voor wachtwoordreplicatie](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="f7d65-124">Go too[Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>
