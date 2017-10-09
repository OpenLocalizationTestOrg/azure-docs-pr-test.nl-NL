---
title: aaaTroubleshoot-routes - PowerShell | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot routeert hello Azure Resource Manager-implementatiemodel met Azure PowerShell.
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
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="fb603-103">Problemen oplossen met Azure PowerShell routes</span><span class="sxs-lookup"><span data-stu-id="fb603-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb603-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fb603-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="fb603-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb603-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="fb603-106">Als u ondervindt network connectivity problemen tooor van uw Azure-virtuele Machine (VM), routes mogelijk van invloed op uw verkeersstromen VM.</span><span class="sxs-lookup"><span data-stu-id="fb603-106">If you are experiencing network connectivity issues tooor from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="fb603-107">Dit artikel bevat een overzicht van diagnostische gegevens mogelijkheden voor routes toohelp probleem verder oplossen.</span><span class="sxs-lookup"><span data-stu-id="fb603-107">This article provides an overview of diagnostics capabilities for routes toohelp troubleshoot further.</span></span>

<span data-ttu-id="fb603-108">Routetabellen zijn gekoppeld aan de subnets en effectieve zijn op alle netwerkinterfaces (NIC) in dat subnet.</span><span class="sxs-lookup"><span data-stu-id="fb603-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="fb603-109">Hallo volgende typen routes kan netwerkinterface toegepaste tooeach zijn:</span><span class="sxs-lookup"><span data-stu-id="fb603-109">hello following types of routes can be applied tooeach network interface:</span></span>

