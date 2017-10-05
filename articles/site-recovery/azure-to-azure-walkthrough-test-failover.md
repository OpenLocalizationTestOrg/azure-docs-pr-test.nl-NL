---
title: Een testfailover voor virtuele machine van Azure replicatie uitvoeren met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van de stappen die u nodig hebt voor een testfailover voor het virtuele Azure-machines repliceren naar een andere Azure-regio met de Azure Site Recovery-service wordt uitgevoerd.
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
ms.openlocfilehash: 8babb0d016729f318442af93596d206c38d91206
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a><span data-ttu-id="aeb80-103">Stap 6: Een testfailover voor replicatie van de virtuele machine in Azure uitvoeren</span><span class="sxs-lookup"><span data-stu-id="aeb80-103">Step 6: Run a test failover for Azure VM replication</span></span>

<span data-ttu-id="aeb80-104">Wanneer u replicatie voor virtuele Azure-machine (VM's) hebt ingeschakeld, volgt u de stappen in dit artikel voor testfailover uitvoeren vanaf een Azure-regio naar de andere met het [Azure Site Recovery](site-recovery-overview.md) service in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="aeb80-104">After you've enabled replication for Azure virtual machine (VMs), follow the steps in this article, to run test failover from one Azure region to another, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

- <span data-ttu-id="aeb80-105">Wanneer u klaar bent met het artikel, moet met een testfailover hebt gecontroleerd dat ten minste één virtuele machine in Azure een failover naar uw secundaire Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="aeb80-105">When you finish the article, you should have verified with a test failover, that at least one Azure VM can fail over to your secondary Azure region.</span></span> 
- <span data-ttu-id="aeb80-106">Eventuele opmerkingen onder aan dit artikel plaatsen of vragen in de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="aeb80-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="aeb80-107">Replicatie van Azure VM is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="aeb80-107">Azure VM replication is currently in preview.</span></span>


## <a name="before-you-start"></a><span data-ttu-id="aeb80-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="aeb80-108">Before you start</span></span>

- <span data-ttu-id="aeb80-109">Voordat u een failovertest uitvoert, wordt aangeraden dat u controleren of de VM-eigenschappen en breng eventuele wijzigingen die u wilt.</span><span class="sxs-lookup"><span data-stu-id="aeb80-109">Before you run a test failover, we recommend that you verify the VM properties, and make any changes you need to.</span></span> <span data-ttu-id="aeb80-110">u kunt toegang tot de VM-eigenschappen in **gerepliceerde items**.</span><span class="sxs-lookup"><span data-stu-id="aeb80-110">You can access the VM properties in **Replicated items**.</span></span> <span data-ttu-id="aeb80-111">De **Essentials** blade ziet u informatie over machines instellingen en status.</span><span class="sxs-lookup"><span data-stu-id="aeb80-111">The **Essentials** blade shows information about machines settings and status.</span></span>
- <span data-ttu-id="aeb80-112">We raden u een afzonderlijk Azure VM-netwerk gebruiken voor de testfailover en niet op het netwerk (standaard of aangepast) die is geconfigureerd voor failover voor productie.</span><span class="sxs-lookup"><span data-stu-id="aeb80-112">We recommend you use a separate Azure VM network for the test failover, and not the network (default or customized) that was set up for production failover.</span></span>
- <span data-ttu-id="aeb80-113">De testfailover is mislukt via Azure Virtual machines (en hun opslag) naar de secundaire Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="aeb80-113">The test failover fails over Azure VMs (and their storage) to the secondary Azure region.</span></span> <span data-ttu-id="aeb80-114">Het niet alle afhankelijke apps of resources worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="aeb80-114">It doesn't replicate any dependent apps or resources.</span></span> <span data-ttu-id="aeb80-115">Als apps worden uitgevoerd op mislukte gedurende VM's afhankelijk van andere resources, zoals Active Directory en DNS zijn, moet u deze ook gerepliceerd als ze nog niet beschikbaar in uw secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="aeb80-115">If apps running on failed over VMs are dependent on other resources, such as Active Directory or DNS, you need to replicate these too, if they're not already available in your secondary region.</span></span> [<span data-ttu-id="aeb80-116">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="aeb80-116">Learn more</span></span>](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- <span data-ttu-id="aeb80-117">Als u toegang wilt tot gerepliceerde virtuele machines na failover van een on-premises site, moet u [voorbereiden op het verbinden](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) voor deze virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="aeb80-117">If you want to access replicated VMs after failover from an on-premises site, you need to [prepare to connect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) to these VMs.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="aeb80-118">Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="aeb80-118">Run a test failover</span></span>

1. <span data-ttu-id="aeb80-119">In **instellingen** > **gerepliceerde Items**, klikt u op de virtuele machine **+ Testfailover** pictogram.</span><span class="sxs-lookup"><span data-stu-id="aeb80-119">In **Settings** > **Replicated Items**, click the VM **+Test Failover** icon.</span></span> 

2. <span data-ttu-id="aeb80-120">In **Testfailover**, selecteer een herstelpunt voor de failover gebruiken:</span><span class="sxs-lookup"><span data-stu-id="aeb80-120">In **Test Failover**, Select a recovery point to use for the failover:</span></span>

    - <span data-ttu-id="aeb80-121">**Meest recente verwerkte**: de virtuele machine wordt overgenomen door de meest recente herstelpunt dat is verwerkt door de Site Recovery-service.</span><span class="sxs-lookup"><span data-stu-id="aeb80-121">**Latest processed**: Fails the VM over to the latest recovery point that was processed by the Site Recovery service.</span></span> <span data-ttu-id="aeb80-122">Het tijdstempel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="aeb80-122">The time stamp is shown.</span></span> <span data-ttu-id="aeb80-123">Met deze optie geen tijd besteed aan het verwerken van gegevens, zodat het biedt een laag RTO (beoogde hersteltijd).</span><span class="sxs-lookup"><span data-stu-id="aeb80-123">With this option, no time is spent processing data, so it provides a low RTO (Recovery Time Objective).</span></span>
    - <span data-ttu-id="aeb80-124">**Meest recente app-consistente**: deze optie alle VM's naar de meest recente herstelpunt van app-consistente failover.</span><span class="sxs-lookup"><span data-stu-id="aeb80-124">**Latest app-consistent**: This option fails over all VMs to the latest app-consistent recovery point.</span></span> <span data-ttu-id="aeb80-125">Het tijdstempel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="aeb80-125">The time stamp is shown.</span></span> 
    - <span data-ttu-id="aeb80-126">**Aangepaste**: eender welk herstelpunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="aeb80-126">**Custom**: Select any recovery point.</span></span>
 
3. <span data-ttu-id="aeb80-127">Selecteer de doel-Azure virtueel netwerk voor welke Azure VM's in de secundaire regio moet worden verbonden nadat de failover plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="aeb80-127">Select the target Azure virtual network to which Azure VMs in the secondary region will be connected, after the failover occurs.</span></span>
4. <span data-ttu-id="aeb80-128">Voor het starten van de failover, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="aeb80-128">To start the failover, click **OK**.</span></span> <span data-ttu-id="aeb80-129">Om de voortgang volgen, klikt u op de virtuele machine om de eigenschappen te openen.</span><span class="sxs-lookup"><span data-stu-id="aeb80-129">To track progress, click the VM to open its properties.</span></span> <span data-ttu-id="aeb80-130">U kunt ook op de **Testfailover** taak in de kluisnaam > **instellingen** > **taken** > **Site Recovery-taken**.</span><span class="sxs-lookup"><span data-stu-id="aeb80-130">Or, you can click the **Test Failover** job in the vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="aeb80-131">Nadat de failover is voltooid, de replica virtuele machine in Azure wordt weergegeven in de Azure portal > **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="aeb80-131">After the failover finishes, the replica Azure VM appears in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="aeb80-132">Zorg ervoor dat de virtuele machine is de juiste grootte heeft, of deze is verbonden met het juiste netwerk en dat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aeb80-132">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="aeb80-133">Als u wilt verwijderen van de virtuele machines die zijn gemaakt tijdens de testfailover, klikt u op **opschonen testfailover** voor het gerepliceerde artikel of het herstelplan.</span><span class="sxs-lookup"><span data-stu-id="aeb80-133">To delete the VMs that were created during the test failover, click **Cleanup test failover** on the replicated item or the recovery plan.</span></span> <span data-ttu-id="aeb80-134">In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover.</span><span class="sxs-lookup"><span data-stu-id="aeb80-134">In **Notes**, record and save any observations associated with the test failover.</span></span> 

<span data-ttu-id="aeb80-135">[Meer informatie](site-recovery-test-failover-to-azure.md) over testfailovers.</span><span class="sxs-lookup"><span data-stu-id="aeb80-135">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aeb80-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aeb80-136">Next steps</span></span>

<span data-ttu-id="aeb80-137">Nadat u de failover hebt getest, wordt in dit scenario is voltooid.</span><span class="sxs-lookup"><span data-stu-id="aeb80-137">After you've tested failover, this walkthrough is complete.</span></span> <span data-ttu-id="aeb80-138">Nu kunt u informatie over het uitvoeren van failovers in productie:</span><span class="sxs-lookup"><span data-stu-id="aeb80-138">Now, learn about running failovers in production:</span></span>

- <span data-ttu-id="aeb80-139">[Meer informatie](site-recovery-failover.md) over verschillende soorten failovers en hoe ze uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="aeb80-139">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="aeb80-140">Meer informatie over mislukte over meerdere virtuele machines [met behulp van een herstelplan](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="aeb80-140">Learn more about failing over multiple VMs [using a recovery plan](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="aeb80-141">Meer informatie over [herstelplannen met](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="aeb80-141">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="aeb80-142">Meer informatie over [andere virtuele Azure-machines](site-recovery-how-to-reprotect.md) na een failover.</span><span class="sxs-lookup"><span data-stu-id="aeb80-142">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>

