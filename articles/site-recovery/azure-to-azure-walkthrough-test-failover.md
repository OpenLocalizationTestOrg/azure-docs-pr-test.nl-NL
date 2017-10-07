---
title: een testfailover voor replicatie van de virtuele machine van Azure met Azure Site Recovery aaaRun | Microsoft Docs
description: Geeft een overzicht van Hallo stappen die u nodig hebt voor het uitvoeren van een testfailover voor virtuele Azure-machines repliceren tooanother Azure-regio met behulp van hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a><span data-ttu-id="2e5e9-103">Stap 6: Een testfailover voor replicatie van de virtuele machine in Azure uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2e5e9-103">Step 6: Run a test failover for Azure VM replication</span></span>

<span data-ttu-id="2e5e9-104">Nadat u replicatie voor virtuele Azure-machine (VM's) hebt ingeschakeld, voert u de stappen in dit artikel, toorun testfailover van een Azure-regio tooanother, met behulp van Hallo Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-104">After you've enabled replication for Azure virtual machine (VMs), follow hello steps in this article, toorun test failover from one Azure region tooanother, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="2e5e9-105">Wanneer u klaar bent met Hallo artikel, moet met een testfailover hebt gecontroleerd dat ten minste één virtuele machine van Azure kunt Failover-overschakeling tooyour secundaire Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-105">When you finish hello article, you should have verified with a test failover, that at least one Azure VM can fail over tooyour secondary Azure region.</span></span> 
- <span data-ttu-id="2e5e9-106">Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="2e5e9-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="2e5e9-107">Replicatie van Azure VM is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-107">Azure VM replication is currently in preview.</span></span>


## <a name="before-you-start"></a><span data-ttu-id="2e5e9-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="2e5e9-108">Before you start</span></span>

- <span data-ttu-id="2e5e9-109">Voordat u een failovertest uitvoert, wordt aangeraden Hallo VM-eigenschappen controleren en eventuele wijzigingen die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-109">Before you run a test failover, we recommend that you verify hello VM properties, and make any changes you need to.</span></span> <span data-ttu-id="2e5e9-110">U toegang hebt tot Hallo VM-eigenschappen in **gerepliceerde items**.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-110">You can access hello VM properties in **Replicated items**.</span></span> <span data-ttu-id="2e5e9-111">Hallo **Essentials** blade ziet u informatie over machines instellingen en status.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-111">hello **Essentials** blade shows information about machines settings and status.</span></span>
- <span data-ttu-id="2e5e9-112">Het is raadzaam u een afzonderlijk Azure VM-netwerk gebruiken voor testfailover hello en niet Hallo-netwerk (standaard of aangepast) die is geconfigureerd voor failover voor productie.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-112">We recommend you use a separate Azure VM network for hello test failover, and not hello network (default or customized) that was set up for production failover.</span></span>
- <span data-ttu-id="2e5e9-113">Hallo test failover mislukt via Azure Virtual machines (en hun opslag) toohello secundaire Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-113">hello test failover fails over Azure VMs (and their storage) toohello secondary Azure region.</span></span> <span data-ttu-id="2e5e9-114">Het niet alle afhankelijke apps of resources worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-114">It doesn't replicate any dependent apps or resources.</span></span> <span data-ttu-id="2e5e9-115">Als apps worden uitgevoerd op mislukte gedurende VM's afhankelijk van andere resources, zoals Active Directory en DNS zijn, moet u tooreplicate deze ook als ze nog niet beschikbaar in uw secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-115">If apps running on failed over VMs are dependent on other resources, such as Active Directory or DNS, you need tooreplicate these too, if they're not already available in your secondary region.</span></span> [<span data-ttu-id="2e5e9-116">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="2e5e9-116">Learn more</span></span>](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- <span data-ttu-id="2e5e9-117">Als u wilt dat tooaccess virtuele machines na failover van een on-premises site gerepliceerd, moet u deze te[voorbereiden tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-117">If you want tooaccess replicated VMs after failover from an on-premises site, you need too[prepare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese VMs.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="2e5e9-118">Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2e5e9-118">Run a test failover</span></span>

1. <span data-ttu-id="2e5e9-119">In **instellingen** > **gerepliceerde Items**, klikt u op Hallo VM **+ Testfailover** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-119">In **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span> 

2. <span data-ttu-id="2e5e9-120">In **Testfailover**, selecteert u een herstel punt toouse voor Hallo failover:</span><span class="sxs-lookup"><span data-stu-id="2e5e9-120">In **Test Failover**, Select a recovery point toouse for hello failover:</span></span>

    - <span data-ttu-id="2e5e9-121">**Meest recente verwerkte**: mislukt Hallo VM via toohello meest recente herstelpunt dat is verwerkt door Hallo Site Recovery-service.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-121">**Latest processed**: Fails hello VM over toohello latest recovery point that was processed by hello Site Recovery service.</span></span> <span data-ttu-id="2e5e9-122">Hallo tijdstempel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-122">hello time stamp is shown.</span></span> <span data-ttu-id="2e5e9-123">Met deze optie geen tijd besteed aan het verwerken van gegevens, zodat het biedt een laag RTO (beoogde hersteltijd).</span><span class="sxs-lookup"><span data-stu-id="2e5e9-123">With this option, no time is spent processing data, so it provides a low RTO (Recovery Time Objective).</span></span>
    - <span data-ttu-id="2e5e9-124">**Meest recente app-consistente**: deze optie is overgenomen van alle virtuele machines toohello laatste app-consistente herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-124">**Latest app-consistent**: This option fails over all VMs toohello latest app-consistent recovery point.</span></span> <span data-ttu-id="2e5e9-125">Hallo tijdstempel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-125">hello time stamp is shown.</span></span> 
    - <span data-ttu-id="2e5e9-126">**Aangepaste**: eender welk herstelpunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-126">**Custom**: Select any recovery point.</span></span>
 
3. <span data-ttu-id="2e5e9-127">Selecteer Hallo doel virtuele Azure-netwerk toowhich virtuele Azure-machines in de secundaire regio Hallo moet worden verbonden, nadat Hallo failover plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-127">Select hello target Azure virtual network toowhich Azure VMs in hello secondary region will be connected, after hello failover occurs.</span></span>
4. <span data-ttu-id="2e5e9-128">toostart Hallo failover, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-128">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="2e5e9-129">tootrack voortgang, klikt u op Hallo VM tooopen eigenschappen ervan.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-129">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="2e5e9-130">U kunt ook op Hallo **Testfailover** taak in de kluisnaam Hallo > **instellingen** > **taken** > **Site Recovery-taken**.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-130">Or, you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="2e5e9-131">Na het Hallo failover is voltooid, Hallo replica virtuele machine van Azure in hello Azure-portal weergegeven > **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-131">After hello failover finishes, hello replica Azure VM appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="2e5e9-132">Zorg ervoor dat Hallo VM is de juiste grootte hello, of deze is verbonden met het juiste netwerk toohello en dat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-132">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="2e5e9-133">toodelete hello virtuele machines die zijn gemaakt tijdens de testfailover hello, klikt u op **testfailover opschonen** op Hallo gerepliceerd item of Hallo herstelplan.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-133">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="2e5e9-134">In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-134">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="2e5e9-135">[Meer informatie](site-recovery-test-failover-to-azure.md) over testfailovers.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-135">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e5e9-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e5e9-136">Next steps</span></span>

<span data-ttu-id="2e5e9-137">Nadat u de failover hebt getest, wordt in dit scenario is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-137">After you've tested failover, this walkthrough is complete.</span></span> <span data-ttu-id="2e5e9-138">Nu kunt u informatie over het uitvoeren van failovers in productie:</span><span class="sxs-lookup"><span data-stu-id="2e5e9-138">Now, learn about running failovers in production:</span></span>

- <span data-ttu-id="2e5e9-139">[Meer informatie](site-recovery-failover.md) over verschillende soorten failovers, en hoe toorun ze.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-139">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="2e5e9-140">Meer informatie over mislukte over meerdere virtuele machines [met behulp van een herstelplan](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="2e5e9-140">Learn more about failing over multiple VMs [using a recovery plan](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="2e5e9-141">Meer informatie over [herstelplannen met](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="2e5e9-141">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="2e5e9-142">Meer informatie over [andere virtuele Azure-machines](site-recovery-how-to-reprotect.md) na een failover.</span><span class="sxs-lookup"><span data-stu-id="2e5e9-142">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>

