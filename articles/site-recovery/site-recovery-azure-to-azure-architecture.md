---
title: Hoe werkt Azure virtuele machinereplicatie tussen Azure-regio's in Azure Site Recovery?  | Microsoft Docs
description: Dit artikel bevat een overzicht van de onderdelen en de architectuur die wordt gebruikt voor het virtuele Azure-machines repliceren tussen Azure-regio's met de Azure Site Recovery-service.
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
ms.openlocfilehash: ec397eaeda963f257d1bd996f1f57189bcde17ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="3b46b-104">Hoe werkt Azure VM-replicatie in Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="3b46b-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="3b46b-105">Dit artikel wordt beschreven voor de onderdelen en -processen betrokken bij repliceren en herstellen van de virtuele Azure-machines (VM's) van de ene regio naar de andere met behulp van de [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="3b46b-105">This article describes the components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region to another by using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="3b46b-106">Azure VM-replicatie met Site Recovery-service is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="3b46b-106">Azure VM replication with the Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="3b46b-107">Eventuele opmerkingen kunt u onderaan dit artikel plaatsen of vragen stellen op het [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3b46b-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="3b46b-108">Architectuuronderdelen</span><span class="sxs-lookup"><span data-stu-id="3b46b-108">Architectural components</span></span>

<span data-ttu-id="3b46b-109">Het volgende diagram toont een globaal overzicht van een virtuele machine van Azure-omgeving in een specifieke regio (in dit voorbeeld is de locatie VS-Oost).</span><span class="sxs-lookup"><span data-stu-id="3b46b-109">The following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, the East US location).</span></span> <span data-ttu-id="3b46b-110">In een virtuele machine van Azure-omgeving:</span><span class="sxs-lookup"><span data-stu-id="3b46b-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="3b46b-111">Apps kunnen worden uitgevoerd op virtuele machines met schijven die zijn verdeeld over de storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="3b46b-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="3b46b-112">De virtuele machines kunnen worden opgenomen in een of meer subnetten binnen een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="3b46b-112">The VMs can be included in one or more subnets within a virtual network.</span></span>

