---
title: aaaNetwork toewijzing tussen twee Azure-regio's in Azure Site Recovery | Microsoft Docs
description: "Azure Site Recovery coördineert Hallo replicatie, failovers en herstel van virtuele machines en fysieke servers. Meer informatie over failover tooAzure of een secundair datacenter."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="ec76b-104">De netwerkkoppeling tussen twee Azure-regio 's</span><span class="sxs-lookup"><span data-stu-id="ec76b-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="ec76b-105">Dit artikel wordt beschreven hoe toomap Azure virtuele netwerken van twee Azure-regio's met elkaar.</span><span class="sxs-lookup"><span data-stu-id="ec76b-105">This article describes how toomap Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="ec76b-106">Netwerktoewijzing zorgt ervoor dat wanneer gerepliceerde virtuele machine wordt gemaakt in Hallo doel-Azure-regio, wordt gemaakt op Hallo virtueel netwerk dat is toegewezen toovirtual netwerk van de virtuele bronmachine Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec76b-106">Network mapping ensures that when replicated virtual machine is created in hello target Azure region, it is created on hello virtual network that is mapped toovirtual network of hello source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="ec76b-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ec76b-107">Prerequisites</span></span>
<span data-ttu-id="ec76b-108">Voordat u toewijzen netwerken zeker dat u hebt gemaakt kunt [virtuele netwerken van Azure](../virtual-network/virtual-networks-overview.md) in zowel bron en doel van de Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="ec76b-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="ec76b-109">Netwerken toewijzen</span><span class="sxs-lookup"><span data-stu-id="ec76b-109">Map networks</span></span>

<span data-ttu-id="ec76b-110">een Azure-netwerk in een Azure-regio tooanother virtueel netwerk in een andere regio, Ga tooSite Recovery-infrastructuur toomap -> netwerktoewijzing (voor Azure Virtual Machines) en maak de netwerktoewijzing van een.</span><span class="sxs-lookup"><span data-stu-id="ec76b-110">toomap an Azure virtual network in one Azure region tooanother virtual network in another region, go tooSite Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="ec76b-112">In het volgende voorbeeld wordt mijn virtuele machine wordt uitgevoerd in de Oost-Azië regio en wordt gerepliceerd in Hallo tooSoutheast Azië.</span><span class="sxs-lookup"><span data-stu-id="ec76b-112">In hello example below my virtual machine is running in East Asia region and is being replicated tooSoutheast Asia.</span></span>

