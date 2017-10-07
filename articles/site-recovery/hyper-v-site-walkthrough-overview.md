---
title: aaaReplicate Hyper-V-machines tooAzure met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe tooorchestrate replicatie, failover en herstel van on-premises Hyper-V-machines tooAzure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a><span data-ttu-id="43cef-103">Hyper-V virtuele machines (zonder VMM) tooAzure repliceren</span><span class="sxs-lookup"><span data-stu-id="43cef-103">Replicate Hyper-V virtual machines (without VMM) tooAzure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="43cef-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="43cef-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="43cef-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="43cef-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="43cef-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="43cef-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="43cef-107">In dit artikel biedt een overzicht van Hallo stappen die nodig zijn tooreplicate lokale Hyper-V virtuele machines tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="43cef-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> <span data-ttu-id="43cef-108">In deze implementatie van Hyper-V-machines worden niet beheerd door System Center Virtual Machine Manager (VMM).</span><span class="sxs-lookup"><span data-stu-id="43cef-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="43cef-109">Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="43cef-109">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="43cef-110">Stap 1: Bekijk de architectuur en vereisten</span><span class="sxs-lookup"><span data-stu-id="43cef-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="43cef-111">Voordat u de implementatie begint, Controleer Hallo scenario-architectuur en zorg ervoor dat u begrijpt dat alle benodigde toodeploy Hallo-onderdelen</span><span class="sxs-lookup"><span data-stu-id="43cef-111">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="43cef-112">Ga te[stap 1: Bekijk Hallo-architectuur](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="43cef-112">Go too[Step 1: Review hello architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="43cef-113">Stap 2: Controleer vereisten</span><span class="sxs-lookup"><span data-stu-id="43cef-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="43cef-114">Zorg ervoor dat u beschikt over de Hallo vereisten voor elk onderdeel van de implementatie:</span><span class="sxs-lookup"><span data-stu-id="43cef-114">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="43cef-115">**Vereisten voor Azure**: U moet een Microsoft Azure-account Azure-netwerken en opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="43cef-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="43cef-116">**Lokale Hyper-V-vereisten**: Zorg ervoor dat Hyper-V-hosts zijn voorbereid voor implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="43cef-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="43cef-117">**Virtuele machines gerepliceerd**: virtuele machines die u wilt dat tooreplicate moet toocomply met Azure-vereisten.</span><span class="sxs-lookup"><span data-stu-id="43cef-117">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements.</span></span>

<span data-ttu-id="43cef-118">Ga te[stap 2: Controleer of de vereisten en beperkingen](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="43cef-118">Go too[Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="43cef-119">Stap 3: Plan capaciteit</span><span class="sxs-lookup"><span data-stu-id="43cef-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="43cef-120">Als u een volledige implementatie uitvoert moet u toofigure uit welke replicatie bronnen die u nodig.</span><span class="sxs-lookup"><span data-stu-id="43cef-120">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="43cef-121">Er zijn enkele van de hulpprogramma's beschikbaar toohelp u dit doen.</span><span class="sxs-lookup"><span data-stu-id="43cef-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="43cef-122">Ga tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="43cef-122">Go tooStep 2.</span></span> <span data-ttu-id="43cef-123">Als u een snelle tootest Hallo-omgeving instellen alleen kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="43cef-123">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="43cef-124">Ga te[stap 3: plannen van capaciteit](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="43cef-124">Go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="43cef-125">Stap 4: Netwerken plannen</span><span class="sxs-lookup"><span data-stu-id="43cef-125">Step 4: Plan networking</span></span>

<span data-ttu-id="43cef-126">U moet een netwerk tooensure dat de virtuele Azure-machines verbonden toonetworks zijn nadat de failover plaatsvindt en dat er Hallo juiste IP-adressen plannen toodo.</span><span class="sxs-lookup"><span data-stu-id="43cef-126">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="43cef-127">Ga te[stap 4: netwerken plannen](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="43cef-127">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="43cef-128">Stap 5: Azure-resources voorbereiden</span><span class="sxs-lookup"><span data-stu-id="43cef-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="43cef-129">Instellen van Azure-netwerken en opslag voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="43cef-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="43cef-130">U kunt dit doen tijdens de implementatie, maar we raden dat u dit doen voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="43cef-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="43cef-131">Ga te[stap 5: Azure voorbereiden](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="43cef-131">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="43cef-132">Stap 6: Hyper-V voorbereiden</span><span class="sxs-lookup"><span data-stu-id="43cef-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="43cef-133">Zorg ervoor dat Hyper-V-servers voldoen aan vereisten voor implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="43cef-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="43cef-134">Ga te[stap 6: Hyper-V voorbereiden](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="43cef-134">Go too[Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="43cef-135">Stap 7: Een kluis instellen</span><span class="sxs-lookup"><span data-stu-id="43cef-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="43cef-136">U moet tooset van een Recovery Services-kluis tooorchestrate en beheren van replicatie.</span><span class="sxs-lookup"><span data-stu-id="43cef-136">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="43cef-137">Wanneer u Hallo kluis instelt, geeft u op wat u tooreplicate, en waar u tooreplicate naar.</span><span class="sxs-lookup"><span data-stu-id="43cef-137">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="43cef-138">Ga te[stap 7: een kluis maken](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="43cef-138">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="43cef-139">Stap 8: Bron- en -instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="43cef-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="43cef-140">Hallo-bron en doel dat wordt gebruikt voor replicatie instellen.</span><span class="sxs-lookup"><span data-stu-id="43cef-140">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="43cef-141">Instellen van de instellingen van de bronserver houdt het toevoegen van Hyper-V-hosts tooa Hyper-V-site, Hallo Site Recovery Provider en de Recovery Services-agent installeren op elke Hyper-V-host en Hallo site registreren op Hallo die Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="43cef-141">Setting up source settings includes adding Hyper-V hosts tooa Hyper-V site, installing hello Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering hello site in hello Recovery Services vault.</span></span>

<span data-ttu-id="43cef-142">Ga te[stap 8: Hallo bron en doel instellen](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="43cef-142">Go too[Step 8: Set up hello source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="43cef-143">Stap 9: Een replicatiebeleid instellen</span><span class="sxs-lookup"><span data-stu-id="43cef-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="43cef-144">U hebt ingesteld een beleid toospecify replicatie-instellingen voor Hyper-V-machines in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="43cef-144">You set up a policy toospecify replication settings for Hyper-V VMs in hello vault.</span></span>

<span data-ttu-id="43cef-145">Ga te[stap 9: een replicatiebeleid instellen](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="43cef-145">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="43cef-146">Stap 10: De replicatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="43cef-146">Step 10: Enable replication</span></span>

<span data-ttu-id="43cef-147">Nadat u een beleid voor wachtwoordreplicatie aanwezig is, na het inschakelen van hebt, vindt initiële replicatie Hallo VM plaats.</span><span class="sxs-lookup"><span data-stu-id="43cef-147">After you have a replication policy in place,  After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="43cef-148">Ga te[stap 10: replicatie inschakelen](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="43cef-148">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="43cef-149">Stap 11: Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="43cef-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="43cef-150">Nadat de eerste replicatie is voltooid en replicatie van verschillen wordt uitgevoerd, kunt u een test failover toomake, controleren of dat alles werkt zoals verwacht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="43cef-150">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="43cef-151">Ga te[stap 11: een testfailover uitvoeren](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="43cef-151">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
