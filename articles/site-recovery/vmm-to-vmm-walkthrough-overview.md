---
title: aaaReplicate Hyper-V-machines tooa secundaire VMM-site met Azure Site Recovery | Microsoft Docs
description: Biedt een overzicht voor het repliceren van Hyper-V-machines tooa secundaire VMM-site met behulp van hello Azure-portal.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a><span data-ttu-id="f3179-103">Hyper-V virtuele machines in VMM-clouds tooa secundaire VMM-site repliceren</span><span class="sxs-lookup"><span data-stu-id="f3179-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3179-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f3179-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="f3179-105">Klassieke portal</span><span class="sxs-lookup"><span data-stu-id="f3179-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="f3179-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f3179-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="f3179-107">In dit artikel biedt een overzicht van Hallo stappen tooreplicate lokale Hyper-V virtuele machines (VM's vereist) in System Center Virtual Machine Manager (VMM)-clouds, tooa secundaire VMM locatie worden beheerd met behulp van [Azure Site Recovery](site-recovery-overview.md)in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f3179-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span>

<span data-ttu-id="f3179-108">Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f3179-108">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="f3179-109">Stap 1: Bekijk Hallo scenario-architectuur</span><span class="sxs-lookup"><span data-stu-id="f3179-109">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="f3179-110">Voordat de implementatie start, bekijk Hallo scenario-architectuur en zorg ervoor dat u weet dat alle Hallo onderdelen moet u toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f3179-110">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="f3179-111">Ga te[stap 1: Bekijk Hallo architectuur](vmm-to-vmm-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="f3179-111">Go too[Step 1: Review hello architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="f3179-112">Stap 2: Controleer de vereisten en beperkingen</span><span class="sxs-lookup"><span data-stu-id="f3179-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="f3179-113">Zorg ervoor dat u Hallo implementatievereisten en beperkingen begrijpt.</span><span class="sxs-lookup"><span data-stu-id="f3179-113">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="f3179-114">**Vereisten voor Azure**: U hebt een Microsoft Azure-abonnement en Azure Recovery Services-kluis, tooorchestrate en beheren van replicatie.</span><span class="sxs-lookup"><span data-stu-id="f3179-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, tooorchestrate and manage replication.</span></span>
<span data-ttu-id="f3179-115">**On-premises VMM-servers en Hyper-V-hosts**: Zorg ervoor dat VMM-servers en Hyper-V-hosts compatibele en voorbereid voor implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f3179-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="f3179-116">Ga te[stap 2: Controleer of de vereisten en beperkingen](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="f3179-116">Go too[Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="f3179-117">Stap 3: Plannen netwerken</span><span class="sxs-lookup"><span data-stu-id="f3179-117">Step 3: Plan networking</span></span>

<span data-ttu-id="f3179-118">U moet een netwerk tooensure kunt u de netwerkkoppeling tussen VMM VM-netwerken bij het implementeren van Hallo scenario configureren planning toodo.</span><span class="sxs-lookup"><span data-stu-id="f3179-118">You need toodo some network planning tooensure that you can configure network mapping between VMM VM networks when you deploy hello scenario.</span></span>

<span data-ttu-id="f3179-119">Ga te[stap 3: plannen netwerken](vmm-to-vmm-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="f3179-119">Go too[Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="f3179-120">Stap 4: Voorbereiden VMM en Hyper-V</span><span class="sxs-lookup"><span data-stu-id="f3179-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="f3179-121">Hallo VMM-servers en Hyper-V-hosts voorbereiden voor implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f3179-121">Prepare hello VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="f3179-122">Ga te[stap 4: lokale servers voorbereiden](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="f3179-122">Go too[Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="f3179-123">Stap 5: Een kluis instellen</span><span class="sxs-lookup"><span data-stu-id="f3179-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="f3179-124">Stel een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="f3179-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="f3179-125">Hallo-kluis bevat configuratie-instellingen en stuurt replicatie.</span><span class="sxs-lookup"><span data-stu-id="f3179-125">hello vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="f3179-126">[Stap 5: Instellen van een kluis](vmm-to-vmm-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="f3179-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="f3179-127">Stap 6: Bron- en -instellingen instellen</span><span class="sxs-lookup"><span data-stu-id="f3179-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="f3179-128">Hallo bron- en replicatie VMM doellocaties instellen.</span><span class="sxs-lookup"><span data-stu-id="f3179-128">Set up hello source and target replication VMM locations.</span></span> <span data-ttu-id="f3179-129">Hallo VMM-servers toohello kluis toevoegen en downloaden Hallo-installatiebestanden voor de onderdelen van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f3179-129">Add hello VMM servers toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="f3179-130">Azure Site Recovery Provider setup uitvoeren op Hallo VMM-server.</span><span class="sxs-lookup"><span data-stu-id="f3179-130">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="f3179-131">Setup installeert Hallo Provider op Hallo VMM-server en Hallo-server registreren in de kluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3179-131">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="f3179-132">U installeren Hallo Microsoft Recovery Services-agent op elke Hyper-V-host.</span><span class="sxs-lookup"><span data-stu-id="f3179-132">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="f3179-133">Ga te[stap 6: Hallo bron en doel-instellingen instellen](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="f3179-133">Go too[Step 6: Set up hello source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="f3179-134">Stap 7: Netwerktoewijzing configureren</span><span class="sxs-lookup"><span data-stu-id="f3179-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="f3179-135">VMM VM-netwerken in de bron- en doellocaties Hallo worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f3179-135">Map VMM VM networks in hello source and target locations.</span></span> <span data-ttu-id="f3179-136">Na een failover worden virtuele machines gemaakt in het doelnetwerk Hallo dat maps toohello bron VM-netwerk in welke Hallo bron-Hyper-V VM zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="f3179-136">After failover, VMs are created in hello target network that maps toohello source VM network in which hello source Hyper-V VM is located.</span></span>

<span data-ttu-id="f3179-137">Ga te[stap 7: netwerktoewijzing configureren](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="f3179-137">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="f3179-138">Stap 8: Een replicatiebeleid instellen</span><span class="sxs-lookup"><span data-stu-id="f3179-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="f3179-139">Geef op hoe virtuele machines worden gerepliceerd tussen VMM-locaties.</span><span class="sxs-lookup"><span data-stu-id="f3179-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="f3179-140">Ga te[stap 8: Stel een beleid voor wachtwoordreplicatie](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="f3179-140">Go too[Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="f3179-141">Stap 9: Replicatie voor virtuele machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="f3179-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="f3179-142">Hallo-virtuele machines die u wilt dat tooreplicate selecteren.</span><span class="sxs-lookup"><span data-stu-id="f3179-142">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="f3179-143">Als u een virtuele machine voor replicatie triggers Hallo initiële replicatie toohello secundaire site, gevolgd door lopende deltareplicatie.</span><span class="sxs-lookup"><span data-stu-id="f3179-143">Enabling a VM for replication triggers hello initial replication toohello secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="f3179-144">Ga te[stap 9: replicatie inschakelen](vmm-to-vmm-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="f3179-144">Go too[Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="f3179-145">Stap 10: Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f3179-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="f3179-146">Een test failover toomake, controleren of dat alles werkt zoals verwacht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f3179-146">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="f3179-147">Ga te[stap 10: een testfailover uitvoeren](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="f3179-147">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