<span data-ttu-id="ec76b-113">Hallo-bron en doel netwerk selecteren en klik op OK toocreate een netwerktoewijzing van Oost-Azië tooSoutheast Azië.</span><span class="sxs-lookup"><span data-stu-id="ec76b-113">Select hello source and target network and then click OK toocreate a network mapping from East Asia tooSoutheast Asia.</span></span>

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="ec76b-115">Hallo dezelfde ding toocreate een netwerktoewijzing van Zuidoost-Azië tooEast Azië.</span><span class="sxs-lookup"><span data-stu-id="ec76b-115">Do hello same thing toocreate a network mapping from Southeast Asia tooEast Asia.</span></span>  
![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="ec76b-117">Netwerkverbinding maken bij het inschakelen van replicatie</span><span class="sxs-lookup"><span data-stu-id="ec76b-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="ec76b-118">Als de netwerktoewijzing is niet uitgevoerd wanneer u een virtuele machine voor Hallo eerste tijd formulier een Azure-regio tooanother repliceert, kunt u doelnetwerk als onderdeel van Hallo hetzelfde proces.</span><span class="sxs-lookup"><span data-stu-id="ec76b-118">If network mapping is not done when you are replicating a virtual machine for hello first time form one Azure region tooanother, then you can choose target network as part of hello same process.</span></span> <span data-ttu-id="ec76b-119">Uit bron regio tootarget regio en regio toosource doelregio op basis van deze selectie, maakt site Recovery-netwerkkoppelingen.</span><span class="sxs-lookup"><span data-stu-id="ec76b-119">Site Recovery creates network mappings from source region tootarget region and from target region toosource region based on this selection.</span></span>   

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="ec76b-121">Site Recovery maakt een netwerk in Hallo doelregio die het Bronnetwerk identieke toohello en door toe te voegen '-asr' als de naam van een achtervoegsel toohello van Hallo Bronnetwerk.</span><span class="sxs-lookup"><span data-stu-id="ec76b-121">By default, Site Recovery creates a network in hello target region that is identical toohello source network and by adding '-asr' as a suffix toohello name of hello source network.</span></span> <span data-ttu-id="ec76b-122">U kunt een bestaande netwerk door te klikken op aanpassen.</span><span class="sxs-lookup"><span data-stu-id="ec76b-122">You can choose an already created network by clicking Customize.</span></span>

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="ec76b-124">Als de netwerktoewijzing Hallo al wordt uitgevoerd, kunt u Hallo doel virtueel netwerk niet wijzigen tijdens het inschakelen van replicatie.</span><span class="sxs-lookup"><span data-stu-id="ec76b-124">If hello network mapping is already done, you can't change hello target virtual network while enabling replication.</span></span> <span data-ttu-id="ec76b-125">toochange, bestaande netwerktoewijzing wijzigt.</span><span class="sxs-lookup"><span data-stu-id="ec76b-125">toochange it, modify existing network mapping.</span></span>  

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="ec76b-128">Als u een netwerktoewijzing vanuit tooregion regio-1-2 wijzigt, zorg er dan voor dat u de netwerktoewijzing Hallo van regio-2-tooregion-ook 1 wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ec76b-128">If you modify a network mapping from region-1 tooregion-2, make sure you modify hello network mapping from region-2 tooregion-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="ec76b-129">Selectie van subnet</span><span class="sxs-lookup"><span data-stu-id="ec76b-129">Subnet selection</span></span>
<span data-ttu-id="ec76b-130">Subnet van de virtuele doelmachine Hallo is geselecteerd op basis van naam van het subnet van de virtuele bronmachine Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="ec76b-130">Subnet of hello target virtual machine is selected based on hello name of hello subnet of hello source virtual machine.</span></span> <span data-ttu-id="ec76b-131">Als er een subnet van Hallo wordt dezelfde naam als die van Hallo virtuele bronmachine beschikbaar zijn in het doelnetwerk hello, en vervolgens die voor de virtuele doelmachine Hallo is gekozen.</span><span class="sxs-lookup"><span data-stu-id="ec76b-131">If there is a subnet of hello same name as that of hello source virtual machine available in hello target network, then that is chosen for hello target virtual machine.</span></span> <span data-ttu-id="ec76b-132">Als er geen subnet met hello wordt dezelfde naam in het doelnetwerk hello, en vervolgens alfabetisch eerste subnet is gekozen als Hallo Doelsubnet.</span><span class="sxs-lookup"><span data-stu-id="ec76b-132">If there is no subnet with hello same name in hello target network, then alphabetically first subnet is chosen as hello target subnet.</span></span> <span data-ttu-id="ec76b-133">U kunt dit subnet wijzigen door te gaan tooCompute en de netwerkinstellingen van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ec76b-133">You can modify this subnet by going tooCompute and Network settings of hello virtual machine.</span></span>

![Wijzigen van Subnet](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="ec76b-135">IP-adres</span><span class="sxs-lookup"><span data-stu-id="ec76b-135">IP address</span></span>

<span data-ttu-id="ec76b-136">IP-adres voor elk van de netwerkinterface Hallo van de virtuele doelmachine Hallo gekozen als volgt:</span><span class="sxs-lookup"><span data-stu-id="ec76b-136">IP address for each of hello network interface of hello target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="ec76b-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="ec76b-137">DHCP</span></span>
<span data-ttu-id="ec76b-138">Als het Hallo-netwerkinterface van de virtuele bronmachine hello wordt DHCP gebruikt, vervolgens netwerkinterface van de virtuele doelmachine Hallo ook ingesteld als DHCP.</span><span class="sxs-lookup"><span data-stu-id="ec76b-138">If hello network interface of hello source virtual machine is using DHCP, then network interface of hello target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="ec76b-139">Vaste IP-adres</span><span class="sxs-lookup"><span data-stu-id="ec76b-139">Static IP</span></span>
<span data-ttu-id="ec76b-140">Als Hallo-netwerkinterface van de virtuele bronmachine Hallo van vaste IP-adres gebruikmaakt, wordt klikt u vervolgens netwerkinterface van de virtuele doelmachine hello ook ingesteld toouse vaste IP-adres.</span><span class="sxs-lookup"><span data-stu-id="ec76b-140">If hello network interface of hello source virtual machine is using Static IP, then network interface of hello target virtual machine is also set toouse Static IP.</span></span> <span data-ttu-id="ec76b-141">Vaste IP-adres is als volgt kiezen:</span><span class="sxs-lookup"><span data-stu-id="ec76b-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="ec76b-142">Dezelfde adresruimte</span><span class="sxs-lookup"><span data-stu-id="ec76b-142">Same address space</span></span>

<span data-ttu-id="ec76b-143">Als Hallo bron subnet en Doelsubnet Hallo Hallo-dezelfde adresruimte, wordt IP-adres doel hetzelfde als Hallo IP-adres van de netwerkinterface Hallo van de virtuele bronmachine Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ec76b-143">If hello source subnet and hello target subnet have hello same address space, then target IP is set same as hello IP of  hello network interface of hello source virtual machine.</span></span> <span data-ttu-id="ec76b-144">Als dezelfde IP niet beschikbaar is, is sommige andere beschikbare IP ingesteld als IP-adres Hallo-doel.</span><span class="sxs-lookup"><span data-stu-id="ec76b-144">If same IP is not available, then some other available IP is set as hello target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="ec76b-145">Andere adresruimte</span><span class="sxs-lookup"><span data-stu-id="ec76b-145">Different address space</span></span>

<span data-ttu-id="ec76b-146">Als Hallo bron subnet en Hallo Doelsubnet hebt verschillende adresruimte, is de doel-IP als een beschikbare IP in het doelsubnet Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ec76b-146">If hello source subnet and hello target subnet have different address space, then target IP is set as any available IP in hello target subnet.</span></span>

<span data-ttu-id="ec76b-147">U kunt Hallo doel-IP-adres op elke netwerkinterface wijzigen door te gaan tooCompute en de netwerkinstellingen van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ec76b-147">You can modify hello target IP on each network interface by going tooCompute and Network settings of hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec76b-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ec76b-148">Next steps</span></span>

- <span data-ttu-id="ec76b-149">Meer informatie over [richtlijnen voor het repliceren van virtuele Azure-machines networking](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="ec76b-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
