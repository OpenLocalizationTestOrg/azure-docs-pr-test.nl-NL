---
title: aaaEnable Hyper-V-replicatie tooa secundaire site met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe tooenable replicatie voor de Hyper-V-machines repliceren tooa secundaire System Center VMM site met Azure Site Recovery.
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
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="ed80a-103">Stap 9: Replicatie tooa secundaire site inschakelen voor Hyper-V virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ed80a-103">Step 9: Enable replication tooa secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="ed80a-104">Na het instellen van een beleid voor wachtwoordreplicatie, kunt u deze site artikel tooenable replicatie tooa secundaire System Center Virtual Machine Manager (VMM) gebruiken voor on-premises Hyper-V virtuele machines (VM), met behulp van [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed80a-104">After setting up a replication policy, use this article tooenable replication tooa secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="ed80a-105">Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ed80a-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-tooreplicate"></a><span data-ttu-id="ed80a-106">Virtuele machines tooreplicate selecteren</span><span class="sxs-lookup"><span data-stu-id="ed80a-106">Select VMs tooreplicate</span></span>

1. <span data-ttu-id="ed80a-107">Klik op **Stap 2: toepassing repliceren** > **Bron**.</span><span class="sxs-lookup"><span data-stu-id="ed80a-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![Replicatie inschakelen](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="ed80a-109">In **bron**Hallo VMM-server en selecteer Hallo cloud in welke Hallo gewenste tooreplicate van Hyper-V-hosts zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="ed80a-109">In **Source**, select hello VMM server, and hello cloud in which hello Hyper-V hosts you want tooreplicate are located.</span></span> <span data-ttu-id="ed80a-110">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ed80a-110">Then click **OK**.</span></span>

    ![Replicatie inschakelen](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="ed80a-112">In **doel**, controleert u of Hallo secundaire VMM-server en de cloud.</span><span class="sxs-lookup"><span data-stu-id="ed80a-112">In **Target**, verify hello secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="ed80a-113">In **virtuele machines**, Hallo virtuele machines die u wilt dat tooprotect uit Hallo lijst selecteren.</span><span class="sxs-lookup"><span data-stu-id="ed80a-113">In **Virtual machines**, select hello VMs you want tooprotect from hello list.</span></span>

    ![Beveiliging van de virtuele machine inschakelen](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="ed80a-115">U kunt de voortgang van Hallo volgen **beveiliging inschakelen** actie in **taken** > **Site Recovery-taken**.</span><span class="sxs-lookup"><span data-stu-id="ed80a-115">You can track progress of hello **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="ed80a-116">Na het Hallo **beveiliging voltooien** taak is voltooid, Hallo initiële replicatie is voltooid en Hallo virtuele machine is gereed voor failover.</span><span class="sxs-lookup"><span data-stu-id="ed80a-116">After hello **Finalize Protection** job completes, hello initial replication is complete, and hello virtual machine is ready for failover.</span></span>

<span data-ttu-id="ed80a-117">Opmerking:</span><span class="sxs-lookup"><span data-stu-id="ed80a-117">Note that:</span></span>

- <span data-ttu-id="ed80a-118">U kunt ook beveiliging voor virtuele machines in Hallo VMM-console inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ed80a-118">You can also enable protection for virtual machines in hello VMM console.</span></span> <span data-ttu-id="ed80a-119">Klik op **beveiliging inschakelen** op Hallo werkbalk in de eigenschappen van de virtuele machine Hallo > **Azure Site Recovery** tabblad.</span><span class="sxs-lookup"><span data-stu-id="ed80a-119">Click **Enable Protection** on hello toolbar in hello virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="ed80a-120">Nadat u replicatie hebt ingeschakeld, kunt u de eigenschappen voor Hallo VM weergeven in **gerepliceerde Items**.</span><span class="sxs-lookup"><span data-stu-id="ed80a-120">After you've enabled replication, you can view properties for hello VM in **Replicated Items**.</span></span> <span data-ttu-id="ed80a-121">Op Hallo **Essentials** dashboard ziet u informatie over het replicatiebeleid Hallo voor Hallo VM en de status ervan.</span><span class="sxs-lookup"><span data-stu-id="ed80a-121">On hello **Essentials** dashboard, you can see information about hello replication policy for hello VM and its status.</span></span> <span data-ttu-id="ed80a-122">Klik op **eigenschappen** voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ed80a-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="ed80a-123">Ingebouwde bestaande virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ed80a-123">Onboard existing VMs</span></span>

<span data-ttu-id="ed80a-124">Als u een bestaande virtuele machines in VMM die worden gerepliceerd met Hyper-V Replica hebt, kunt u vrijgeven ze voor Azure Site Recovery replicatie als volgt:</span><span class="sxs-lookup"><span data-stu-id="ed80a-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="ed80a-125">Zorg dat Hallo Hyper-V-hostserver Hallo bestaande virtuele machine bevindt zich in de primaire cloud Hallo en die Hallo Hyper-V-server die als host fungeert voor Hallo replica virtuele machine bevindt zich in Hallo secundaire cloud.</span><span class="sxs-lookup"><span data-stu-id="ed80a-125">Ensure that hello Hyper-V server hosting hello existing VM is located in hello primary cloud, and that hello Hyper-V server hosting hello replica virtual machine is located in hello secondary cloud.</span></span>
2. <span data-ttu-id="ed80a-126">Zorg ervoor dat een beleid voor wachtwoordreplicatie is geconfigureerd voor Hallo primaire VMM-cloud.</span><span class="sxs-lookup"><span data-stu-id="ed80a-126">Make sure a replication policy is configured for hello primary VMM cloud.</span></span>
3. <span data-ttu-id="ed80a-127">Replicatie inschakelen voor Hallo primaire virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ed80a-127">Enable replication for hello primary virtual machine.</span></span> <span data-ttu-id="ed80a-128">Azure Site Recovery en VMM ervoor te zorgen dat hello dezelfde replicatiehost en virtuele machine wordt gedetecteerd, en Azure Site Recovery opnieuw wilt gebruiken en om opnieuw replicatie met Hallo instellingen opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ed80a-128">Azure Site Recovery and VMM ensure that hello same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using hello specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ed80a-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ed80a-129">Next steps</span></span>

<span data-ttu-id="ed80a-130">Ga te[stap 10: een testfailover uitvoeren](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="ed80a-130">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
