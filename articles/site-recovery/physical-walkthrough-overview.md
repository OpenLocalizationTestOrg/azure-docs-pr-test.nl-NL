---
title: Fysieke repliceren lokale servers naar Azure met Azure Site Recovery | Microsoft Docs
description: Biedt een overzicht van de stappen voor het repliceren van workloads die worden uitgevoerd op fysieke on-premises Windows of Linux-servers naar Azure met de Azure Site Recovery-service.
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
ms.openlocfilehash: 0a09b35e98dc0b2f5283c2a707a3a2b8ac9a39f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-physical-servers-to-azure-with-site-recovery"></a><span data-ttu-id="cb9a4-103">Fysieke servers repliceren naar Azure met Site Recovery</span><span class="sxs-lookup"><span data-stu-id="cb9a4-103">Replicate physical servers to Azure with Site Recovery</span></span>

<span data-ttu-id="cb9a4-104">In dit artikel biedt een overzicht van de stappen die nodig zijn voor het repliceren van fysieke on-premises Windows of Linux-servers naar Azure, met behulp van de [Azure Site Recovery](site-recovery-overview.md) service in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-104">This article provides an overview of the steps required to replicate on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="cb9a4-105">Stap 1: Bekijk de architectuur en vereisten</span><span class="sxs-lookup"><span data-stu-id="cb9a4-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="cb9a4-106">Voordat u de implementatie begint, Controleer de scenarioarchitectuur en zorg dat u begrijpt dat alle onderdelen die u nodig hebt voor het instellen van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-106">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to set up the deployment.</span></span>

<span data-ttu-id="cb9a4-107">Ga naar [stap 1: Bekijk de architectuur](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="cb9a4-107">Go to [Step 1: Review the architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="cb9a4-108">Stap 2: Controleer vereisten</span><span class="sxs-lookup"><span data-stu-id="cb9a4-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="cb9a4-109">Zorg ervoor dat u beschikken over de vereisten voor elk onderdeel van de implementatie:</span><span class="sxs-lookup"><span data-stu-id="cb9a4-109">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="cb9a4-110">**Vereisten voor Azure**: U moet een Microsoft Azure-account Azure-netwerken en opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="cb9a4-111">**Site Recovery-onderdelen op lokale**: U moet een machine met on-premises Site Recovery-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="cb9a4-112">**Gerepliceerde machines**: u wilt repliceren Servers moeten voldoen aan de on-premises en Azure-vereisten.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-112">**Replicated machines**: Servers you want to replicate need to comply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="cb9a4-113">Ga naar [stap 2: Controleer de vereisten en beperkingen](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="cb9a4-113">Go to [Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="cb9a4-114">Stap 3: Plan capaciteit</span><span class="sxs-lookup"><span data-stu-id="cb9a4-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="cb9a4-115">Als u een volledige implementatie uitvoert moet u achterhalen welke replicatie bronnen die u nodig.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-115">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="cb9a4-116">Als u een snelle instellen voor het testen van de omgeving doet, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-116">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="cb9a4-117">[Stap 3: Capaciteit plannen](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="cb9a4-117">Go to [Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="cb9a4-118">Stap 4: Netwerken plannen</span><span class="sxs-lookup"><span data-stu-id="cb9a4-118">Step 4: Plan networking</span></span>

<span data-ttu-id="cb9a4-119">U moet uitvoeren van een netwerk om ervoor te zorgen dat virtuele Azure-machines zijn verbonden met netwerken nadat er failover wordt uitgevoerd en die dat ze het juiste IP hebben-adressen.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-119">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="cb9a4-120">Ga naar [stap 4: netwerken plannen](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="cb9a4-120">Go to [Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="cb9a4-121">Stap 5: Azure-resources voorbereiden</span><span class="sxs-lookup"><span data-stu-id="cb9a4-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="cb9a4-122">Instellen van Azure-netwerken en opslag voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="cb9a4-123">Ga naar [stap 5: Azure voorbereiden](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="cb9a4-123">Go to [Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="cb9a4-124">Stap 6: Een kluis instellen</span><span class="sxs-lookup"><span data-stu-id="cb9a4-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="cb9a4-125">U instellen kunt een Recovery Services-kluis organiseren en beheren van replicatie.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-125">You set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="cb9a4-126">Wanneer u de kluis instelt, geeft u wat u wilt repliceren en waar u naar wilt repliceren naar.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-126">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="cb9a4-127">Ga naar [stap 6: een kluis instellen](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="cb9a4-127">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="cb9a4-128">Stap 7: De bron en doel-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="cb9a4-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="cb9a4-129">Configureer instellingen voor de bron en doelsite (Azure).</span><span class="sxs-lookup"><span data-stu-id="cb9a4-129">Configure settings for the source and target (Azure) site.</span></span> <span data-ttu-id="cb9a4-130">Instellingen van de bronserver omvat Unified installatieprogramma voor het installeren van de on-premises Site Recovery-onderdelen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-130">Source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="cb9a4-131">Ga naar [stap 7: de bron en doel instellen](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="cb9a4-131">Go to [Step 7: Set up the source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="cb9a4-132">Stap 8: Een replicatiebeleid instellen</span><span class="sxs-lookup"><span data-stu-id="cb9a4-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="cb9a4-133">U moet een beleid om op te geven welke fysieke servers repliceren.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-133">You set up a policy to specify how physical servers should replicate.</span></span>

<span data-ttu-id="cb9a4-134">Ga naar [stap 8: een replicatiebeleid instellen](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="cb9a4-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="cb9a4-135">Stap 9: Installeer de Mobility-service</span><span class="sxs-lookup"><span data-stu-id="cb9a4-135">Step 9: Install the Mobility service</span></span>

<span data-ttu-id="cb9a4-136">De Mobility-service moet worden geïnstalleerd op elke server die u wilt repliceren.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-136">The Mobility service must be installed on each server you want to replicate.</span></span> <span data-ttu-id="cb9a4-137">Er zijn een aantal manieren voor het instellen van de service, push of pull-installatie.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-137">There are a few ways to set up the service, with push or pull installation.</span></span>

<span data-ttu-id="cb9a4-138">Ga naar [stap 9: de Mobility-service installeren](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="cb9a4-138">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="cb9a4-139">Stap 10: De replicatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="cb9a4-139">Step 10: Enable replication</span></span>

<span data-ttu-id="cb9a4-140">Nadat de Mobility-service wordt uitgevoerd op een server, kunt u replicatie inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-140">After the Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="cb9a4-141">Na het inschakelen, treedt initiële replicatie van de virtuele machine op.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-141">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="cb9a4-142">Ga naar [stap 10: replicatie inschakelen](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="cb9a4-142">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="cb9a4-143">Stap 11: Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="cb9a4-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="cb9a4-144">Nadat de eerste replicatie is voltooid en de replicatie van verschillen wordt uitgevoerd, kunt u een testfailover om te controleren of dat alles werkt zoals verwacht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cb9a4-144">After initial replication finishes and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="cb9a4-145">Ga naar [stap 11: een testfailover uitvoeren](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="cb9a4-145">Go to [Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

