---
title: aaaReplicate virtuele VMware-machines tooAzure met Azure Site Recovery | Microsoft Docs
description: Biedt een overzicht van Hallo stappen voor het repliceren van de werkbelasting op virtuele VMware-machines tooAzure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a><span data-ttu-id="bb9e6-103">TooAzure met Site Recovery virtuele VMware-machines repliceren</span><span class="sxs-lookup"><span data-stu-id="bb9e6-103">Replicate VMware VMs tooAzure with Site Recovery</span></span>

<span data-ttu-id="bb9e6-104">In dit artikel biedt een overzicht van Hallo stappen vereist tooreplicate lokale VMware virtuele machines tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-104">This article provides an overview of hello steps required tooreplicate on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


![Implementatieproces](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="bb9e6-106">**Afbeelding 1: Implementatieoverzicht**</span><span class="sxs-lookup"><span data-stu-id="bb9e6-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="bb9e6-107">Stap 1: Bekijk de architectuur en vereisten</span><span class="sxs-lookup"><span data-stu-id="bb9e6-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="bb9e6-108">Voordat u de implementatie begint, Controleer Hallo scenario-architectuur en zorg ervoor dat u begrijpt dat alle benodigde toodeploy Hallo-onderdelen</span><span class="sxs-lookup"><span data-stu-id="bb9e6-108">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="bb9e6-109">Ga te[stap 1: Bekijk Hallo-architectuur](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="bb9e6-109">Go too[Step 1: Review hello architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="bb9e6-110">Stap 2: Controleer vereisten</span><span class="sxs-lookup"><span data-stu-id="bb9e6-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="bb9e6-111">Zorg ervoor dat u beschikt over de Hallo vereisten voor elk onderdeel van de implementatie:</span><span class="sxs-lookup"><span data-stu-id="bb9e6-111">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="bb9e6-112">**Vereisten voor Azure**: U moet een Microsoft Azure-account Azure-netwerken en opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="bb9e6-113">**Site Recovery-onderdelen op lokale**: U moet een machine met on-premises Site Recovery-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="bb9e6-114">**Lokale VMware vereisten**: U moet tooset accounts zodat Site Recovery toegang hebben tot VMware-servers en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-114">**On-premises VMware prerequisites**: You need tooset up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="bb9e6-115">**Virtuele machines gerepliceerd**: VM's u wilt tooreplicate nodig toocomply met Azure-vereisten en Hallo Mobility serviceonderdeel is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-115">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements, and have hello Mobility service component installed.</span></span>

<span data-ttu-id="bb9e6-116">Ga te[stap 2: Controleer de vereisten en beperkingen](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="bb9e6-116">Go too[Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="bb9e6-117">Stap 3: Plan capaciteit</span><span class="sxs-lookup"><span data-stu-id="bb9e6-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="bb9e6-118">Als u een volledige implementatie uitvoert moet u toofigure uit welke replicatie bronnen die u nodig.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-118">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="bb9e6-119">Er zijn enkele van de hulpprogramma's beschikbaar toohelp u dit doen.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-119">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="bb9e6-120">Ga tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-120">Go tooStep 2.</span></span> <span data-ttu-id="bb9e6-121">Als u een snelle tootest Hallo-omgeving instellen alleen kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-121">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="bb9e6-122">Ga te[stap 3: plannen van capaciteit](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="bb9e6-122">Go too[Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="bb9e6-123">Stap 4: Netwerken plannen</span><span class="sxs-lookup"><span data-stu-id="bb9e6-123">Step 4: Plan networking</span></span>

<span data-ttu-id="bb9e6-124">U moet een netwerk tooensure dat de virtuele Azure-machines verbonden toonetworks zijn nadat de failover plaatsvindt en dat er Hallo juiste IP-adressen plannen toodo.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-124">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="bb9e6-125">Ga te[stap 4: netwerken plannen](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="bb9e6-125">Go too[Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="bb9e6-126">Stap 5: Azure-resources voorbereiden</span><span class="sxs-lookup"><span data-stu-id="bb9e6-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="bb9e6-127">Instellen van Azure-netwerken en opslag voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="bb9e6-128">U kunt dit doen tijdens de implementatie, maar we raden dat u dit doen voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="bb9e6-129">Ga te[stap 5: Azure voorbereiden](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="bb9e6-129">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="bb9e6-130">Stap 6: VMware voorbereiden</span><span class="sxs-lookup"><span data-stu-id="bb9e6-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="bb9e6-131">U moet tooset accounts die Site Recovery gebruiken voor:</span><span class="sxs-lookup"><span data-stu-id="bb9e6-131">You need tooset up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="bb9e6-132">Toegang VMware virtualisatie servers tooautomatically detecteren voor virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-132">Access VMware virtualization servers tooautomatically detect VMs.</span></span>
- <span data-ttu-id="bb9e6-133">Toegang tot virtuele machines tooinstall Hallo Mobility-service.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-133">Access VMs tooinstall hello Mobility service.</span></span> <span data-ttu-id="bb9e6-134">Elke VM die u wilt dat tooreplicate moet hebben Hallo Mobility service agent is geïnstalleerd voordat u kunt replicatie inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-134">Each VM you want tooreplicate must have hello Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="bb9e6-135">Ga te[stap 6: VMware voorbereiden](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="bb9e6-135">Go too[Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="bb9e6-136">Stap 7: Een kluis instellen</span><span class="sxs-lookup"><span data-stu-id="bb9e6-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="bb9e6-137">U moet tooset van een Recovery Services-kluis tooorchestrate en beheren van replicatie.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-137">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="bb9e6-138">Wanneer u Hallo kluis instelt, geeft u op wat u tooreplicate, en waar u tooreplicate naar.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-138">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="bb9e6-139">Ga te[stap 7: een kluis instellen](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="bb9e6-139">Go too[Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="bb9e6-140">Stap 8: Bron- en -instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="bb9e6-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="bb9e6-141">Hallo-bron en doel dat wordt gebruikt voor replicatie instellen.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-141">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="bb9e6-142">Instellen van de instellingen van de bronserver omvat Hallo on-premises Site Recovery-onderdelen voor Setup Unified tooinstall uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-142">Setting up source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="bb9e6-143">Ga te[stap 8: Hallo bron en doel instellen](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="bb9e6-143">Go too[Step 8: Set up hello source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="bb9e6-144">Stap 9: Een replicatiebeleid instellen</span><span class="sxs-lookup"><span data-stu-id="bb9e6-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="bb9e6-145">U hebt ingesteld een beleid toospecify replicatie-instellingen voor virtuele VMware-machines in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-145">You set up a policy toospecify replication settings for VMware VMs in hello vault.</span></span>

<span data-ttu-id="bb9e6-146">Ga te[stap 9: een replicatiebeleid instellen](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="bb9e6-146">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="bb9e6-147">Stap 10: Hallo Mobility-service installeren</span><span class="sxs-lookup"><span data-stu-id="bb9e6-147">Step 10: Install hello Mobility service</span></span>

<span data-ttu-id="bb9e6-148">Hallo Mobility-service moet worden geïnstalleerd op elke virtuele machine die u wilt tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-148">hello Mobility service must be installed on each VM you want tooreplicate.</span></span> <span data-ttu-id="bb9e6-149">Er zijn enkele manieren tooset Hallo service push of pull-installatie.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-149">There are a few ways tooset up hello service with push or pull installation.</span></span>

<span data-ttu-id="bb9e6-150">Ga te[stap 10: Hallo Mobility-service installeren](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="bb9e6-150">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="bb9e6-151">Stap 11: Replicatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="bb9e6-151">Step 11: Enable replication</span></span>

<span data-ttu-id="bb9e6-152">U kunt replicatie inschakelen nadat Hallo Mobility-service wordt uitgevoerd op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-152">After hello Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="bb9e6-153">Na het inschakelen, initiële replicatie van Hallo VM zich voordoet.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-153">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="bb9e6-154">Ga te[stap 11: replicatie inschakelen](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="bb9e6-154">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="bb9e6-155">Stap 12: Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bb9e6-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="bb9e6-156">Nadat de eerste replicatie is voltooid en replicatie van verschillen wordt uitgevoerd, kunt u een test failover toomake, controleren of dat alles werkt zoals verwacht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bb9e6-156">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="bb9e6-157">Ga te[stap 12: een testfailover uitvoeren](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="bb9e6-157">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
