---
title: aaaReplicate Hyper-V-machines in VMM-clouds tooAzure met Azure Site Recovery | Microsoft Docs
description: Biedt een overzicht voor het repliceren van Hyper-V-machines in VMM-clouds tooAzure hello Azure Site Recovery-service gebruiken
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a><span data-ttu-id="6ba94-103">Hyper-V virtuele machines in VMM-clouds tooAzure met Site Recovery in hello Azure-portal repliceren</span><span class="sxs-lookup"><span data-stu-id="6ba94-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6ba94-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6ba94-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="6ba94-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6ba94-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="6ba94-106">PowerShell Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6ba94-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="6ba94-107">PowerShell klassiek</span><span class="sxs-lookup"><span data-stu-id="6ba94-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="6ba94-108">In dit artikel biedt een overzicht van Hallo stappen vereist tooreplicate lokale Hyper-V virtuele machines (VM's) in System Center Virtual Machine Manager (VMM) clouds tooAzure, met behulp van Hallo beheerd [Azure Site Recovery](site-recovery-overview.md) service in Hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6ba94-108">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="6ba94-109">Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6ba94-109">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="6ba94-110">Stap 1: Bekijk Hallo scenario-architectuur</span><span class="sxs-lookup"><span data-stu-id="6ba94-110">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="6ba94-111">Voordat de implementatie start, bekijk Hallo scenario-architectuur en zorg ervoor dat u weet dat alle Hallo onderdelen moet u toodeploy.</span><span class="sxs-lookup"><span data-stu-id="6ba94-111">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="6ba94-112">Ga te[stap 1: Bekijk Hallo-architectuur](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="6ba94-112">Go too[Step 1: Review hello architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="6ba94-113">Stap 2: Controleer de vereisten en beperkingen</span><span class="sxs-lookup"><span data-stu-id="6ba94-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="6ba94-114">Zorg ervoor dat u Hallo implementatievereisten en beperkingen begrijpt.</span><span class="sxs-lookup"><span data-stu-id="6ba94-114">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="6ba94-115">**Vereisten voor Azure**: U moet een Microsoft Azure-account Azure-netwerken en opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="6ba94-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="6ba94-116">**On-premises VMM-servers en Hyper-V-hosts**: Zorg ervoor dat VMM-servers en Hyper-V-hosts compatibele en voorbereid voor implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6ba94-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="6ba94-117">**Virtuele machines gerepliceerd**: Controleer of de virtuele machines die u wilt dat tooreplicate Azure-vereisten voldoen.</span><span class="sxs-lookup"><span data-stu-id="6ba94-117">**Replicated VMs**: Check that VMs you want tooreplicate comply with Azure requirements.</span></span>

