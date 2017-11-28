---
title: fysieke aaaReplicate lokale servers tooAzure met Azure Site Recovery | Microsoft Docs
description: Biedt een overzicht van Hallo stappen voor het repliceren van workloads die worden uitgevoerd op de lokale Windows-/ Linux fysieke servers tooAzure Hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a><span data-ttu-id="ef46e-103">Replicatie van fysieke servers tooAzure met Site Recovery</span><span class="sxs-lookup"><span data-stu-id="ef46e-103">Replicate physical servers tooAzure with Site Recovery</span></span>

<span data-ttu-id="ef46e-104">In dit artikel biedt een overzicht van Hallo stappen vereist tooreplicate lokale Windows-/ Linux fysieke servers tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ef46e-104">This article provides an overview of hello steps required tooreplicate on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="ef46e-105">Stap 1: Bekijk de architectuur en vereisten</span><span class="sxs-lookup"><span data-stu-id="ef46e-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="ef46e-106">Voordat u de implementatie begint, Controleer Hallo scenario-architectuur en zorg ervoor dat u begrijpt dat alle benodigde tooset Hallo implementatie Hallo-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="ef46e-106">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need tooset up hello deployment.</span></span>

<span data-ttu-id="ef46e-107">Ga te[stap 1: Bekijk Hallo-architectuur](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="ef46e-107">Go too[Step 1: Review hello architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="ef46e-108">Stap 2: Controleer vereisten</span><span class="sxs-lookup"><span data-stu-id="ef46e-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="ef46e-109">Zorg ervoor dat u beschikt over de Hallo vereisten voor elk onderdeel van de implementatie:</span><span class="sxs-lookup"><span data-stu-id="ef46e-109">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="ef46e-110">**Vereisten voor Azure**: U moet een Microsoft Azure-account Azure-netwerken en opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="ef46e-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="ef46e-111">**Site Recovery-onderdelen op lokale**: U moet een machine met on-premises Site Recovery-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="ef46e-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="ef46e-112">**Gerepliceerde machines**: Servers die u wilt dat tooreplicate moeten toocomply met on-premises en Azure-vereisten.</span><span class="sxs-lookup"><span data-stu-id="ef46e-112">**Replicated machines**: Servers you want tooreplicate need toocomply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="ef46e-113">Ga te[stap 2: Controleer de vereisten en beperkingen](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="ef46e-113">Go too[Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="ef46e-114">Stap 3: Plan capaciteit</span><span class="sxs-lookup"><span data-stu-id="ef46e-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="ef46e-115">Als u een volledige implementatie uitvoert moet u toofigure uit welke replicatie bronnen die u nodig.</span><span class="sxs-lookup"><span data-stu-id="ef46e-115">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="ef46e-116">Als u een snelle tootest Hallo-omgeving instellen doet, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="ef46e-116">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="ef46e-117">Ga te[stap 3: plannen van capaciteit](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="ef46e-117">Go too[Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="ef46e-118">Stap 4: Netwerken plannen</span><span class="sxs-lookup"><span data-stu-id="ef46e-118">Step 4: Plan networking</span></span>

<span data-ttu-id="ef46e-119">U moet een netwerk tooensure dat de virtuele Azure-machines verbonden toonetworks zijn nadat de failover plaatsvindt en dat er Hallo juiste IP-adressen plannen toodo.</span><span class="sxs-lookup"><span data-stu-id="ef46e-119">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="ef46e-120">Ga te[stap 4: netwerken plannen](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="ef46e-120">Go too[Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="ef46e-121">Stap 5: Azure-resources voorbereiden</span><span class="sxs-lookup"><span data-stu-id="ef46e-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="ef46e-122">Instellen van Azure-netwerken en opslag voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="ef46e-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="ef46e-123">Ga te[stap 5: Azure voorbereiden](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="ef46e-123">Go too[Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="ef46e-124">Stap 6: Een kluis instellen</span><span class="sxs-lookup"><span data-stu-id="ef46e-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="ef46e-125">U een Recovery Services-kluis tooorchestrate instellen en beheren van replicatie.</span><span class="sxs-lookup"><span data-stu-id="ef46e-125">You set up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="ef46e-126">Wanneer u Hallo kluis instelt, geeft u op wat u tooreplicate, en waar u tooreplicate naar.</span><span class="sxs-lookup"><span data-stu-id="ef46e-126">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="ef46e-127">Ga te[stap 6: een kluis instellen](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="ef46e-127">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="ef46e-128">Stap 7: De bron en doel-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="ef46e-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="ef46e-129">Instellingen configureren voor Hallo bron en doel (Azure) site.</span><span class="sxs-lookup"><span data-stu-id="ef46e-129">Configure settings for hello source and target (Azure) site.</span></span> <span data-ttu-id="ef46e-130">Instellingen van de bronserver omvat Hallo on-premises Site Recovery-onderdelen voor Setup Unified tooinstall uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ef46e-130">Source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="ef46e-131">Ga te[stap 7: Hallo bron en doel instellen](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="ef46e-131">Go too[Step 7: Set up hello source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="ef46e-132">Stap 8: Een replicatiebeleid instellen</span><span class="sxs-lookup"><span data-stu-id="ef46e-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="ef46e-133">Instellen van een beleid toospecify welke fysieke servers te repliceren.</span><span class="sxs-lookup"><span data-stu-id="ef46e-133">You set up a policy toospecify how physical servers should replicate.</span></span>

<span data-ttu-id="ef46e-134">Ga te[stap 8: een replicatiebeleid instellen](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ef46e-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="ef46e-135">Stap 9: Hallo Mobility-service installeren</span><span class="sxs-lookup"><span data-stu-id="ef46e-135">Step 9: Install hello Mobility service</span></span>

<span data-ttu-id="ef46e-136">Hallo Mobility-service moet worden geïnstalleerd op elke server die u wilt tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="ef46e-136">hello Mobility service must be installed on each server you want tooreplicate.</span></span> <span data-ttu-id="ef46e-137">Er zijn enkele manieren tooset Hallo-service met push of pull-installatie.</span><span class="sxs-lookup"><span data-stu-id="ef46e-137">There are a few ways tooset up hello service, with push or pull installation.</span></span>

<span data-ttu-id="ef46e-138">Ga te[stap 9: Hallo Mobility-service installeren](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="ef46e-138">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="ef46e-139">Stap 10: De replicatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="ef46e-139">Step 10: Enable replication</span></span>

<span data-ttu-id="ef46e-140">Nadat het Hallo Mobility-service wordt uitgevoerd op een server, kunt u replicatie inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ef46e-140">After hello Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="ef46e-141">Na het inschakelen, initiële replicatie van Hallo VM zich voordoet.</span><span class="sxs-lookup"><span data-stu-id="ef46e-141">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="ef46e-142">Ga te[stap 10: replicatie inschakelen](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ef46e-142">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="ef46e-143">Stap 11: Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ef46e-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="ef46e-144">Nadat de eerste replicatie is voltooid en de replicatie van verschillen wordt uitgevoerd, kunt u een test failover toomake, controleren of dat alles werkt zoals verwacht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ef46e-144">After initial replication finishes and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="ef46e-145">Ga te[stap 11: een testfailover uitvoeren](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="ef46e-145">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

