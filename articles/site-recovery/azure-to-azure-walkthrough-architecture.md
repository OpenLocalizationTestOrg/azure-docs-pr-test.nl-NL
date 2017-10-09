---
title: Hallo-architectuur voor de replicatie van Azure VM's tussen Azure-regio's aaaReview | Microsoft Docs
description: Dit artikel bevat een overzicht van de onderdelen en de architectuur die wordt gebruikt voor het virtuele Azure-machines repliceren tussen Azure-regio's met behulp van hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="1e5e0-103">Stap 1: Bekijk Hallo-architectuur voor replicatie van de virtuele machine van Azure tussen Azure-regio 's</span><span class="sxs-lookup"><span data-stu-id="1e5e0-103">Step 1: Review hello architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="1e5e0-104">Nadat u hebt bekeken Hallo [overzicht stappen](azure-to-azure-walkthrough-overview.md) voor deze implementatie Lees dit artikel toounderstand Hallo onderdelen en -processen die worden gebruikt bij het repliceren en herstellen van de virtuele Azure-machines (VM's) van een Azure-regio tooanother, met behulp van [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e5e0-104">After reviewing hello [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article toounderstand hello components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region tooanother, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="1e5e0-105">Wanneer u klaar bent met Hallo artikel, moet u een duidelijk beeld van de werking van Azure VM replicatie tooanother regio hebben.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-105">When you finish hello article, you should have a clear understanding of how Azure VM replication tooanother region works.</span></span>
- <span data-ttu-id="1e5e0-106">Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1e5e0-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="1e5e0-107">Azure VM-replicatie met Hallo Site Recovery-service is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-107">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="1e5e0-108">Architectuuronderdelen</span><span class="sxs-lookup"><span data-stu-id="1e5e0-108">Architectural components</span></span>

<span data-ttu-id="1e5e0-109">Hallo volgende diagram toont een globaal overzicht van een virtuele machine van Azure-omgeving in een specifieke regio (in dit voorbeeld Hallo locatie VS-Oost).</span><span class="sxs-lookup"><span data-stu-id="1e5e0-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="1e5e0-110">In een virtuele machine van Azure-omgeving:</span><span class="sxs-lookup"><span data-stu-id="1e5e0-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="1e5e0-111">Apps kunnen worden uitgevoerd op virtuele machines met schijven die zijn verdeeld over de storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="1e5e0-112">Hallo virtuele machines kan worden opgenomen in een of meer subnetten binnen een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![klant-omgeving](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="1e5e0-114">Replicatieproces</span><span class="sxs-lookup"><span data-stu-id="1e5e0-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="1e5e0-115">Stap 1</span><span class="sxs-lookup"><span data-stu-id="1e5e0-115">Step 1</span></span>

<span data-ttu-id="1e5e0-116">Wanneer u Azure VM-replicatie in hello Azure-portal inschakelt, Hallo bronnen die in het volgende Hallo diagram en de tabel automatisch worden gemaakt in Hallo doelregio.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-116">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="1e5e0-117">Resources worden gemaakt op basis van regio broninstellingen standaard.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="1e5e0-118">Hallo-doelinstellingen zo nodig kunt u aanpassen.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-118">You can customize hello target settings as required.</span></span> <span data-ttu-id="1e5e0-119">[Meer informatie](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="1e5e0-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Stap 1 replicatieproces inschakelen](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="1e5e0-121">**Resource**</span><span class="sxs-lookup"><span data-stu-id="1e5e0-121">**Resource**</span></span> | <span data-ttu-id="1e5e0-122">**Details**</span><span class="sxs-lookup"><span data-stu-id="1e5e0-122">**Details**</span></span>
--- | ---
<span data-ttu-id="1e5e0-123">**Doelresourcegroep**</span><span class="sxs-lookup"><span data-stu-id="1e5e0-123">**Target resource group**</span></span> | <span data-ttu-id="1e5e0-124">Hallo resource groep toowhich gerepliceerde virtuele machines na een failover behoren.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-124">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="1e5e0-125">**Doel virtueel netwerk**</span><span class="sxs-lookup"><span data-stu-id="1e5e0-125">**Target virtual network**</span></span> | <span data-ttu-id="1e5e0-126">Hallo-netwerk waarin gerepliceerde virtuele machines zich bevinden na een failover.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-126">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="1e5e0-127">Een netwerktoewijzing wordt gemaakt tussen bron- en virtuele netwerken, en vice versa.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="1e5e0-128">**Cache-opslagaccounts**</span><span class="sxs-lookup"><span data-stu-id="1e5e0-128">**Cache storage accounts**</span></span> | <span data-ttu-id="1e5e0-129">Voordat u wijzigingen op de bron-VM's zijn gerepliceerd toohello doel storage-account, worden ze bijgehouden en toohello cache storage-account in de doellocatie Hallo verzonden.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-129">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="1e5e0-130">Dit zorgt ervoor minimale gevolgen voor de productie-apps die worden uitgevoerd op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-130">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="1e5e0-131">**Doel storage-accounts**</span><span class="sxs-lookup"><span data-stu-id="1e5e0-131">**Target storage accounts**</span></span>  | <span data-ttu-id="1e5e0-132">Storage-accounts in Hallo doel toowhich Hallo locatiegegevens wordt gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-132">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="1e5e0-133">**Doel-beschikbaarheidssets**</span><span class="sxs-lookup"><span data-stu-id="1e5e0-133">**Target availability sets**</span></span>  | <span data-ttu-id="1e5e0-134">Beschikbaarheidssets in welke Hallo gerepliceerde virtuele machines zich bevinden na een failover.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-134">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="1e5e0-135">Stap 2</span><span class="sxs-lookup"><span data-stu-id="1e5e0-135">Step 2</span></span>

<span data-ttu-id="1e5e0-136">Als replicatie is ingeschakeld, wordt automatisch Hallo Site Recovery-extensie Mobility-service op Hallo VM geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-136">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="1e5e0-137">Hallo volgende gebeurt:</span><span class="sxs-lookup"><span data-stu-id="1e5e0-137">hello following occurs:</span></span>

1. <span data-ttu-id="1e5e0-138">Hallo VM is geregistreerd met Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-138">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="1e5e0-139">Continue replicatie is geconfigureerd voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-139">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="1e5e0-140">Schrijft gegevens op Hallo VM met schijven zijn continu toohello cache storage-account in de bronlocatie Hallo overgedragen.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-140">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Stap 2 replicatieproces inschakelen](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="1e5e0-142">Houd er rekening mee dat de Site Recovery nooit moet binnenkomende verbindingen toohello VM.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-142">Note that Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="1e5e0-143">Alleen uitgaande connectiviteit tooSite Recovery-service-URL's of het IP-adressen, Office 365-verificatie-URL's of het IP-adressen en IP-adressen van cache storage-account nodig.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-143">Only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="1e5e0-144">Continue replicatie in proces</span><span class="sxs-lookup"><span data-stu-id="1e5e0-144">Continuous replication process</span></span>

<span data-ttu-id="1e5e0-145">Nadat u continue replicatie werkt, overgedragen schijf schrijfbewerkingen onmiddellijk zijn toohello cache storage-account.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-145">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="1e5e0-146">Site Recovery Hallo gegevens verwerkt en verzendt het toohello doel storage-account.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-146">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="1e5e0-147">Nadat het Hallo-gegevens zijn verwerkt, worden herstelpunten gegenereerd in Hallo doel storage-account om de paar minuten.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-147">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="1e5e0-148">Failover-proces</span><span class="sxs-lookup"><span data-stu-id="1e5e0-148">Failover process</span></span>

<span data-ttu-id="1e5e0-149">Wanneer u een failover initieert, doel virtuele machines worden gemaakt in de doelresourcegroep hello, virtuele doelnetwerk, Doelsubnet Hallo en Hallo-beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-149">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="1e5e0-150">U kunt een willekeurig herstelpunt gebruiken tijdens een failover.</span><span class="sxs-lookup"><span data-stu-id="1e5e0-150">During a failover, you can use any recovery point.</span></span>

![Failover-proces](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="1e5e0-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1e5e0-152">Next steps</span></span>

<span data-ttu-id="1e5e0-153">Ga te[stap 2: Controleer of de vereisten en beperkingen](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="1e5e0-153">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>
