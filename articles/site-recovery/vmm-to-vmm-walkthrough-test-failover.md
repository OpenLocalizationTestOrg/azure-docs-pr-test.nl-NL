---
title: een testfailover voor virtuele machine van Hyper-V-replicatie tooa secundaire site met Azure Site Recovery aaaRun | Microsoft Docs
description: Beschrijft hoe een testfailover voor virtuele machine van Hyper-V-replicatie tooa toorun secundaire System Center VMM site met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="8ad5a-103">Stap 10: Een testfailover voor Hyper-V-replicatie tooa secundaire site uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8ad5a-103">Step 10: Run a test failover for Hyper-V replication tooa secondary site</span></span>


<span data-ttu-id="8ad5a-104">Nadat u replicatie voor Hyper-V virtuele machines (VM's) met inschakelen [Azure Site Recovery](site-recovery-overview.md), gebruik dit artikel toorun een testfailover.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article toorun a test failover.</span></span> <span data-ttu-id="8ad5a-105">Een testfailover controleert of dat replicatie werkt, zonder enige impact op uw productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="8ad5a-106">Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8ad5a-106">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="8ad5a-107">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="8ad5a-107">Before you start</span></span>

- <span data-ttu-id="8ad5a-108">Wanneer u een testfailover activeren wilt, kunt u Hallo netwerk toowhich Hallo testreplica die VMS wordt verbinding gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-108">When you're triggering a test failover, you can specify hello network toowhich hello test replica VMs will connect.</span></span> <span data-ttu-id="8ad5a-109">[Meer informatie](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) over netwerkopties Hallo.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about hello network options.</span></span>
- <span data-ttu-id="8ad5a-110">Het is raadzaam dat u een netwerk dat u hebt geselecteerd tijdens de netwerktoewijzing niet kiezen.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="8ad5a-111">Hallo-instructies in dit artikel wordt beschreven hoe toofail via één VM.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-111">hello instructions in this article describe how toofail over a single VM.</span></span> <span data-ttu-id="8ad5a-112">Meer informatie over [herstelplannen maken](site-recovery-create-recovery-plans.md) als u wilt dat toofail over meerdere virtuele machines samen.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want toofail over multiple VMs together.</span></span>
- <span data-ttu-id="8ad5a-113">Meer informatie over [beperkingen voor testfailovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="8ad5a-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="8ad5a-114">Hallo IP-adres opgegeven tooa VM tijdens de testfailover is Hallo hetzelfde IP-adres dat Hallo VM ontvangt voor een geplande of niet-geplande failover (ervan uitgaande dat Hallo IP-adres beschikbaar in het testfailovernetwerk Hallo is).</span><span class="sxs-lookup"><span data-stu-id="8ad5a-114">hello IP address given tooa VM during test failover is hello same IP address that hello VM would receive for a planned or unplanned failover (presuming that hello IP address is available in hello test failover network).</span></span> <span data-ttu-id="8ad5a-115">Als Hallo IP-adres is niet beschikbaar in het testfailovernetwerk hello, ontvangt Hallo VM een ander IP-adres dat beschikbaar is in het testfailovernetwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-115">If hello IP address isn't available in hello test failover network, hello VM receives another IP address that is available in hello test failover network.</span></span>
- <span data-ttu-id="8ad5a-116">Als u een testfailover toodo in uw productienetwerk voor volledige validatation van end-to-end network connectivity machine wilt, houd er rekening mee dat:</span><span class="sxs-lookup"><span data-stu-id="8ad5a-116">If you do want toodo a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="8ad5a-117">Hallo die primaire virtuele machine moet worden afgesloten wanneer u Hallo testfailover uitvoert.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-117">hello primary VM should be shut down when you're doing hello test failover.</span></span> <span data-ttu-id="8ad5a-118">Anders twee virtuele machines met dezelfde identiteit zal worden uitgevoerd in de Hallo Hallo netwerk op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-118">Otherwise, two VMs with hello same identity will be running in hello same network at hello same time.</span></span> 
    - <span data-ttu-id="8ad5a-119">Als u wijzigingen tootest virtuele machines aanbrengt, gaan deze wijzigingen verloren wanneer u opschonen Hallo failover testen.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-119">If you make changes tootest VMs, those changes are lost when you clean up hello test failover.</span></span> <span data-ttu-id="8ad5a-120">Deze wijzigingen worden niet-gerepliceerde back toohello primaire virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-120">These changes aren't replicated back toohello primary VM.</span></span>
    - <span data-ttu-id="8ad5a-121">Testen van een een productienetwerk leidt toodowntime voor uw productie-workloads.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-121">Testing a a production network leads toodowntime for your production workloads.</span></span> <span data-ttu-id="8ad5a-122">Vraag gebruikers geen toouse Hallo app als Hallo disaster recovery inzoomen uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-122">Ask users not toouse hello app when hello disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="8ad5a-123">Een testfailover uitvoeren voor een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8ad5a-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="8ad5a-124">toofail via één VM in **gerepliceerde Items**, klikt u op Hallo VM > **Testfailover**.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-124">toofail over a single VM, in **Replicated Items**, click hello VM > **Test Failover**.</span></span>
2. <span data-ttu-id="8ad5a-125">In **Testfailover**, opgeven hoe test-virtuele machines verbonden toonetworks worden na Hallo testfailover.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-125">In **Test Failover**, specify how test VMs will be connected toonetworks after hello test failover.</span></span> 
3. <span data-ttu-id="8ad5a-126">Klik op **OK** toobegin Hallo failover.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-126">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="8ad5a-127">Voortgang volgen op Hallo **taken** tabblad.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-127">Track progress on hello **Jobs** tab.</span></span>
5. <span data-ttu-id="8ad5a-128">Nadat de failover is voltooid, controleert u Hallo test start van de virtuele machines is of.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-128">After failover is complete, verify that hello test VMs start successfully.</span></span>
6. <span data-ttu-id="8ad5a-129">Wanneer u bent klaar, klikt u op **testfailover opschonen** op Hallo herstelplan.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-129">When you're done, click **Cleanup test failover** on hello recovery plan.</span></span>
7. <span data-ttu-id="8ad5a-130">In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-130">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="8ad5a-131">Deze stap verwijdert Hallo virtuele machines en netwerken die zijn gemaakt tijdens de testfailover.</span><span class="sxs-lookup"><span data-stu-id="8ad5a-131">This step deletes hello virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8ad5a-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8ad5a-132">Next steps</span></span>

<span data-ttu-id="8ad5a-133">Nadat u Hallo-implementatie hebt getest, meer informatie over andere typen [failover](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="8ad5a-133">After you've tested hello deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