![klant-omgeving](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="3b46b-114">Meer informatie over de vereisten voor implementatie en de vereisten in de [ondersteuningsmatrix](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="3b46b-114">Learn about the deployment prerequisites and requirements in the [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="3b46b-115">Replicatieproces</span><span class="sxs-lookup"><span data-stu-id="3b46b-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="3b46b-116">Stap 1</span><span class="sxs-lookup"><span data-stu-id="3b46b-116">Step 1</span></span>

<span data-ttu-id="3b46b-117">Wanneer u replicatie voor virtuele Azure-machine in de Azure portal inschakelt, worden de resources die wordt weergegeven in het volgende diagram en de tabel automatisch gemaakt in de doelregio.</span><span class="sxs-lookup"><span data-stu-id="3b46b-117">When you enable Azure VM replication in the Azure portal, the resources shown in the following diagram and table are automatically created in the target region.</span></span> <span data-ttu-id="3b46b-118">Resources worden gemaakt op basis van regio broninstellingen standaard.</span><span class="sxs-lookup"><span data-stu-id="3b46b-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="3b46b-119">U kunt de doelinstellingen zo nodig kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="3b46b-119">You can customize the target settings as required.</span></span> <span data-ttu-id="3b46b-120">[Meer informatie](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="3b46b-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Stap 1 replicatieproces inschakelen](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="3b46b-122">**Resource**</span><span class="sxs-lookup"><span data-stu-id="3b46b-122">**Resource**</span></span> | <span data-ttu-id="3b46b-123">**Details**</span><span class="sxs-lookup"><span data-stu-id="3b46b-123">**Details**</span></span>
--- | ---
<span data-ttu-id="3b46b-124">**Doelresourcegroep**</span><span class="sxs-lookup"><span data-stu-id="3b46b-124">**Target resource group**</span></span> | <span data-ttu-id="3b46b-125">De resourcegroep waartoe gerepliceerde virtuele machines na een failover behoren.</span><span class="sxs-lookup"><span data-stu-id="3b46b-125">The resource group to which replicated VMs belong after failover.</span></span>
<span data-ttu-id="3b46b-126">**Doel virtueel netwerk**</span><span class="sxs-lookup"><span data-stu-id="3b46b-126">**Target virtual network**</span></span> | <span data-ttu-id="3b46b-127">Het virtuele netwerk waarin gerepliceerde virtuele machines zich bevinden na een failover.</span><span class="sxs-lookup"><span data-stu-id="3b46b-127">The virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="3b46b-128">Een netwerktoewijzing wordt gemaakt tussen bron- en virtuele netwerken, en vice versa.</span><span class="sxs-lookup"><span data-stu-id="3b46b-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="3b46b-129">**Cache-opslagaccounts**</span><span class="sxs-lookup"><span data-stu-id="3b46b-129">**Cache storage accounts**</span></span> | <span data-ttu-id="3b46b-130">Voordat u wijzigingen op de bron-VM's worden gerepliceerd naar de doel-opslagaccount, zijn ze bijgehouden en verzonden naar het storage-account van de cache op de doellocatie.</span><span class="sxs-lookup"><span data-stu-id="3b46b-130">Before changes on source VMs are replicated to the target storage account, they are tracked and sent to the cache storage account in the target location.</span></span> <span data-ttu-id="3b46b-131">Dit zorgt ervoor minimale gevolgen voor de productie-apps die worden uitgevoerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3b46b-131">This ensures minimal impact on production apps running on the VM.</span></span>
<span data-ttu-id="3b46b-132">**Doel storage-accounts**</span><span class="sxs-lookup"><span data-stu-id="3b46b-132">**Target storage accounts**</span></span>  | <span data-ttu-id="3b46b-133">Storage-accounts in de doellocatie waarnaar de gegevens worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="3b46b-133">Storage accounts in the target location to which the data is replicated.</span></span>
<span data-ttu-id="3b46b-134">**Doel-beschikbaarheidssets**</span><span class="sxs-lookup"><span data-stu-id="3b46b-134">**Target availability sets**</span></span>  | <span data-ttu-id="3b46b-135">Beschikbaarheidssets in die de gerepliceerde virtuele machines zich na een failover.</span><span class="sxs-lookup"><span data-stu-id="3b46b-135">Availability sets in which the replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="3b46b-136">Stap 2</span><span class="sxs-lookup"><span data-stu-id="3b46b-136">Step 2</span></span>

<span data-ttu-id="3b46b-137">Als replicatie is ingeschakeld, wordt de Site Recovery-extensie Mobility-service wordt automatisch geïnstalleerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3b46b-137">As replication is enabled, the Site Recovery extension Mobility service is automatically installed on the VM.</span></span> <span data-ttu-id="3b46b-138">Het volgende gebeurt:</span><span class="sxs-lookup"><span data-stu-id="3b46b-138">The following occurs:</span></span>

1. <span data-ttu-id="3b46b-139">De virtuele machine is geregistreerd met Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3b46b-139">The VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="3b46b-140">Continue replicatie is geconfigureerd voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3b46b-140">Continuous replication is configured for the VM.</span></span> <span data-ttu-id="3b46b-141">Gegevens van schrijfbewerkingen op de VM-schijven worden continu overgebracht naar het storage-account van de cache op de bronlocatie.</span><span class="sxs-lookup"><span data-stu-id="3b46b-141">Data writes on the VM disks are continuously transferred to the cache storage account in the source location.</span></span>

   ![Stap 2 replicatieproces inschakelen](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="3b46b-143">Site Recovery moet nooit binnenkomende verbinding hebben met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3b46b-143">Site Recovery never needs inbound connectivity to the VM.</span></span> <span data-ttu-id="3b46b-144">De virtuele machine moet alleen uitgaande verbinding met Site Recovery-service-URL's of het IP-adressen, Office 365-verificatie URL's of het IP-adressen en IP-adressen van cache storage-account.</span><span class="sxs-lookup"><span data-stu-id="3b46b-144">The VM needs only outbound connectivity to Site Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="3b46b-145">Zie voor meer informatie de [netwerken richtlijnen voor het repliceren van virtuele machines in Azure](site-recovery-azure-to-azure-networking-guidance.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="3b46b-145">For more information, see the [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="3b46b-146">Continue replicatie in proces</span><span class="sxs-lookup"><span data-stu-id="3b46b-146">Continuous replication process</span></span>

<span data-ttu-id="3b46b-147">Nadat u continue replicatie werkt, worden schrijfbewerkingen onmiddellijk overgebracht naar het opslagaccount van de cache.</span><span class="sxs-lookup"><span data-stu-id="3b46b-147">After continuous replication is working, disk writes are immediately transferred to the cache storage account.</span></span> <span data-ttu-id="3b46b-148">Site Recovery de gegevens worden verwerkt en verzonden naar de doel-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3b46b-148">Site Recovery processes the data and sends it to the target storage account.</span></span> <span data-ttu-id="3b46b-149">Nadat de gegevens zijn verwerkt, worden herstelpunten gegenereerd in de doel-storage-account om de paar minuten.</span><span class="sxs-lookup"><span data-stu-id="3b46b-149">After the data is processed, recovery points are generated in the target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="3b46b-150">Failover-proces</span><span class="sxs-lookup"><span data-stu-id="3b46b-150">Failover process</span></span>

<span data-ttu-id="3b46b-151">Wanneer u een failover initieert, de virtuele machines worden gemaakt in de doelresourcegroep, doel virtueel netwerk, Doelsubnet, en de beschikbaarheid van het doel is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3b46b-151">When you initiate a failover, the VMs are created in the target resource group, target virtual network, target subnet, and the target availability set.</span></span> <span data-ttu-id="3b46b-152">U kunt een willekeurig herstelpunt gebruiken tijdens een failover.</span><span class="sxs-lookup"><span data-stu-id="3b46b-152">During a failover, you can use any recovery point.</span></span>

![Failover-proces](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="3b46b-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3b46b-154">Next steps</span></span>

- <span data-ttu-id="3b46b-155">Meer informatie over [netwerken](site-recovery-azure-to-azure-networking-guidance.md) voor replicatie van de virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="3b46b-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="3b46b-156">Ga als volgt een overzicht te [virtuele Azure-machines repliceren.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="3b46b-156">Follow a walkthrough to [replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
