---
title: Netwerken voor virtuele machine van Hyper-V-replicatie worden toegewezen aan een secundaire site met Azure Site Recovery | Microsoft Docs
description: Beschrijft hoe netwerken toewijzen als Hyper-V-machines repliceren naar een secundaire VMM-site met Azure Site Recovery.
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
ms.openlocfilehash: 606e2d3d0e31b9d80200105e812f9d7bbbcf939c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-to-a-secondary-site"></a><span data-ttu-id="f3ebd-103">Stap 7: Netwerken voor virtuele machine van Hyper-V-replicatie worden toegewezen aan een secundaire site</span><span class="sxs-lookup"><span data-stu-id="f3ebd-103">Step 7: Map networks for Hyper-V VM replication to a secondary site</span></span>


<span data-ttu-id="f3ebd-104">Na het instellen van [bron en doel instellingen](vmm-to-vmm-walkthrough-source-target.md) gebruiken voor het repliceren van Hyper-V virtuele machines (VM's) naar een secundaire site van System Center Virtual Machine Manager (VMM), in dit artikel netwerktoewijzing voor Hyper-V virtuele machine (configureren Replicatie van de virtuele machine) naar een secundaire site, met behulp van [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f3ebd-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) to a secondary System Center Virtual Machine Manager (VMM) site, use this article to configure network mapping for Hyper-V virtual machine (VM) replication to a secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="f3ebd-105">Na het lezen van dit artikel kunt u onder aan dit artikel of op het [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) opmerkingen of vragen plaatsen.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="f3ebd-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f3ebd-106">Before you start</span></span>

- <span data-ttu-id="f3ebd-107">Meer informatie over [netwerktoewijzing](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="f3ebd-108">Controleren of de virtuele machines op de VMM-servers zijn verbonden met een VM-netwerk.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-108">Verify that virtual machines on VMM servers are connected to a VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="f3ebd-109">Netwerktoewijzing configureren</span><span class="sxs-lookup"><span data-stu-id="f3ebd-109">Configure network mapping</span></span>

1. <span data-ttu-id="f3ebd-110">In **netwerktoewijzing** > **Netwerktoewijzingen**, klikt u op **+ netwerktoewijzing**.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="f3ebd-111">In **netwerktoewijzing toevoegen** tabblad, selecteert u de bron en doel van de VMM-servers.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-111">In **Add network mapping** tab, select the source and target VMM servers.</span></span> <span data-ttu-id="f3ebd-112">De VM-netwerken die zijn gekoppeld aan de VMM-servers worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-112">The VM networks associated with the VMM servers are retrieved.</span></span>
3. <span data-ttu-id="f3ebd-113">In **Bronnetwerk**, selecteer het netwerk die u wilt gebruiken in de lijst met VM-netwerken die zijn gekoppeld aan de primaire VMM-server.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-113">In **Source network**, select the network you want to use from the list of VM networks associated with the primary VMM server.</span></span>
4. <span data-ttu-id="f3ebd-114">In **doelnetwerk**, selecteer het netwerk die u wilt gebruiken op de secundaire VMM-server.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-114">In **Target network**, select the network you want to use on the secondary VMM server.</span></span> <span data-ttu-id="f3ebd-115">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-115">Then click **OK**.</span></span>

    ![Netwerktoewijzing](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="f3ebd-117">Dit is wat er gebeurt wanneer er netwerktoewijzing wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="f3ebd-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="f3ebd-118">Alle bestaande gerepliceerde virtuele machines die met de bron-VM-netwerk overeenkomen wordt worden verbonden met het VM-netwerk van het doel.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-118">Any existing replica virtual machines that correspond to the source VM network will be connected to the target VM network.</span></span>
* <span data-ttu-id="f3ebd-119">Nieuwe virtuele machines die zijn verbonden met de bron-VM-netwerk, wordt na de replicatie worden verbonden met het doelnetwerk toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-119">New virtual machines that are connected to the source VM network will be connected to the target mapped network after replication.</span></span>
* <span data-ttu-id="f3ebd-120">Als u een bestaande toewijzing wijzigt met een nieuw netwerk, worden gerepliceerde virtuele machines verbonden met de nieuwe instellingen.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using the new settings.</span></span>
* <span data-ttu-id="f3ebd-121">Als het doelnetwerk meerdere subnetten bevat en een van deze subnetten dezelfde naam heeft als het subnet waarin de virtuele bronmachine zich bevindt, wordt de gerepliceerde virtuele machine na een failover verbonden met dat doelsubnet.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-121">If the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="f3ebd-122">Als er geen doelsubnet met een overeenkomende naam bestaat, wordt de virtuele machine verbonden met het eerste subnet in het netwerk.</span><span class="sxs-lookup"><span data-stu-id="f3ebd-122">If there’s no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="f3ebd-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f3ebd-123">Next steps</span></span>

<span data-ttu-id="f3ebd-124">Ga naar [stap 8: Configureer een beleid voor wachtwoordreplicatie](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="f3ebd-124">Go to [Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>