* <span data-ttu-id="fb603-110">**Systeemroutes:** elk subnet dat is gemaakt in een Azure-netwerk (VNet) heeft standaard route systeemtabellen waarmee lokale VNet-verkeer, lokale-verkeer via de VPN-gateways en internetverkeer.</span><span class="sxs-lookup"><span data-stu-id="fb603-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="fb603-111">Systeemroutes ook aanwezig zijn voor VNets peer is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="fb603-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="fb603-112">**BGP-routes:** doorgegeven toonetwork interfaces via ExpressRoute of site-naar-site VPN-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="fb603-112">**BGP routes:** Propagated toonetwork interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="fb603-113">Meer informatie over BGP-routering door te lezen Hallo [BGP met VPN-gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) en [overzicht van ExpressRoute](../expressroute/expressroute-introduction.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="fb603-113">Learn more about BGP routing by reading hello [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="fb603-114">**Gebruiker gedefinieerde routes (UDR):** als u virtuele netwerkapparaten gebruikt of worden geforceerde tunneling verkeer tooan on-premises netwerk via een site-naar-site VPN, wellicht hebt u gebruiker gedefinieerde routes (udr's) die zijn gekoppeld aan de routetabel voor subnet.</span><span class="sxs-lookup"><span data-stu-id="fb603-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic tooan on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="fb603-115">Als u niet bekend met udr's bent, leest u Hallo [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md#user-defined-routes) artikel.</span><span class="sxs-lookup"><span data-stu-id="fb603-115">If you're not familiar with UDRs, read hello [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="fb603-116">Met Hallo verschillende routes die toegepast tooa netwerkinterface worden kunnen, kan het zijn moeilijk toodetermine welke cumulatieve routes geldig zijn.</span><span class="sxs-lookup"><span data-stu-id="fb603-116">With hello various routes that can be applied tooa network interface, it can be difficult toodetermine which aggregate routes are effective.</span></span> <span data-ttu-id="fb603-117">toohelp VM-netwerkverbinding oplossen, kunt u alle Hallo effectieve routes voor een netwerkinterface weergeven in hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="fb603-117">toohelp troubleshoot VM network connectivity, you can view all hello effective routes for a network interface in hello Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="fb603-118">Met behulp van effectieve Routes tootroubleshoot VM-netwerkverkeer</span><span class="sxs-lookup"><span data-stu-id="fb603-118">Using Effective Routes tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="fb603-119">In dit artikel maakt gebruik van Hallo scenario als een voorbeeld tooillustrate hoe tootroubleshoot Hallo effectief voor een netwerkinterface routeert te volgen:</span><span class="sxs-lookup"><span data-stu-id="fb603-119">This article uses hello following scenario as an example tooillustrate how tootroubleshoot hello effective routes for a network interface:</span></span>

<span data-ttu-id="fb603-120">Een virtuele machine (*VM1*) verbonden toohello VNet (*VNet1*, voorvoegsel: 10.9.0.0/16) tooconnect tooa VM(VM3) in een nieuw peered VNet is mislukt (*VNet3*, 10.10.0.0/16 voorvoegsel).</span><span class="sxs-lookup"><span data-stu-id="fb603-120">A VM (*VM1*) connected toohello VNet (*VNet1*, prefix: 10.9.0.0/16) fails tooconnect tooa VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="fb603-121">Er zijn geen udr's of BGP-routes toegepaste tooVM1-NIC1 network interface die is verbonden toohello VM, alleen de systeemroutes van het worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="fb603-121">There are no UDRs or BGP routes applied tooVM1-NIC1 network interface connected toohello VM, only system routes are applied.</span></span>

<span data-ttu-id="fb603-122">Dit artikel wordt uitgelegd hoe toodetermine Hallo veroorzaken Hallo verbinding mislukt, met behulp van de mogelijkheid effectieve routes in Azure Resource Management-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="fb603-122">This article explains how toodetermine hello cause of hello connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="fb603-123">Tijdens het Hallo-voorbeeld wordt alleen de systeemroutes van het, Hallo dezelfde stappen kan worden gebruikte toodetermine binnenkomende en uitgaande verbindingsfouten via een routetype.</span><span class="sxs-lookup"><span data-stu-id="fb603-123">While hello example uses only system routes, hello same steps can be used toodetermine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="fb603-124">Als uw virtuele machine meer dan één NIC die is gekoppeld heeft, controleert u effectieve routes voor elk Hallo NIC's toodiagnose network connectivity problemen tooand van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fb603-124">If your VM has more than one NIC attached, check effective routes for each of hello NICs toodiagnose network connectivity issues tooand from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="fb603-125">De effectieve routes weergeven voor een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="fb603-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="fb603-126">toosee hello cumulatieve routes die zijn toegepast tooa VM, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fb603-126">toosee hello aggregate routes that are applied tooa VM, complete hello following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="fb603-127">De effectieve routes weergeven voor een netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="fb603-127">View effective routes for a network interface</span></span>
<span data-ttu-id="fb603-128">toosee hello cumulatieve routes die zijn toegepast tooa netwerkinterface, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fb603-128">toosee hello aggregate routes that are applied tooa network interface, complete hello following steps:</span></span>

1. <span data-ttu-id="fb603-129">Start een Azure PowerShell-sessie en meld u aan tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fb603-129">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="fb603-130">Als u niet bekend met Azure PowerShell bent, leest u Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="fb603-130">If you’re not familiar with Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="fb603-131">Hallo volgende opdracht retourneert alle routes toegepast tooa-netwerkinterface met de naam *VM1 NIC1* in de resourcegroep Hallo *RG1*.</span><span class="sxs-lookup"><span data-stu-id="fb603-131">hello following command returns all routes applied tooa network interface named *VM1-NIC1* in hello resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="fb603-132">Als u de naam van een netwerkinterface Hallo niet weet, typt u Hallo tooretrieve Hallo opdrachtnamen van alle netwerkinterfaces in een resource group.* na</span><span class="sxs-lookup"><span data-stu-id="fb603-132">If you don’t know hello name of a network interface, type hello following command tooretrieve hello names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="fb603-133">Hallo volgende uitvoer ziet er vergelijkbare toohello uitvoer voor elke route toegepast toohello subnet Hallo die NIC is verbonden met:</span><span class="sxs-lookup"><span data-stu-id="fb603-133">hello following output looks similar toohello output for each route applied toohello subnet hello NIC is connected to:</span></span>
   
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
   
   <span data-ttu-id="fb603-134">U ziet in Hallo uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="fb603-134">Notice hello following in hello output:</span></span>
   
   * <span data-ttu-id="fb603-135">**Naam**: naam van de effectieve route Hallo mag niet leeg zijn, tenzij expliciet is opgegeven voor de gebruiker gedefinieerde routes.</span><span class="sxs-lookup"><span data-stu-id="fb603-135">**Name**: Name of hello effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="fb603-136">**Status**: geeft de status van de effectieve Hallo-route.</span><span class="sxs-lookup"><span data-stu-id="fb603-136">**State**: Indicates state of hello effective route.</span></span> <span data-ttu-id="fb603-137">Mogelijke waarden zijn 'Active' of 'Ongeldig'</span><span class="sxs-lookup"><span data-stu-id="fb603-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="fb603-138">**AddressPrefixes**: Hiermee geeft u Hallo-adresvoorvoegsel van Hallo effectieve route in CIDR-notatie.</span><span class="sxs-lookup"><span data-stu-id="fb603-138">**AddressPrefixes**: Specifies hello address prefix of hello effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="fb603-139">**nextHopType**: geeft aan Hallo volgende hop voor Hallo opgegeven route.</span><span class="sxs-lookup"><span data-stu-id="fb603-139">**nextHopType**: Indicates hello next hop for hello given route.</span></span> <span data-ttu-id="fb603-140">Mogelijke waarden zijn *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, of *Null*.</span><span class="sxs-lookup"><span data-stu-id="fb603-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="fb603-141">Een waarde van *Null* voor **nextHopType** een UDR kan duiden op een ongeldige route.</span><span class="sxs-lookup"><span data-stu-id="fb603-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="fb603-142">Bijvoorbeeld, als **nextHopType** is *VirtualAppliance* en Hallo virtueel netwerkapparaat VM niet in een status ingericht/uitvoeren is.</span><span class="sxs-lookup"><span data-stu-id="fb603-142">For example, if **nextHopType** is *VirtualAppliance* and hello network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="fb603-143">Als **nextHopType** is *VPNGateway* en er is geen gateway ingericht/uitvoeren in VNet gegeven hello, Hallo route ongeldig geworden.</span><span class="sxs-lookup"><span data-stu-id="fb603-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in hello given VNet, hello route may become invalid.</span></span>
   * <span data-ttu-id="fb603-144">**NextHopIpAddress**: Hallo IP-adres van de volgende hop Hallo van Hallo effectieve route.</span><span class="sxs-lookup"><span data-stu-id="fb603-144">**NextHopIpAddress**: Specifies hello IP address of hello next hop of hello effective route.</span></span>
   
   <span data-ttu-id="fb603-145">Hallo volgende opdracht retourneert Hallo routes in een eenvoudiger tooview tabel:</span><span class="sxs-lookup"><span data-stu-id="fb603-145">hello following command returns hello routes in an easier tooview table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="fb603-146">Hallo volgende uitvoer is aantal Hallo uitvoer ontvangen voor Hallo scenario eerder beschreven:</span><span class="sxs-lookup"><span data-stu-id="fb603-146">hello following output is some of hello output received for hello scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="fb603-147">Er is geen route vermeld toohello *WestUS VNet3* VNet (10.10.0.0/16)** van het voorvoegsel *WestUS VNet1* (voorvoegsel 10.9.0.0/16) in de uitvoer van de vorige stap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="fb603-147">There is no route listed toohello *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in hello output from hello previous step.</span></span> <span data-ttu-id="fb603-148">Zoals u in de volgende afbeelding hello, Hallo VNet peeringkoppeling Hello *WestUS VNet3* VNet is in Hallo *verbroken* status.</span><span class="sxs-lookup"><span data-stu-id="fb603-148">As shown in hello following picture, hello VNet peering link with hello *WestUS-VNet3* VNet is in hello *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="fb603-149">Hallo bidirectionele koppeling voor Hallo peering verbroken wordt, waarin wordt uitgelegd waarom VM1 kan geen verbinding maken tooVM3 in Hallo *WestUS VNet3* VNet.</span><span class="sxs-lookup"><span data-stu-id="fb603-149">hello bi-directional link for hello peering is broken, which explains why VM1 could not connect tooVM3 in hello *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="fb603-150">Instellen van een bidirectionele VNet-peeringkoppeling opnieuw voor *WestUS VNet1* en *WestUS VNet3* VNets.</span><span class="sxs-lookup"><span data-stu-id="fb603-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="fb603-151">Hier volgt Hallo uitvoer die wordt geretourneerd nadat Hallo VNet peeringkoppeling correct is ingesteld:</span><span class="sxs-lookup"><span data-stu-id="fb603-151">hello output returned after hello VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="fb603-152">Zodra u hebt vastgesteld Hallo probleem, u kunt toevoegen, verwijderen, of wijzig routes en routetabellen.</span><span class="sxs-lookup"><span data-stu-id="fb603-152">Once you determine hello issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="fb603-153">Type Hallo na de opdracht toosee een lijst met opdrachten Hallo gebruikt dus toodo:</span><span class="sxs-lookup"><span data-stu-id="fb603-153">Type hello following command toosee a list of hello commands used toodo so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="fb603-154">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="fb603-154">Considerations</span></span>
<span data-ttu-id="fb603-155">Een paar dingen tookeep rekening moet houden bij het controleren van de lijst met routes Hallo geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="fb603-155">A few things tookeep in mind when reviewing hello list of routes returned:</span></span>

* <span data-ttu-id="fb603-156">Routering is gebaseerd op langste voorvoegsel overeen (LPM) tussen udr's, systeem- en BGP-routes.</span><span class="sxs-lookup"><span data-stu-id="fb603-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="fb603-157">Als er meer dan één route met Hallo dezelfde LPM overeenkomen, en vervolgens een route geselecteerd op basis van de oorsprong in Hallo volgorde:</span><span class="sxs-lookup"><span data-stu-id="fb603-157">If there is more than one route with hello same LPM match, then a route is selected based on its origin in hello following order:</span></span>
  
  * <span data-ttu-id="fb603-158">Gebruiker gedefinieerde route</span><span class="sxs-lookup"><span data-stu-id="fb603-158">User-defined route</span></span>
  * <span data-ttu-id="fb603-159">BGP-route</span><span class="sxs-lookup"><span data-stu-id="fb603-159">BGP route</span></span>
  * <span data-ttu-id="fb603-160">Systeemroute (standaard)</span><span class="sxs-lookup"><span data-stu-id="fb603-160">System (Default) route</span></span>
    
    <span data-ttu-id="fb603-161">U kunt alleen effectieve routes die overeenkomende LPM op basis van alle routes van Hallo beschikbaar zijn met effectieve routes zien.</span><span class="sxs-lookup"><span data-stu-id="fb603-161">With effective routes, you can only see effective routes that are LPM match based on all hello availble routes.</span></span> <span data-ttu-id="fb603-162">Door te laten zien hoe Hallo routes daadwerkelijk wordt geëvalueerd voor een bepaalde NIC, maakt dit het veel eenvoudiger tootroubleshoot specifieke routes die mogelijk van invloed op de connectiviteit van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fb603-162">By showing how hello routes are actually evaluated for a given NIC, this makes it a lot easier tootroubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="fb603-163">Als u udr's hebt en van verkeer tooa netwerk virtueel apparaat (NVA) met verzenden *VirtualAppliance* als **nextHopType**, zorg dat doorsturen via IP is ingeschakeld op het Hallo NVA ontvangende Hallo verkeer of pakketten worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fb603-163">If you have UDRs and are sending traffic tooa network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on hello NVA receiving hello traffic or packets are dropped.</span></span> 
* <span data-ttu-id="fb603-164">Als de geforceerde tunneling is ingeschakeld, worden alle uitgaand internetverkeer gerouteerde tooon-premises.</span><span class="sxs-lookup"><span data-stu-id="fb603-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed tooon-premises.</span></span> <span data-ttu-id="fb603-165">RDP/SSH vanaf Internet tooyour die VM niet met deze instelling werkt, afhankelijk van hoe Hallo lokale verwerkt dit verkeer.</span><span class="sxs-lookup"><span data-stu-id="fb603-165">RDP/SSH from Internet tooyour VM may not work with this setting, depending on how hello on-premises handles this traffic.</span></span> 
  <span data-ttu-id="fb603-166">Geforceerde tunneling kan worden ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="fb603-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="fb603-167">Als u site-naar-site VPN, door een door de gebruiker opgegeven routes (UDR) met nextHopType als VPN-Gateway</span><span class="sxs-lookup"><span data-stu-id="fb603-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="fb603-168">Als een standaardroute wordt geadverteerd via BGP</span><span class="sxs-lookup"><span data-stu-id="fb603-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="fb603-169">Voor VNet-verkeer toowork correct peering een systeemroute met **nextHopType** *VNetPeering* voor Hallo van de VNet-voorvoegsel bereik brengen moet bestaan.</span><span class="sxs-lookup"><span data-stu-id="fb603-169">For VNet peering traffic toowork correctly, a system route with **nextHopType** *VNetPeering* must exist for hello peered VNet’s prefix range.</span></span> <span data-ttu-id="fb603-170">Als deze route bestaat niet en VNet-peering Hallo opgezocht koppeling OK:</span><span class="sxs-lookup"><span data-stu-id="fb603-170">If such a route doesn’t exist and hello VNet peering link looks OK:</span></span>
  * <span data-ttu-id="fb603-171">Wacht een paar seconden en probeer het opnieuw als het een nieuw opgezette peeringkoppeling.</span><span class="sxs-lookup"><span data-stu-id="fb603-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="fb603-172">Tijd tot tijd duurt het langer toopropagate routes tooall Hallo netwerkinterfaces in een subnet.</span><span class="sxs-lookup"><span data-stu-id="fb603-172">It occasionally takes longer toopropagate routes tooall hello network interfaces in a subnet.</span></span>
  * <span data-ttu-id="fb603-173">Netwerkbeveiligingsgroep (NSG) regels mogelijk van invloed op Hallo verkeersstromen.</span><span class="sxs-lookup"><span data-stu-id="fb603-173">Network Security Group (NSG) rules may be impacting hello traffic flows.</span></span> <span data-ttu-id="fb603-174">Zie voor meer informatie, Hallo [Netwerkbeveiligingsgroepen oplossen](virtual-network-nsg-troubleshoot-powershell.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="fb603-174">For more information, see hello [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