<span data-ttu-id="6ba94-118">Ga te[stap 2: Controleer of de vereisten en beperkingen](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="6ba94-118">Go too[Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="6ba94-119">Stap 3: Plan capaciteit</span><span class="sxs-lookup"><span data-stu-id="6ba94-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="6ba94-120">Als u een volledige implementatie uitvoert, moet u toofigure welke replicatie bronnen die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="6ba94-120">If you're doing a full deployment, you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="6ba94-121">Er zijn enkele van de hulpprogramma's beschikbaar toohelp u dit doen.</span><span class="sxs-lookup"><span data-stu-id="6ba94-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="6ba94-122">Als u een snelle tootest Hallo-omgeving instellen doet, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="6ba94-122">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="6ba94-123">Ga te[stap 3: plannen van capaciteit](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="6ba94-123">Go too[Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="6ba94-124">Stap 4: Netwerken plannen</span><span class="sxs-lookup"><span data-stu-id="6ba94-124">Step 4: Plan networking</span></span>

<span data-ttu-id="6ba94-125">Moet u toodo sommige netwerk planning tooensure die u bij het implementeren van Hallo scenario netwerktoewijzing kunt configureren dat virtuele Azure-machines verbonden tooAzure virtuele netwerken zijn nadat de failover wordt uitgevoerd en die dat ze zijn toegewezen aan geschikte IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="6ba94-125">You need toodo some network planning tooensure that you can configure network mapping when you deploy hello scenario, that Azure VMs will be connected tooAzure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="6ba94-126">Ga te[stap 4: netwerken plannen](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="6ba94-126">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="6ba94-127">Stap 5: Azure-resources voorbereiden</span><span class="sxs-lookup"><span data-stu-id="6ba94-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="6ba94-128">Instellen van een Azure-account, netwerken en opslag.</span><span class="sxs-lookup"><span data-stu-id="6ba94-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="6ba94-129">U kunt dit doen tijdens de implementatie, maar we raden dat u dit doen voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="6ba94-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="6ba94-130">Ga te[stap 5: Azure voorbereiden](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="6ba94-130">Go too[Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="6ba94-131">Stap 6: Voorbereiden VMM en Hyper-V</span><span class="sxs-lookup"><span data-stu-id="6ba94-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="6ba94-132">Hallo lokale VMM-servers en Hyper-V-hosts voorbereiden voor implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6ba94-132">Prepare hello on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="6ba94-133">Ga te[stap 6: lokale servers voorbereiden](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="6ba94-133">Go too[Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="6ba94-134">Stap 7: Een kluis instellen</span><span class="sxs-lookup"><span data-stu-id="6ba94-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="6ba94-135">Stel een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="6ba94-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="6ba94-136">Hallo-kluis bevat configuratie-instellingen en stuurt replicatie.</span><span class="sxs-lookup"><span data-stu-id="6ba94-136">hello vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="6ba94-137">Stap 7: Een kluis instellen</span><span class="sxs-lookup"><span data-stu-id="6ba94-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="6ba94-138">Stap 8: Bron- en -instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="6ba94-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="6ba94-139">Hallo bron- en replicatie doellocaties instellen.</span><span class="sxs-lookup"><span data-stu-id="6ba94-139">Set up hello source and target replication locations.</span></span> <span data-ttu-id="6ba94-140">Hallo VMM server toohello kluis toevoegen en downloaden Hallo-installatiebestanden voor de onderdelen van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6ba94-140">Add hello VMM server toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="6ba94-141">Azure Site Recovery Provider setup uitvoeren op Hallo VMM-server.</span><span class="sxs-lookup"><span data-stu-id="6ba94-141">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="6ba94-142">Setup installeert Hallo Provider op Hallo VMM-server en Hallo-server registreren in de kluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="6ba94-142">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="6ba94-143">U installeren Hallo Microsoft Recovery Services-agent op elke Hyper-V-host.</span><span class="sxs-lookup"><span data-stu-id="6ba94-143">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="6ba94-144">Ga te[stap 8: bron- en -instellingen configureren](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="6ba94-144">Go too[Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="6ba94-145">Stap 9: Netwerktoewijzing configureren</span><span class="sxs-lookup"><span data-stu-id="6ba94-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="6ba94-146">Kaart een on-premises VMM VM-netwerken tooAzure virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="6ba94-146">Map on-premises VMM VM networks tooAzure virtual networks.</span></span> <span data-ttu-id="6ba94-147">Na een failover worden Azure VM's gemaakt in hello Azure-netwerk dat is toegewezen toohello on-premises VM-netwerk in welke Hallo Hyper-V-bron zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="6ba94-147">After failover, Azure VMs are created in hello Azure network that maps toohello on-premises VM network in which hello source Hyper-V is located.</span></span>

<span data-ttu-id="6ba94-148">Ga te[stap 9: netwerktoewijzing configureren](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="6ba94-148">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="6ba94-149">Stap 10: Een replicatiebeleid instellen</span><span class="sxs-lookup"><span data-stu-id="6ba94-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="6ba94-150">Opgeven hoe lokale VMs gerepliceerde tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6ba94-150">Specify how on-premises VMs will be replicated tooAzure.</span></span>

<span data-ttu-id="6ba94-151">Ga te[stap 10: een replicatiebeleid instellen](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6ba94-151">Go too[Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="6ba94-152">Stap 11: Replicatie voor virtuele machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="6ba94-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="6ba94-153">Hallo-virtuele machines die u wilt dat tooreplicate selecteren.</span><span class="sxs-lookup"><span data-stu-id="6ba94-153">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="6ba94-154">Als u een VM voor replicatie triggers Hallo initiële replicatie tooAzure, gevolgd door lopende deltareplicatie.</span><span class="sxs-lookup"><span data-stu-id="6ba94-154">ENabling a VM for replication triggers hello initial replication tooAzure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="6ba94-155">Ga te[stap 11: replicatie inschakelen](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6ba94-155">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="6ba94-156">Stap 12: Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6ba94-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="6ba94-157">Een test failover toomake, controleren of dat alles werkt zoals verwacht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6ba94-157">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="6ba94-158">Ga te[stap 12: een testfailover uitvoeren](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="6ba94-158">Go too[Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


