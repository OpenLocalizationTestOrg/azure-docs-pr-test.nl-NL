---
title: Problemen met routes - PowerShell | Microsoft Docs
description: Informatie over het oplossen van problemen met routes in het Azure Resource Manager-implementatiemodel met Azure PowerShell.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 141e3c571d744470fd07e99538b6e38d4144e8d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="60e20-103">Problemen oplossen met Azure PowerShell routes</span><span class="sxs-lookup"><span data-stu-id="60e20-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60e20-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="60e20-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="60e20-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60e20-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="60e20-106">Als u ondervindt problemen met de netwerkverbinding naar of van uw Azure-virtuele Machine (VM), routes mogelijk van invloed op uw verkeersstromen VM.</span><span class="sxs-lookup"><span data-stu-id="60e20-106">If you are experiencing network connectivity issues to or from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="60e20-107">Dit artikel bevat een overzicht van mogelijkheden voor routes om op te lossen verdere diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="60e20-107">This article provides an overview of diagnostics capabilities for routes to help troubleshoot further.</span></span>

<span data-ttu-id="60e20-108">Routetabellen zijn gekoppeld aan de subnets en effectieve zijn op alle netwerkinterfaces (NIC) in dat subnet.</span><span class="sxs-lookup"><span data-stu-id="60e20-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="60e20-109">De volgende soorten routes kunnen worden toegepast op elke netwerkinterface:</span><span class="sxs-lookup"><span data-stu-id="60e20-109">The following types of routes can be applied to each network interface:</span></span>

