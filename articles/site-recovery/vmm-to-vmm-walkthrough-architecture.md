---
title: Hallo-architectuur voor Hyper-V-replicatie tooa secundaire site met Azure Site Recovery aaaReview | Microsoft Docs
description: Dit artikel bevat een overzicht van Hallo-architectuur voor het repliceren van lokale Hyper-V-machines tooa secundaire System Center VMM-site met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="7e1f8-103">Stap 1: Bekijk Hallo-architectuur voor Hyper-V-replicatie tooa secundaire site</span><span class="sxs-lookup"><span data-stu-id="7e1f8-103">Step 1: Review hello architecture for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="7e1f8-104">Dit artikel wordt beschreven Hallo-onderdelen en processen die betrokken zijn bij het repliceren van on-premises Hyper-V virtuele machines (VM's) in System Center Virtual Machine Manager (VMM) clouds, tooa secundaire VMM-site met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md)service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-104">This article describes hello components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM site using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="7e1f8-105">Eventuele opmerkingen posten onderin Hallo van dit artikel of in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7e1f8-105">Post any comments at hello bottom of this article, or in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="7e1f8-106">Architectuuronderdelen</span><span class="sxs-lookup"><span data-stu-id="7e1f8-106">Architectural components</span></span>

<span data-ttu-id="7e1f8-107">Dit is wat u nodig hebt voor het repliceren van Hyper-V-machines tooa secundaire VMM-site.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-107">Here's what you need for replicating Hyper-V VMs tooa secondary VMM site.</span></span>

<span data-ttu-id="7e1f8-108">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="7e1f8-108">**Component**</span></span> | <span data-ttu-id="7e1f8-109">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="7e1f8-109">**Location**</span></span> | <span data-ttu-id="7e1f8-110">**Details**</span><span class="sxs-lookup"><span data-stu-id="7e1f8-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="7e1f8-111">**Azure**</span><span class="sxs-lookup"><span data-stu-id="7e1f8-111">**Azure**</span></span> | <span data-ttu-id="7e1f8-112">Abonnement in Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-112">Subscription in Azure.</span></span> | <span data-ttu-id="7e1f8-113">Een Recovery Services-kluis in hello Azure-abonnement, tooorchestrate maken en beheren van replicatie tussen de VMM-locaties.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-113">You create a Recovery Services vault in hello Azure subscription, tooorchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="7e1f8-114">**VMM-server**</span><span class="sxs-lookup"><span data-stu-id="7e1f8-114">**VMM server**</span></span> | <span data-ttu-id="7e1f8-115">U hebt een primaire en secundaire VMM-locatie nodig.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="7e1f8-116">Het is raadzaam een VMM-server op Hallo primaire site, en één in Hallo secundaire site</span><span class="sxs-lookup"><span data-stu-id="7e1f8-116">We recommend a VMM server in hello primary site, and one in hello secondary site</span></span> 
<span data-ttu-id="7e1f8-117">**Hyper-V-server**</span><span class="sxs-lookup"><span data-stu-id="7e1f8-117">**Hyper-V server**</span></span> |  <span data-ttu-id="7e1f8-118">Een of meer Hyper-V-hostservers in Hallo primaire en secundaire VMM-clouds.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-118">One or more Hyper-V host servers in hello primary and secondary VMM clouds.</span></span> | <span data-ttu-id="7e1f8-119">Gegevens worden gerepliceerd tussen Hallo primaire en secundaire Hyper-V-hostservers via Hallo LAN of VPN-, Kerberos of certificaatverificatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-119">Data is replicated between hello primary and secondary Hyper-V host servers over hello LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="7e1f8-120">**Virtuele Hyper-V-machines**</span><span class="sxs-lookup"><span data-stu-id="7e1f8-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="7e1f8-121">Op Hyper-V-hostserver.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-121">On Hyper-V host server.</span></span> | <span data-ttu-id="7e1f8-122">Hallo-bronserver host moet ten minste één virtuele machine die u wilt dat tooreplicate hebben.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-122">hello source host server should have at least one VM that you want tooreplicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="7e1f8-123">Replicatieproces</span><span class="sxs-lookup"><span data-stu-id="7e1f8-123">Replication process</span></span>

1. <span data-ttu-id="7e1f8-124">Hello Azure-account instellen, een Recovery Services-kluis maken en geef op wat u wilt tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-124">You set up hello Azure account, create a Recovery Services vault, and specify what you want tooreplicate.</span></span>
2. <span data-ttu-id="7e1f8-125">U Hallo bron- en replicatie-instellingen configureren, waaronder het hello Azure Site Recovery Provider installeren op de VMM-servers en Hallo Microsoft Azure Recovery Services agent op elke Hyper-V-host.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-125">You configure hello source and target replication settings, which includes installing hello Azure Site Recovery Provider on VMM servers, and hello Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="7e1f8-126">Maakt u een replicatiebeleid voor de gegevensbron Hallo VMM-cloud.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-126">You create a replication policy for hello source VMM cloud.</span></span> <span data-ttu-id="7e1f8-127">Hallo beleid is toegepast tooall virtuele machines op hosts in Hallo cloud bevindt.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-127">hello policy is applied tooall VMs located on hosts in hello cloud.</span></span>
4. <span data-ttu-id="7e1f8-128">U replicatie voor elke VMM inschakelen en initiële replicatie van een virtuele machine plaats in overeenstemming met Hallo instellingen die u kiest.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with hello settings you choose.</span></span>
5. <span data-ttu-id="7e1f8-129">Na de initiële replicatie begint de replicatie van deltawijzigingen.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="7e1f8-130">Bijgehouden wijzigingen voor een item worden opgeslagen in een .hrl-bestand.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-130">Tracked changes for an item are held in a .hrl file.</span></span>


![Lokale tooon-premises](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="7e1f8-132">Failover- en failbackproces</span><span class="sxs-lookup"><span data-stu-id="7e1f8-132">Failover and failback process</span></span>

1. <span data-ttu-id="7e1f8-133">U kunt een geplande of niet-geplande [failover](site-recovery-failover.md) uitvoeren tussen on-premises sites.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="7e1f8-134">Als u een geplande failover uitvoert, wordt de Bronmachines tooensure worden afgesloten zonder verlies van gegevens.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-134">If you run a planned failover, then source VMs are shut down tooensure no data loss.</span></span>
2. <span data-ttu-id="7e1f8-135">U kunt één machine failover of maken [herstelplannen](site-recovery-create-recovery-plans.md) tooorchestrate failover van meerdere machines.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) tooorchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="7e1f8-136">Als u een niet-geplande failover tooa secundaire site na Hallo failover-machines op de secundaire locatie Hallo uitvoert zijn niet ingeschakeld voor beveiliging of replicatie.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-136">If you perform an unplanned failover tooa secondary site, after hello failover machines in hello secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="7e1f8-137">Als u een geplande failover uitgevoerd na een failover hello, worden machines op de secundaire locatie Hallo beveiligd.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-137">If you ran a planned failover, after hello failover, machines in hello secondary location are protected.</span></span>
5. <span data-ttu-id="7e1f8-138">Voer vervolgens Hallo failover toostart toegang tot Hallo werkbelasting van Hallo replica-VM.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-138">Then, you commit hello failover toostart accessing hello workload from hello replica VM.</span></span>
6. <span data-ttu-id="7e1f8-139">Als uw primaire site weer beschikbaar is, start u omgekeerde replicatie tooreplicate van Hallo secundaire site toohello primaire.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-139">When your primary site is available again, you initiate reverse replication tooreplicate from hello secondary site toohello primary.</span></span> <span data-ttu-id="7e1f8-140">Omgekeerde replicatie worden Hallo virtuele machines naar een beveiligde status, maar er is nog steeds Hallo secundair datacenter Hallo active-locatie.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-140">Reverse replication brings hello virtual machines into a protected state, but hello secondary datacenter is still hello active location.</span></span>
7. <span data-ttu-id="7e1f8-141">toomake hello primaire site naar de actieve locatie Hallo opnieuw u start een geplande failover van de secundaire tooprimary, gevolgd door een andere omgekeerde replicatie.</span><span class="sxs-lookup"><span data-stu-id="7e1f8-141">toomake hello primary site into hello active location again, you initiate a planned failover from secondary tooprimary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="7e1f8-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7e1f8-142">Next steps</span></span>

<span data-ttu-id="7e1f8-143">Ga te[stap 2: Controleer Hallo vereisten en beperkingen](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="7e1f8-143">Go too[Step 2: Review hello prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
