---
title: 'Configureer geforceerde tunneling voor Azure Site-naar-Site-verbindingen: Resource Manager | Microsoft Docs'
description: Hoe tooredirect of 'force' alle Internet bestemd verkeer back tooyour een on-premises locatie.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a><span data-ttu-id="39583-103">Configureer geforceerde tunneling met hello Azure Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="39583-103">Configure forced tunneling using hello Azure Resource Manager deployment model</span></span>

<span data-ttu-id="39583-104">Geforceerde tunneling, kunt u omleiden of 'force' alle Internet bestemd verkeer back tooyour on-premises locatie via een Site-naar-Site VPN-tunnel voor inspectie en controle.</span><span class="sxs-lookup"><span data-stu-id="39583-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="39583-105">Dit is een kritieke beveiligingsvereiste voor de meeste bedrijven beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="39583-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="39583-106">Zonder geforceerde tunneling passeert internetverkeer van uw virtuele machines in Azure altijd van Azure netwerkinfrastructuur rechtstreeks uit toohello Internet, zonder Hallo optie tooallow u tooinspect of audit Hallo-verkeer.</span><span class="sxs-lookup"><span data-stu-id="39583-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="39583-107">Niet-geautoriseerde toegang tot het Internet kan mogelijk leiden tooinformation openbaarmaking of andere typen schendingen van de beveiliging.</span><span class="sxs-lookup"><span data-stu-id="39583-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="39583-108">In dit artikel begeleidt u bij het configureren geforceerde tunneling voor virtuele netwerken die zijn gemaakt met Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="39583-108">This article walks you through configuring forced tunneling for virtual networks created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="39583-109">Geforceerde tunneling kan worden geconfigureerd met behulp van PowerShell, niet via het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="39583-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="39583-110">Als u tooconfigure geforceerde tunneling voor het klassieke implementatiemodel hello wilt, selecteert u klassieke artikel van Hallo vervolgkeuzelijst te volgen:</span><span class="sxs-lookup"><span data-stu-id="39583-110">If you want tooconfigure forced tunneling for hello classic deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="39583-111">PowerShell - Klassiek</span><span class="sxs-lookup"><span data-stu-id="39583-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="39583-112">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="39583-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="39583-113">Over geforceerde tunneling</span><span class="sxs-lookup"><span data-stu-id="39583-113">About forced tunneling</span></span>

<span data-ttu-id="39583-114">Hallo volgende diagram illustreert hoe geforceerde tunneling werkt.</span><span class="sxs-lookup"><span data-stu-id="39583-114">hello following diagram illustrates how forced tunneling works.</span></span> 

