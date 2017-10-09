---
title: aaaHow ondersteunt de virtuele machine van Azure replicatie tussen de werkzaamheden van de Azure-regio's in Azure Site Recovery?  | Microsoft Docs
description: Dit artikel bevat een overzicht van de onderdelen en de architectuur die wordt gebruikt voor het virtuele Azure-machines repliceren tussen Azure-regio's met behulp van hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="e3f09-104">Hoe werkt Azure VM-replicatie in Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="e3f09-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="e3f09-105">Dit artikel wordt beschreven Hallo-onderdelen en -processen betrokken bij repliceren en herstellen van de virtuele Azure-machines (VM's) van één regio tooanother met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="e3f09-105">This article describes hello components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region tooanother by using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="e3f09-106">Azure VM-replicatie met Hallo Site Recovery-service is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="e3f09-106">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="e3f09-107">Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e3f09-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="e3f09-108">Architectuuronderdelen</span><span class="sxs-lookup"><span data-stu-id="e3f09-108">Architectural components</span></span>

<span data-ttu-id="e3f09-109">Hallo volgende diagram toont een globaal overzicht van een virtuele machine van Azure-omgeving in een specifieke regio (in dit voorbeeld Hallo locatie VS-Oost).</span><span class="sxs-lookup"><span data-stu-id="e3f09-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="e3f09-110">In een virtuele machine van Azure-omgeving:</span><span class="sxs-lookup"><span data-stu-id="e3f09-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="e3f09-111">Apps kunnen worden uitgevoerd op virtuele machines met schijven die zijn verdeeld over de storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="e3f09-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="e3f09-112">Hallo virtuele machines kan worden opgenomen in een of meer subnetten binnen een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="e3f09-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![klant-omgeving](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="e3f09-114">Meer informatie over de implementatievereisten Hallo en vereisten op Hallo [ondersteuningsmatrix](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="e3f09-114">Learn about hello deployment prerequisites and requirements in hello [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="e3f09-115">Replicatieproces</span><span class="sxs-lookup"><span data-stu-id="e3f09-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="e3f09-116">Stap 1</span><span class="sxs-lookup"><span data-stu-id="e3f09-116">Step 1</span></span>

<span data-ttu-id="e3f09-117">Wanneer u Azure VM-replicatie in hello Azure-portal inschakelt, Hallo bronnen die in het volgende Hallo diagram en de tabel automatisch worden gemaakt in Hallo doelregio.</span><span class="sxs-lookup"><span data-stu-id="e3f09-117">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="e3f09-118">Resources worden gemaakt op basis van regio broninstellingen standaard.</span><span class="sxs-lookup"><span data-stu-id="e3f09-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="e3f09-119">Hallo-doelinstellingen zo nodig kunt u aanpassen.</span><span class="sxs-lookup"><span data-stu-id="e3f09-119">You can customize hello target settings as required.</span></span> <span data-ttu-id="e3f09-120">[Meer informatie](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="e3f09-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Stap 1 replicatieproces inschakelen](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="e3f09-122">**Resource**</span><span class="sxs-lookup"><span data-stu-id="e3f09-122">**Resource**</span></span> | <span data-ttu-id="e3f09-123">**Details**</span><span class="sxs-lookup"><span data-stu-id="e3f09-123">**Details**</span></span>
--- | ---
<span data-ttu-id="e3f09-124">**Doelresourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e3f09-124">**Target resource group**</span></span> | <span data-ttu-id="e3f09-125">Hallo resource groep toowhich gerepliceerde virtuele machines na een failover behoren.</span><span class="sxs-lookup"><span data-stu-id="e3f09-125">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="e3f09-126">**Doel virtueel netwerk**</span><span class="sxs-lookup"><span data-stu-id="e3f09-126">**Target virtual network**</span></span> | <span data-ttu-id="e3f09-127">Hallo-netwerk waarin gerepliceerde virtuele machines zich bevinden na een failover.</span><span class="sxs-lookup"><span data-stu-id="e3f09-127">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="e3f09-128">Een netwerktoewijzing wordt gemaakt tussen bron- en virtuele netwerken, en vice versa.</span><span class="sxs-lookup"><span data-stu-id="e3f09-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="e3f09-129">**Cache-opslagaccounts**</span><span class="sxs-lookup"><span data-stu-id="e3f09-129">**Cache storage accounts**</span></span> | <span data-ttu-id="e3f09-130">Voordat u wijzigingen op de bron-VM's zijn gerepliceerd toohello doel storage-account, worden ze bijgehouden en toohello cache storage-account in de doellocatie Hallo verzonden.</span><span class="sxs-lookup"><span data-stu-id="e3f09-130">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="e3f09-131">Dit zorgt ervoor minimale gevolgen voor de productie-apps die worden uitgevoerd op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e3f09-131">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="e3f09-132">**Doel storage-accounts**</span><span class="sxs-lookup"><span data-stu-id="e3f09-132">**Target storage accounts**</span></span>  | <span data-ttu-id="e3f09-133">Storage-accounts in Hallo doel toowhich Hallo locatiegegevens wordt gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="e3f09-133">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="e3f09-134">**Doel-beschikbaarheidssets**</span><span class="sxs-lookup"><span data-stu-id="e3f09-134">**Target availability sets**</span></span>  | <span data-ttu-id="e3f09-135">Beschikbaarheidssets in welke Hallo gerepliceerde virtuele machines zich bevinden na een failover.</span><span class="sxs-lookup"><span data-stu-id="e3f09-135">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="e3f09-136">Stap 2</span><span class="sxs-lookup"><span data-stu-id="e3f09-136">Step 2</span></span>

<span data-ttu-id="e3f09-137">Als replicatie is ingeschakeld, wordt automatisch Hallo Site Recovery-extensie Mobility-service op Hallo VM geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e3f09-137">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="e3f09-138">Hallo volgende gebeurt:</span><span class="sxs-lookup"><span data-stu-id="e3f09-138">hello following occurs:</span></span>

1. <span data-ttu-id="e3f09-139">Hallo VM is geregistreerd met Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e3f09-139">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="e3f09-140">Continue replicatie is geconfigureerd voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e3f09-140">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="e3f09-141">Schrijft gegevens op Hallo VM met schijven zijn continu toohello cache storage-account in de bronlocatie Hallo overgedragen.</span><span class="sxs-lookup"><span data-stu-id="e3f09-141">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Stap 2 replicatieproces inschakelen](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="e3f09-143">Site Recovery moet nooit binnenkomende verbindingen toohello VM.</span><span class="sxs-lookup"><span data-stu-id="e3f09-143">Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="e3f09-144">Hallo VM moet alleen uitgaande verbinding tooSite Recovery service-URL's of het IP-adressen, Office 365-verificatie URL's of het IP-adressen en IP-adressen van cache storage-account.</span><span class="sxs-lookup"><span data-stu-id="e3f09-144">hello VM needs only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="e3f09-145">Zie voor meer informatie, Hallo [netwerken richtlijnen voor het repliceren van virtuele machines in Azure](site-recovery-azure-to-azure-networking-guidance.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="e3f09-145">For more information, see hello [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="e3f09-146">Continue replicatie in proces</span><span class="sxs-lookup"><span data-stu-id="e3f09-146">Continuous replication process</span></span>

<span data-ttu-id="e3f09-147">Nadat u continue replicatie werkt, overgedragen schijf schrijfbewerkingen onmiddellijk zijn toohello cache storage-account.</span><span class="sxs-lookup"><span data-stu-id="e3f09-147">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="e3f09-148">Site Recovery Hallo gegevens verwerkt en verzendt het toohello doel storage-account.</span><span class="sxs-lookup"><span data-stu-id="e3f09-148">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="e3f09-149">Nadat het Hallo-gegevens zijn verwerkt, worden herstelpunten gegenereerd in Hallo doel storage-account om de paar minuten.</span><span class="sxs-lookup"><span data-stu-id="e3f09-149">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="e3f09-150">Failover-proces</span><span class="sxs-lookup"><span data-stu-id="e3f09-150">Failover process</span></span>

<span data-ttu-id="e3f09-151">Wanneer u een failover initieert, doel virtuele machines worden gemaakt in de doelresourcegroep hello, virtuele doelnetwerk, Doelsubnet Hallo en Hallo-beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="e3f09-151">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="e3f09-152">U kunt een willekeurig herstelpunt gebruiken tijdens een failover.</span><span class="sxs-lookup"><span data-stu-id="e3f09-152">During a failover, you can use any recovery point.</span></span>

![Failover-proces](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="e3f09-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3f09-154">Next steps</span></span>

- <span data-ttu-id="e3f09-155">Meer informatie over [netwerken](site-recovery-azure-to-azure-networking-guidance.md) voor replicatie van de virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="e3f09-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="e3f09-156">Ga als volgt een overzicht te[virtuele Azure-machines repliceren.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="e3f09-156">Follow a walkthrough too[replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
