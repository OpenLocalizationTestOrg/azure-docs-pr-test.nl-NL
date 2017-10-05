---
title: De netwerkkoppeling tussen twee Azure-regio's in Azure Site Recovery | Microsoft Docs
description: "Azure Site Recovery coördineert de replicatie, failovers en herstel van virtuele machines en fysieke servers. Meer informatie over failover naar Azure of een secundair datacenter."
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
ms.openlocfilehash: 9d6a806ec533259797080fbfee2c38f918ebd8a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="bbc97-104">De netwerkkoppeling tussen twee Azure-regio 's</span><span class="sxs-lookup"><span data-stu-id="bbc97-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="bbc97-105">In dit artikel wordt beschreven hoe virtuele Azure-netwerken van twee Azure-regio's met elkaar worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bbc97-105">This article describes how to map Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="bbc97-106">Netwerktoewijzing zorgt ervoor dat wanneer gerepliceerde virtuele machine wordt gemaakt in de doel-Azure-regio, wordt gemaakt op het virtuele netwerk dat is toegewezen aan het virtuele netwerk van de virtuele bronmachine.</span><span class="sxs-lookup"><span data-stu-id="bbc97-106">Network mapping ensures that when replicated virtual machine is created in the target Azure region, it is created on the virtual network that is mapped to virtual network of the source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="bbc97-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bbc97-107">Prerequisites</span></span>
<span data-ttu-id="bbc97-108">Voordat u toewijzen netwerken zeker dat u hebt gemaakt kunt [virtuele netwerken van Azure](../virtual-network/virtual-networks-overview.md) in zowel bron en doel van de Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="bbc97-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="bbc97-109">Netwerken toewijzen</span><span class="sxs-lookup"><span data-stu-id="bbc97-109">Map networks</span></span>

<span data-ttu-id="bbc97-110">Als u wilt een Azure-netwerk in een Azure-regio worden toegewezen aan een ander virtueel netwerk in een andere regio, gaat u naar Site Recovery-infrastructuur -> netwerktoewijzing (voor Azure Virtual Machines) en maak de netwerktoewijzing van een.</span><span class="sxs-lookup"><span data-stu-id="bbc97-110">To map an Azure virtual network in one Azure region to another virtual network in another region, go to Site Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="bbc97-112">In het onderstaande voorbeeld is mijn virtuele machine wordt uitgevoerd in de regio Oost-Azië, en wordt gerepliceerd naar Zuidoost-Azië.</span><span class="sxs-lookup"><span data-stu-id="bbc97-112">In the example below my virtual machine is running in East Asia region and is being replicated to Southeast Asia.</span></span>