![Geforceerde tunneling](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="39583-116">Hallo Frontend-subnet wordt niet geforceerd via een tunnel Hallo bovenstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="39583-116">In hello example above, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="39583-117">Hallo werkbelastingen in Hallo Frontend subnet kunnen blijven tooaccept en toocustomer aanvragen rechtstreeks van Internet Hallo reageren.</span><span class="sxs-lookup"><span data-stu-id="39583-117">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="39583-118">Hallo middelste laag en back-end subnetten worden gedwongen via een tunnel.</span><span class="sxs-lookup"><span data-stu-id="39583-118">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="39583-119">Alle uitgaande verbindingen van deze twee subnetten toohello Internet worden geforceerd of omgeleide terug tooan lokale site via een S2S-VPN-tunnels Hallo.</span><span class="sxs-lookup"><span data-stu-id="39583-119">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="39583-120">Hiermee kunt u toorestrict en inspecteren van toegang tot Internet vanaf uw virtuele machines of cloudservices in Azure, maar blijft tooenable uw service met meerdere lagen architectuur die is vereist.</span><span class="sxs-lookup"><span data-stu-id="39583-120">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="39583-121">Als er geen internetverbinding werkbelastingen in uw virtuele netwerken, kunt u ook geforceerde tunneling toohello volledige virtuele netwerken toepassen.</span><span class="sxs-lookup"><span data-stu-id="39583-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling toohello entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="39583-122">Vereisten en overwegingen</span><span class="sxs-lookup"><span data-stu-id="39583-122">Requirements and considerations</span></span>

<span data-ttu-id="39583-123">Geforceerde tunneling in Azure wordt geconfigureerd via het virtuele netwerk zelfgedefinieerde routes.</span><span class="sxs-lookup"><span data-stu-id="39583-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="39583-124">Omleiden van verkeer tooan lokale site wordt uitgedrukt als een standaardroute toohello Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="39583-124">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="39583-125">Zie voor meer informatie over de gebruiker gedefinieerde Routering en virtuele netwerken, [gebruiker gedefinieerde routes en doorsturen via IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39583-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="39583-126">Elk virtueel netwerksubnet heeft een ingebouwd systeem-routeringstabel.</span><span class="sxs-lookup"><span data-stu-id="39583-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="39583-127">Hallo system routeringstabel heeft Hallo volgende drie groepen van routes:</span><span class="sxs-lookup"><span data-stu-id="39583-127">hello system routing table has hello following three groups of routes:</span></span>
  
  * <span data-ttu-id="39583-128">**Lokale VNet routes:** rechtstreeks toohello bestemming virtuele machines in Hallo hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="39583-128">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="39583-129">**Lokale routes:** toohello Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="39583-129">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="39583-130">**Standaardroute:** rechtstreeks toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="39583-130">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="39583-131">Pakketten die bestemd zijn toohello privé IP-adressen niet wordt gedekt door de vorige twee Hallo routes worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="39583-131">Packets destined toohello private IP addresses not covered by hello previous two routes are dropped.</span></span>
* <span data-ttu-id="39583-132">Deze procedure maakt gebruik van de gebruiker gedefinieerde routes (UDR) toocreate een routering tabel tooadd een standaardroute en koppel deze Hallo routering tabel tooyour VNet subnetten tooenable geforceerde tunneling op deze subnetten.</span><span class="sxs-lookup"><span data-stu-id="39583-132">This procedure uses user-defined routes (UDR) toocreate a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="39583-133">Geforceerde tunneling moet worden gekoppeld aan een VNet met een op route gebaseerde VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="39583-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="39583-134">U moet tooset "standaardsite" tussen Hallo cross-premises lokale sites verbonden toohello virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="39583-134">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span> <span data-ttu-id="39583-135">Bovendien Hallo lokale VPN-apparaat moet worden geconfigureerd met 0.0.0.0/0 als verkeer selectoren.</span><span class="sxs-lookup"><span data-stu-id="39583-135">Also, hello on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="39583-136">ExpressRoute geforceerde tunneling via dit mechanisme niet is geconfigureerd, maar in plaats daarvan wordt ingeschakeld door kondigt een standaardroute via ExpressRoute BGP Hallo peeringsessies.</span><span class="sxs-lookup"><span data-stu-id="39583-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="39583-137">Zie voor meer informatie, Hallo [ExpressRoute-documentatie](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="39583-137">For more information, see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="39583-138">Configuratie-overzicht</span><span class="sxs-lookup"><span data-stu-id="39583-138">Configuration overview</span></span>

<span data-ttu-id="39583-139">Hallo na procedure kunt u een resourcegroep en een VNet maken.</span><span class="sxs-lookup"><span data-stu-id="39583-139">hello following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="39583-140">Vervolgens moet u een VPN-gateway maken en geforceerde tunneling configureren.</span><span class="sxs-lookup"><span data-stu-id="39583-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="39583-141">In deze procedure Hallo virtueel netwerk MultiTier-VNet drie subnetten heeft: 'Frontend', 'Midtier' en 'Back-end' met vier cross-premises verbindingen: 'DefaultSiteHQ' en drie vertakkingen.</span><span class="sxs-lookup"><span data-stu-id="39583-141">In this procedure, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="39583-142">procedurestappen Hallo Hallo 'DefaultSiteHQ' niet instellen omdat Hallo standaard site-verbinding voor geforceerde tunneling en Hallo 'Midtier' en 'Back-end' subnetten toouse geforceerde tunneling configureren.</span><span class="sxs-lookup"><span data-stu-id="39583-142">hello procedure steps set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello 'Midtier' and 'Backend' subnets toouse forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="39583-143">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="39583-143">Before you begin</span></span>

<span data-ttu-id="39583-144">Installeer de nieuwste versie Hallo Hallo Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="39583-144">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="39583-145">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van Hallo PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="39583-145">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="toolog-in"></a><span data-ttu-id="39583-146">toolog in</span><span class="sxs-lookup"><span data-stu-id="39583-146">toolog in</span></span>

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="39583-147">Geforceerde tunneling configureren</span><span class="sxs-lookup"><span data-stu-id="39583-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="39583-148">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="39583-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="39583-149">Een virtueel netwerk maken en geef de subnetten.</span><span class="sxs-lookup"><span data-stu-id="39583-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="39583-150">Hallo lokale netwerkgateways maken.</span><span class="sxs-lookup"><span data-stu-id="39583-150">Create hello local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="39583-151">Hallo route tabel en route-regel maken.</span><span class="sxs-lookup"><span data-stu-id="39583-151">Create hello route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="39583-152">Hallo route tabel toohello Midtier en back-end subnetten koppelen.</span><span class="sxs-lookup"><span data-stu-id="39583-152">Associate hello route table toohello Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="39583-153">Hallo Gateway met een standaard-site maken.</span><span class="sxs-lookup"><span data-stu-id="39583-153">Create hello Gateway with a default site.</span></span> <span data-ttu-id="39583-154">Deze stap duurt enige tijd toocomplete, soms 45 minuten of langer, omdat u momenteel maakt en Hallo gateway configureert.</span><span class="sxs-lookup"><span data-stu-id="39583-154">This step takes some time toocomplete, sometimes 45 minutes or more, because you are creating and configuring hello gateway.</span></span><br> <span data-ttu-id="39583-155">Hallo **- GatewayDefaultSite** Hallo cmdlet-parameter waarmee Hallo gedwongen routering configuratie toowork, dus nemen voorzichtig tooconfigure deze instelling correct is.</span><span class="sxs-lookup"><span data-stu-id="39583-155">hello **-GatewayDefaultSite** is hello cmdlet parameter that allows hello forced routing configuration toowork, so take care tooconfigure this setting properly.</span></span> <span data-ttu-id="39583-156">Deze parameter is beschikbaar in PowerShell 1.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="39583-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="39583-157">Tot stand brengen Hallo Site-naar-Site VPN-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="39583-157">Establish hello Site-to-Site VPN connections.</span></span>

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```