* <span data-ttu-id="60e20-110">**Systeemroutes:** elk subnet dat is gemaakt in een Azure-netwerk (VNet) heeft standaard route systeemtabellen waarmee lokale VNet-verkeer, lokale-verkeer via de VPN-gateways en internetverkeer.</span><span class="sxs-lookup"><span data-stu-id="60e20-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="60e20-111">Systeemroutes ook aanwezig zijn voor VNets peer is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="60e20-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="60e20-112">**BGP-routes:** doorgegeven aan netwerkinterfaces via ExpressRoute of site-naar-site VPN-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="60e20-112">**BGP routes:** Propagated to network interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="60e20-113">Meer informatie over BGP-routering door het lezen van de [BGP met VPN-gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) en [overzicht van ExpressRoute](../expressroute/expressroute-introduction.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="60e20-113">Learn more about BGP routing by reading the [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="60e20-114">**Gebruiker gedefinieerde routes (UDR):** als u virtuele netwerkapparaten of zijn geforceerde tunneling verkeer naar een on-premises netwerk via een site-naar-site VPN, wellicht hebt u gebruiker gedefinieerde routes (udr's) die zijn gekoppeld aan de routetabel voor subnet.</span><span class="sxs-lookup"><span data-stu-id="60e20-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic to an on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="60e20-115">Als u niet bekend met udr's bent, leest u de [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md#user-defined-routes) artikel.</span><span class="sxs-lookup"><span data-stu-id="60e20-115">If you're not familiar with UDRs, read the [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="60e20-116">Met de verschillende routes die aan een netwerkinterface kunnen worden toegepast, kan het lastig zijn om te bepalen welke cumulatieve routes effectieve zijn.</span><span class="sxs-lookup"><span data-stu-id="60e20-116">With the various routes that can be applied to a network interface, it can be difficult to determine which aggregate routes are effective.</span></span> <span data-ttu-id="60e20-117">U kunt de effectieve routes voor een netwerkinterface voor het oplossen van VM-netwerkverbinding, bekijken in het Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="60e20-117">To help troubleshoot VM network connectivity, you can view all the effective routes for a network interface in the Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="60e20-118">Problemen met VM-netwerkverkeer met effectieve Routes</span><span class="sxs-lookup"><span data-stu-id="60e20-118">Using Effective Routes to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="60e20-119">In dit artikel wordt het volgende scenario als voorbeeld ter illustratie van de effectieve routes voor een netwerkinterface oplossen:</span><span class="sxs-lookup"><span data-stu-id="60e20-119">This article uses the following scenario as an example to illustrate how to troubleshoot the effective routes for a network interface:</span></span>

<span data-ttu-id="60e20-120">Een virtuele machine (*VM1*) is verbonden met het VNet (*VNet1*, voorvoegsel: 10.9.0.0/16) geen verbinding maken met een VM(VM3) in een nieuw peered VNet (*VNet3*, 10.10.0.0/16 voorvoegsel).</span><span class="sxs-lookup"><span data-stu-id="60e20-120">A VM (*VM1*) connected to the VNet (*VNet1*, prefix: 10.9.0.0/16) fails to connect to a VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="60e20-121">Er zijn geen udr's of BGP-routes aan netwerkinterface VM1 NIC1 verbonden met de virtuele machine is toegepast, alleen de systeemroutes van het worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="60e20-121">There are no UDRs or BGP routes applied to VM1-NIC1 network interface connected to the VM, only system routes are applied.</span></span>

<span data-ttu-id="60e20-122">In dit artikel wordt uitgelegd hoe de oorzaak van de verbindingsfout met van effectieve routes mogelijkheid in Azure Resource Management-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="60e20-122">This article explains how to determine the cause of the connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="60e20-123">Terwijl het voorbeeld alleen de systeemroutes van het wordt, kunnen dezelfde stappen om te bepalen van binnenkomende en uitgaande verbindingsfouten via een routetype worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="60e20-123">While the example uses only system routes, the same steps can be used to determine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="60e20-124">Als uw virtuele machine meer dan één NIC die is gekoppeld heeft, controleert u effectieve routes voor elk van de NIC's voor het vaststellen van problemen met de netwerkverbinding naar en van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="60e20-124">If your VM has more than one NIC attached, check effective routes for each of the NICs to diagnose network connectivity issues to and from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="60e20-125">De effectieve routes weergeven voor een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="60e20-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="60e20-126">Overzicht van de cumulatieve routes die worden toegepast op een virtuele machine, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="60e20-126">To see the aggregate routes that are applied to a VM, complete the following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="60e20-127">De effectieve routes weergeven voor een netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="60e20-127">View effective routes for a network interface</span></span>
<span data-ttu-id="60e20-128">Overzicht van de cumulatieve routes die worden toegepast op een netwerkinterface, de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="60e20-128">To see the aggregate routes that are applied to a network interface, complete the following steps:</span></span>

1. <span data-ttu-id="60e20-129">Start een Azure PowerShell-sessie en meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="60e20-129">Start an Azure PowerShell session and login to Azure.</span></span> <span data-ttu-id="60e20-130">Als u niet bekend met Azure PowerShell bent, leest u de [installeren en configureren van Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="60e20-130">If you’re not familiar with Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="60e20-131">De volgende opdracht retourneert alle routes die worden toegepast op een netwerkinterface met de naam *VM1 NIC1* in de resourcegroep *RG1*.</span><span class="sxs-lookup"><span data-stu-id="60e20-131">The following command returns all routes applied to a network interface named *VM1-NIC1* in the resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="60e20-132">Als u de naam van een netwerkinterface niet weet, typ de volgende opdracht voor het ophalen van de namen van alle netwerkinterfaces in een group.* resource</span><span class="sxs-lookup"><span data-stu-id="60e20-132">If you don’t know the name of a network interface, type the following command to retrieve the names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="60e20-133">De volgende uitvoer lijkt op de uitvoer voor elke toegepast op het subnet dat de NIC is verbonden met route:</span><span class="sxs-lookup"><span data-stu-id="60e20-133">The following output looks similar to the output for each route applied to the subnet the NIC is connected to:</span></span>
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   <span data-ttu-id="60e20-134">U ziet het volgende in de uitvoer:</span><span class="sxs-lookup"><span data-stu-id="60e20-134">Notice the following in the output:</span></span>
   
   * <span data-ttu-id="60e20-135">**Naam**: naam van de effectieve route mag niet leeg zijn, tenzij expliciet is opgegeven voor de gebruiker gedefinieerde routes.</span><span class="sxs-lookup"><span data-stu-id="60e20-135">**Name**: Name of the effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="60e20-136">**Status**: geeft de status van de effectieve route.</span><span class="sxs-lookup"><span data-stu-id="60e20-136">**State**: Indicates state of the effective route.</span></span> <span data-ttu-id="60e20-137">Mogelijke waarden zijn 'Active' of 'Ongeldig'</span><span class="sxs-lookup"><span data-stu-id="60e20-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="60e20-138">**AddressPrefixes**: Hiermee geeft u het adresvoorvoegsel van de effectieve route in CIDR-notatie.</span><span class="sxs-lookup"><span data-stu-id="60e20-138">**AddressPrefixes**: Specifies the address prefix of the effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="60e20-139">**nextHopType**: Hiermee geeft u de volgende hop voor de opgegeven route.</span><span class="sxs-lookup"><span data-stu-id="60e20-139">**nextHopType**: Indicates the next hop for the given route.</span></span> <span data-ttu-id="60e20-140">Mogelijke waarden zijn *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, of *Null*.</span><span class="sxs-lookup"><span data-stu-id="60e20-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="60e20-141">Een waarde van *Null* voor **nextHopType** een UDR kan duiden op een ongeldige route.</span><span class="sxs-lookup"><span data-stu-id="60e20-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="60e20-142">Bijvoorbeeld, als **nextHopType** is *VirtualAppliance* en het netwerk van een virtueel apparaat VM niet in een status ingericht/uitvoeren is.</span><span class="sxs-lookup"><span data-stu-id="60e20-142">For example, if **nextHopType** is *VirtualAppliance* and the network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="60e20-143">Als **nextHopType** is *VPNGateway* en er is geen gateway ingericht/uitvoeren in het opgegeven VNet de route ongeldig geworden.</span><span class="sxs-lookup"><span data-stu-id="60e20-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in the given VNet, the route may become invalid.</span></span>
   * <span data-ttu-id="60e20-144">**NextHopIpAddress**: Hiermee geeft u het IP-adres van de volgende hop van de effectieve route.</span><span class="sxs-lookup"><span data-stu-id="60e20-144">**NextHopIpAddress**: Specifies the IP address of the next hop of the effective route.</span></span>
   
   <span data-ttu-id="60e20-145">De volgende opdracht retourneert de routes in een eenvoudiger tabel weergeven:</span><span class="sxs-lookup"><span data-stu-id="60e20-145">The following command returns the routes in an easier to view table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="60e20-146">De volgende uitvoer, is enkele van de uitvoer ontvangen voor het scenario zoals eerder beschreven:</span><span class="sxs-lookup"><span data-stu-id="60e20-146">The following output is some of the output received for the scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="60e20-147">Er is geen route worden vermeld om het *WestUS VNet3* VNet (10.10.0.0/16)** van het voorvoegsel *WestUS VNet1* (voorvoegsel 10.9.0.0/16) in de uitvoer van de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="60e20-147">There is no route listed to the *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in the output from the previous step.</span></span> <span data-ttu-id="60e20-148">Zoals u in de volgende afbeelding, de VNet-peering te koppelen met de *WestUS VNet3* VNet is in de *verbroken* status.</span><span class="sxs-lookup"><span data-stu-id="60e20-148">As shown in the following picture, the VNet peering link with the *WestUS-VNet3* VNet is in the *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="60e20-149">De koppeling in twee richtingen voor de peering verbroken wordt, waarin wordt uitgelegd waarom VM1 kan geen verbinding maken met VM3 in de *WestUS VNet3* VNet.</span><span class="sxs-lookup"><span data-stu-id="60e20-149">The bi-directional link for the peering is broken, which explains why VM1 could not connect to VM3 in the *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="60e20-150">Instellen van een bidirectionele VNet-peeringkoppeling opnieuw voor *WestUS VNet1* en *WestUS VNet3* VNets.</span><span class="sxs-lookup"><span data-stu-id="60e20-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="60e20-151">Hier volgt de uitvoer die wordt geretourneerd nadat de VNet-peering koppeling correct is ingesteld:</span><span class="sxs-lookup"><span data-stu-id="60e20-151">The output returned after the VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="60e20-152">Zodra u hebt vastgesteld dat het probleem, u kunt toevoegen, verwijderen, of wijzig routes en routetabellen.</span><span class="sxs-lookup"><span data-stu-id="60e20-152">Once you determine the issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="60e20-153">Typ de volgende opdracht om een lijst weer van de opdrachten om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="60e20-153">Type the following command to see a list of the commands used to do so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="60e20-154">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="60e20-154">Considerations</span></span>
<span data-ttu-id="60e20-155">Een aantal dingen rekening moet houden bij het controleren van de lijst met routes geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="60e20-155">A few things to keep in mind when reviewing the list of routes returned:</span></span>

* <span data-ttu-id="60e20-156">Routering is gebaseerd op langste voorvoegsel overeen (LPM) tussen udr's, systeem- en BGP-routes.</span><span class="sxs-lookup"><span data-stu-id="60e20-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="60e20-157">Als er meer dan één route met dezelfde overeenkomende LPM is, klikt u vervolgens een route geselecteerd op basis van de oorsprong in de volgende volgorde:</span><span class="sxs-lookup"><span data-stu-id="60e20-157">If there is more than one route with the same LPM match, then a route is selected based on its origin in the following order:</span></span>
  
  * <span data-ttu-id="60e20-158">Gebruiker gedefinieerde route</span><span class="sxs-lookup"><span data-stu-id="60e20-158">User-defined route</span></span>
  * <span data-ttu-id="60e20-159">BGP-route</span><span class="sxs-lookup"><span data-stu-id="60e20-159">BGP route</span></span>
  * <span data-ttu-id="60e20-160">Systeemroute (standaard)</span><span class="sxs-lookup"><span data-stu-id="60e20-160">System (Default) route</span></span>
    
    <span data-ttu-id="60e20-161">U kunt alleen effectieve routes die overeenkomende LPM op basis van alle routes in de beschikbaar zijn met effectieve routes zien.</span><span class="sxs-lookup"><span data-stu-id="60e20-161">With effective routes, you can only see effective routes that are LPM match based on all the availble routes.</span></span> <span data-ttu-id="60e20-162">Door te laten zien hoe de routes daadwerkelijk wordt geëvalueerd voor een bepaalde NIC, hierdoor veel eenvoudiger om op te lossen specifieke routes die mogelijk van invloed op de connectiviteit van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="60e20-162">By showing how the routes are actually evaluated for a given NIC, this makes it a lot easier to troubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="60e20-163">Als u udr's hebt en verkeer naar een virtueel apparaat voor netwerk (NVA) met verzendt *VirtualAppliance* als **nextHopType**, zorg dat doorsturen via IP is ingeschakeld op de ontvangst van het verkeer NVA of pakketten verloren gaan.</span><span class="sxs-lookup"><span data-stu-id="60e20-163">If you have UDRs and are sending traffic to a network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on the NVA receiving the traffic or packets are dropped.</span></span> 
* <span data-ttu-id="60e20-164">Als geforceerde tunneling is ingeschakeld, worden alle uitgaand internetverkeer wordt gerouteerd naar on-premises.</span><span class="sxs-lookup"><span data-stu-id="60e20-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed to on-premises.</span></span> <span data-ttu-id="60e20-165">RDP/SSH van Internet naar uw virtuele machine werkt mogelijk niet met deze instelling kan, afhankelijk van hoe deze verkeer in de on-premises worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="60e20-165">RDP/SSH from Internet to your VM may not work with this setting, depending on how the on-premises handles this traffic.</span></span> 
  <span data-ttu-id="60e20-166">Geforceerde tunneling kan worden ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="60e20-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="60e20-167">Als u site-naar-site VPN, door een door de gebruiker opgegeven routes (UDR) met nextHopType als VPN-Gateway</span><span class="sxs-lookup"><span data-stu-id="60e20-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="60e20-168">Als een standaardroute wordt geadverteerd via BGP</span><span class="sxs-lookup"><span data-stu-id="60e20-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="60e20-169">Voor VNet-peering verkeer correct te laten werken, een systeemroute met **nextHopType** *VNetPeering* voor het peered VNet-voorvoegsel bereik moet bestaan.</span><span class="sxs-lookup"><span data-stu-id="60e20-169">For VNet peering traffic to work correctly, a system route with **nextHopType** *VNetPeering* must exist for the peered VNet’s prefix range.</span></span> <span data-ttu-id="60e20-170">Als deze route bestaat niet en de VNet-peering koppeling OK lijkt:</span><span class="sxs-lookup"><span data-stu-id="60e20-170">If such a route doesn’t exist and the VNet peering link looks OK:</span></span>
  * <span data-ttu-id="60e20-171">Wacht een paar seconden en probeer het opnieuw als het een nieuw opgezette peeringkoppeling.</span><span class="sxs-lookup"><span data-stu-id="60e20-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="60e20-172">Tijd tot tijd duurt langer doorgeven routes naar alle netwerkinterfaces in een subnet.</span><span class="sxs-lookup"><span data-stu-id="60e20-172">It occasionally takes longer to propagate routes to all the network interfaces in a subnet.</span></span>
  * <span data-ttu-id="60e20-173">Netwerkbeveiligingsgroep (NSG) regels mogelijk van invloed op de verkeersstromen.</span><span class="sxs-lookup"><span data-stu-id="60e20-173">Network Security Group (NSG) rules may be impacting the traffic flows.</span></span> <span data-ttu-id="60e20-174">Zie voor meer informatie de [Netwerkbeveiligingsgroepen oplossen](virtual-network-nsg-troubleshoot-powershell.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="60e20-174">For more information, see the [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

