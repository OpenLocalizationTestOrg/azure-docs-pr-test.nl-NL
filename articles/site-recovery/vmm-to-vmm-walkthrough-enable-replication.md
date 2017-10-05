---
title: Schakel Hyper-V-replicatie naar een secundaire site met Azure Site Recovery | Microsoft Docs
description: Beschrijft hoe u replicatie inschakelen voor Hyper-V-machines repliceren naar een secundaire site van System Center VMM met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 6673d192dbc18bfc955d9e7e3c55893512511ffb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="step-9-enable-replication-to-a-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="c41a5-103">Stap 9: Schakel replicatie naar een secundaire site voor Hyper-V-machines</span><span class="sxs-lookup"><span data-stu-id="c41a5-103">Step 9: Enable replication to a secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="c41a5-104">Nadat het instellen van een beleid voor wachtwoordreplicatie gebruiken in dit artikel replicatie naar een secundaire site van System Center Virtual Machine Manager (VMM) voor on-premises Hyper-V virtuele machines (VM) in te schakelen, gebruik [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c41a5-104">After setting up a replication policy, use this article to enable replication to a secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="c41a5-105">Na het lezen van dit artikel kunt u onder aan dit artikel of op het [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) opmerkingen of vragen plaatsen.</span><span class="sxs-lookup"><span data-stu-id="c41a5-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-to-replicate"></a><span data-ttu-id="c41a5-106">Selecteer de virtuele machines repliceren</span><span class="sxs-lookup"><span data-stu-id="c41a5-106">Select VMs to replicate</span></span>

1. <span data-ttu-id="c41a5-107">Klik op **Stap 2: toepassing repliceren** > **Bron**.</span><span class="sxs-lookup"><span data-stu-id="c41a5-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![Replicatie inschakelen](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="c41a5-109">In **bron**, selecteert u de VMM-server en de cloud waarin u wilt repliceren Hyper-V-hosts zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="c41a5-109">In **Source**, select the VMM server, and the cloud in which the Hyper-V hosts you want to replicate are located.</span></span> <span data-ttu-id="c41a5-110">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c41a5-110">Then click **OK**.</span></span>

    ![Replicatie inschakelen](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="c41a5-112">In **doel**, controleert u de secundaire VMM-server en de cloud.</span><span class="sxs-lookup"><span data-stu-id="c41a5-112">In **Target**, verify the secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="c41a5-113">In **virtuele machines**, selecteert u de virtuele machines die u wilt beveiligen in de lijst.</span><span class="sxs-lookup"><span data-stu-id="c41a5-113">In **Virtual machines**, select the VMs you want to protect from the list.</span></span>

    ![Beveiliging van de virtuele machine inschakelen](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="c41a5-115">U kunt de voortgang van volgen de **beveiliging inschakelen** actie in **taken** > **Site Recovery-taken**.</span><span class="sxs-lookup"><span data-stu-id="c41a5-115">You can track progress of the **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="c41a5-116">Na de **beveiliging voltooien** taak is voltooid, de initiële replicatie is voltooid en de virtuele machine is gereed voor failover.</span><span class="sxs-lookup"><span data-stu-id="c41a5-116">After the **Finalize Protection** job completes, the initial replication is complete, and the virtual machine is ready for failover.</span></span>

<span data-ttu-id="c41a5-117">Opmerking:</span><span class="sxs-lookup"><span data-stu-id="c41a5-117">Note that:</span></span>

- <span data-ttu-id="c41a5-118">U kunt ook beveiliging voor virtuele machines in de VMM-console inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c41a5-118">You can also enable protection for virtual machines in the VMM console.</span></span> <span data-ttu-id="c41a5-119">Klik op **beveiliging inschakelen** op de werkbalk van de eigenschappen van de virtuele machine > **Azure Site Recovery** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c41a5-119">Click **Enable Protection** on the toolbar in the virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="c41a5-120">Nadat u replicatie hebt ingeschakeld, kunt u de eigenschappen weergeven voor de virtuele machine in **gerepliceerde Items**.</span><span class="sxs-lookup"><span data-stu-id="c41a5-120">After you've enabled replication, you can view properties for the VM in **Replicated Items**.</span></span> <span data-ttu-id="c41a5-121">Op de **Essentials** dashboard ziet u informatie over het replicatiebeleid voor de virtuele machine en de status ervan.</span><span class="sxs-lookup"><span data-stu-id="c41a5-121">On the **Essentials** dashboard, you can see information about the replication policy for the VM and its status.</span></span> <span data-ttu-id="c41a5-122">Klik op **eigenschappen** voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c41a5-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="c41a5-123">Ingebouwde bestaande virtuele machines</span><span class="sxs-lookup"><span data-stu-id="c41a5-123">Onboard existing VMs</span></span>

<span data-ttu-id="c41a5-124">Als u een bestaande virtuele machines in VMM die worden gerepliceerd met Hyper-V Replica hebt, kunt u vrijgeven ze voor Azure Site Recovery replicatie als volgt:</span><span class="sxs-lookup"><span data-stu-id="c41a5-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="c41a5-125">Zorg ervoor dat de Hyper-V-server die als host fungeert voor de bestaande virtuele machine zich bevinden in de primaire cloud en dat de Hyper-V-server die als host fungeert voor de replica virtuele machine bevindt zich in de secundaire cloud.</span><span class="sxs-lookup"><span data-stu-id="c41a5-125">Ensure that the Hyper-V server hosting the existing VM is located in the primary cloud, and that the Hyper-V server hosting the replica virtual machine is located in the secondary cloud.</span></span>
2. <span data-ttu-id="c41a5-126">Zorg ervoor dat een beleid voor wachtwoordreplicatie is geconfigureerd voor de primaire VMM-cloud.</span><span class="sxs-lookup"><span data-stu-id="c41a5-126">Make sure a replication policy is configured for the primary VMM cloud.</span></span>
3. <span data-ttu-id="c41a5-127">Replicatie inschakelen voor de primaire virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c41a5-127">Enable replication for the primary virtual machine.</span></span> <span data-ttu-id="c41a5-128">Azure Site Recovery en VMM Zorg ervoor dat de dezelfde replicatiehost en de virtuele machine wordt gedetecteerd en Azure Site Recovery wordt opnieuw gebruikt en herstellen van replicatie met de opgegeven instellingen.</span><span class="sxs-lookup"><span data-stu-id="c41a5-128">Azure Site Recovery and VMM ensure that the same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using the specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c41a5-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c41a5-129">Next steps</span></span>

<span data-ttu-id="c41a5-130">Ga naar [stap 10: een testfailover uitvoeren](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="c41a5-130">Go to [Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