<span data-ttu-id="bbc97-113">Selecteer de bron en doel-netwerk en klik vervolgens op OK als u wilt maken een netwerktoewijzing tussen Oost-Azië Zuidoost-Azië.</span><span class="sxs-lookup"><span data-stu-id="bbc97-113">Select the source and target network and then click OK to create a network mapping from East Asia to Southeast Asia.</span></span>

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="bbc97-115">Doe hetzelfde voor een netwerktoewijzing maken tussen Zuidoost-Azië Oost-Azië.</span><span class="sxs-lookup"><span data-stu-id="bbc97-115">Do the same thing to create a network mapping from Southeast Asia to East Asia.</span></span>  
![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="bbc97-117">Netwerkverbinding maken bij het inschakelen van replicatie</span><span class="sxs-lookup"><span data-stu-id="bbc97-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="bbc97-118">Als de netwerktoewijzing is niet uitgevoerd wanneer u een virtuele machine voor de eerste keer formulier een Azure-regio worden gerepliceerd naar een andere, kunt u doelnetwerk als onderdeel van hetzelfde proces.</span><span class="sxs-lookup"><span data-stu-id="bbc97-118">If network mapping is not done when you are replicating a virtual machine for the first time form one Azure region to another, then you can choose target network as part of the same process.</span></span> <span data-ttu-id="bbc97-119">Uit de regio van bron naar doelregio en doelregio bron regio op basis van deze selectie, maakt site Recovery-netwerkkoppelingen.</span><span class="sxs-lookup"><span data-stu-id="bbc97-119">Site Recovery creates network mappings from source region to target region and from target region to source region based on this selection.</span></span>   

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="bbc97-121">Standaard maakt Site Recovery een netwerk in de doelregio die identiek is aan het Bronnetwerk en toe te voegen '-asr' als achtervoegsel aan de naam van het bron-netwerk.</span><span class="sxs-lookup"><span data-stu-id="bbc97-121">By default, Site Recovery creates a network in the target region that is identical to the source network and by adding '-asr' as a suffix to the name of the source network.</span></span> <span data-ttu-id="bbc97-122">U kunt een bestaande netwerk door te klikken op aanpassen.</span><span class="sxs-lookup"><span data-stu-id="bbc97-122">You can choose an already created network by clicking Customize.</span></span>

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="bbc97-124">Als de netwerktoewijzing al wordt uitgevoerd, kunt u het virtuele netwerk niet wijzigen tijdens het inschakelen van replicatie.</span><span class="sxs-lookup"><span data-stu-id="bbc97-124">If the network mapping is already done, you can't change the target virtual network while enabling replication.</span></span> <span data-ttu-id="bbc97-125">Als u wilt wijzigen, bestaande netwerktoewijzing te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bbc97-125">To change it, modify existing network mapping.</span></span>  

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="bbc97-128">Als u een netwerktoewijzing van gebied-1 tot regio 2 wijzigt, zorg er dan voor dat u de netwerktoewijzing van regio 2 op regio 1 ook wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bbc97-128">If you modify a network mapping from region-1 to region-2, make sure you modify the network mapping from region-2 to region-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="bbc97-129">Selectie van subnet</span><span class="sxs-lookup"><span data-stu-id="bbc97-129">Subnet selection</span></span>
<span data-ttu-id="bbc97-130">Subnet van de virtuele doelmachine is geselecteerd op basis van de naam van het subnet van de virtuele bronmachine.</span><span class="sxs-lookup"><span data-stu-id="bbc97-130">Subnet of the target virtual machine is selected based on the name of the subnet of the source virtual machine.</span></span> <span data-ttu-id="bbc97-131">Als er een subnet met dezelfde naam als die van de virtuele bronmachine beschikbaar zijn in het doelnetwerk, is voor de virtuele doelmachine die gekozen.</span><span class="sxs-lookup"><span data-stu-id="bbc97-131">If there is a subnet of the same name as that of the source virtual machine available in the target network, then that is chosen for the target virtual machine.</span></span> <span data-ttu-id="bbc97-132">Als er geen subnet met dezelfde naam in het doelnetwerk vervolgens alfabetisch is eerste subnet gekozen als het doelsubnet.</span><span class="sxs-lookup"><span data-stu-id="bbc97-132">If there is no subnet with the same name in the target network, then alphabetically first subnet is chosen as the target subnet.</span></span> <span data-ttu-id="bbc97-133">U kunt dit subnet wijzigen door te gaan naar de berekening en netwerk-instellingen van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bbc97-133">You can modify this subnet by going to Compute and Network settings of the virtual machine.</span></span>

![Wijzigen van Subnet](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="bbc97-135">IP-adres</span><span class="sxs-lookup"><span data-stu-id="bbc97-135">IP address</span></span>

<span data-ttu-id="bbc97-136">IP-adres voor elk van de netwerkinterface van de virtuele doelmachine gekozen als volgt:</span><span class="sxs-lookup"><span data-stu-id="bbc97-136">IP address for each of the network interface of the target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="bbc97-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="bbc97-137">DHCP</span></span>
<span data-ttu-id="bbc97-138">Als de netwerkinterface van de virtuele bronmachine DHCP gebruikt, wordt de netwerkinterface van de virtuele doelmachine ook als DHCP ingesteld.</span><span class="sxs-lookup"><span data-stu-id="bbc97-138">If the network interface of the source virtual machine is using DHCP, then network interface of the target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="bbc97-139">Vaste IP-adres</span><span class="sxs-lookup"><span data-stu-id="bbc97-139">Static IP</span></span>
<span data-ttu-id="bbc97-140">Als de netwerkinterface van de virtuele bronmachine van vaste IP-adres gebruikmaakt, wordt de netwerkinterface van de virtuele doelmachine ook ingesteld op statische IP gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bbc97-140">If the network interface of the source virtual machine is using Static IP, then network interface of the target virtual machine is also set to use Static IP.</span></span> <span data-ttu-id="bbc97-141">Vaste IP-adres is als volgt kiezen:</span><span class="sxs-lookup"><span data-stu-id="bbc97-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="bbc97-142">Dezelfde adresruimte</span><span class="sxs-lookup"><span data-stu-id="bbc97-142">Same address space</span></span>

<span data-ttu-id="bbc97-143">Als het subnet van de bron en het doelsubnet hebt dezelfde adresruimte, wordt IP-adres van doel hetzelfde als het IP-adres van de netwerkinterface van de virtuele bronmachine instellen.</span><span class="sxs-lookup"><span data-stu-id="bbc97-143">If the source subnet and the target subnet have the same address space, then target IP is set same as the IP of  the network interface of the source virtual machine.</span></span> <span data-ttu-id="bbc97-144">Als dezelfde IP niet beschikbaar is, is enkele beschikbare IP ingesteld als het doel-IP.</span><span class="sxs-lookup"><span data-stu-id="bbc97-144">If same IP is not available, then some other available IP is set as the target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="bbc97-145">Andere adresruimte</span><span class="sxs-lookup"><span data-stu-id="bbc97-145">Different address space</span></span>

<span data-ttu-id="bbc97-146">Als het subnet van de bron en het doelsubnet hebt verschillende adresruimte, wordt IP-adres doel ingesteld als een beschikbare IP in het doelsubnet.</span><span class="sxs-lookup"><span data-stu-id="bbc97-146">If the source subnet and the target subnet have different address space, then target IP is set as any available IP in the target subnet.</span></span>

<span data-ttu-id="bbc97-147">U kunt het doel-IP op elke netwerkinterface wijzigen door te gaan naar berekenings- en instellingen van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bbc97-147">You can modify the target IP on each network interface by going to Compute and Network settings of the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbc97-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bbc97-148">Next steps</span></span>

- <span data-ttu-id="bbc97-149">Meer informatie over [richtlijnen voor het repliceren van virtuele Azure-machines networking](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="bbc97-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
