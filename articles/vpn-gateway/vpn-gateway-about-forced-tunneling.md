---
title: 'Configureer geforceerde tunneling voor Azure Site-naar-Site-verbindingen: klassieke | Microsoft Docs'
description: Hoe tooredirect of 'force' alle Internet bestemd verkeer back tooyour een on-premises locatie.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a><span data-ttu-id="d6874-103">Configureer geforceerde tunneling met behulp van het klassieke implementatiemodel Hallo</span><span class="sxs-lookup"><span data-stu-id="d6874-103">Configure forced tunneling using hello classic deployment model</span></span>

<span data-ttu-id="d6874-104">Geforceerde tunneling, kunt u omleiden of 'force' alle Internet bestemd verkeer back tooyour on-premises locatie via een Site-naar-Site VPN-tunnel voor inspectie en controle.</span><span class="sxs-lookup"><span data-stu-id="d6874-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="d6874-105">Dit is een kritieke beveiligingsvereiste voor de meeste bedrijven beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="d6874-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="d6874-106">Zonder geforceerde tunneling wordt internetverkeer van uw virtuele machines in Azure altijd passeren van Azure netwerkinfrastructuur rechtstreeks uit toohello Internet, zonder Hallo optie tooallow u tooinspect of audit Hallo-verkeer.</span><span class="sxs-lookup"><span data-stu-id="d6874-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="d6874-107">Niet-geautoriseerde toegang tot het Internet kan mogelijk leiden tooinformation openbaarmaking of andere typen schendingen van de beveiliging.</span><span class="sxs-lookup"><span data-stu-id="d6874-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="d6874-108">In dit artikel begeleidt u bij het configureren geforceerde tunneling voor virtuele netwerken die zijn gemaakt met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6874-108">This article walks you through configuring forced tunneling for virtual networks created using hello classic deployment model.</span></span> <span data-ttu-id="d6874-109">Geforceerde tunneling kan worden geconfigureerd met behulp van PowerShell, niet via het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d6874-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="d6874-110">Als u tooconfigure geforceerde tunneling Hallo Resource Manager-implementatiemodel wilt, selecteert u klassieke artikel van Hallo vervolgkeuzelijst te volgen:</span><span class="sxs-lookup"><span data-stu-id="d6874-110">If you want tooconfigure forced tunneling for hello Resource Manager deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6874-111">PowerShell - Klassiek</span><span class="sxs-lookup"><span data-stu-id="d6874-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="d6874-112">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d6874-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="d6874-113">Vereisten en overwegingen</span><span class="sxs-lookup"><span data-stu-id="d6874-113">Requirements and considerations</span></span>
<span data-ttu-id="d6874-114">Geforceerde tunneling in Azure wordt geconfigureerd via het virtuele netwerk zelfgedefinieerde routes (UDR).</span><span class="sxs-lookup"><span data-stu-id="d6874-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="d6874-115">Omleiden van verkeer tooan lokale site wordt uitgedrukt als een standaardroute toohello Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="d6874-115">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="d6874-116">Hallo volgende sectie vindt u Hallo beperking van het Hallo-routeringstabel en -routes voor een virtuele Azure-netwerk:</span><span class="sxs-lookup"><span data-stu-id="d6874-116">hello following section lists hello current limitation of hello routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="d6874-117">Elk virtueel netwerksubnet heeft een ingebouwd systeem-routeringstabel.</span><span class="sxs-lookup"><span data-stu-id="d6874-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="d6874-118">Hallo system routeringstabel heeft Hallo volgende drie groepen van routes:</span><span class="sxs-lookup"><span data-stu-id="d6874-118">hello system routing table has hello following three groups of routes:</span></span>

  * <span data-ttu-id="d6874-119">**Lokale VNet routes:** rechtstreeks toohello bestemming virtuele machines in Hallo hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="d6874-119">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="d6874-120">**Lokale routes:** toohello Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="d6874-120">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="d6874-121">**Standaardroute:** rechtstreeks toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="d6874-121">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="d6874-122">Pakketten die bestemd zijn toohello privé IP-adressen niet wordt gedekt door de vorige twee Hallo routes worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d6874-122">Packets destined toohello private IP addresses not covered by hello previous two routes will be dropped.</span></span>
* <span data-ttu-id="d6874-123">U kunt met Hallo-release van de gebruiker gedefinieerde routes, een routering tabel tooadd een standaardroute maken en vervolgens koppelen Hallo routering tabel tooyour VNet subnetten tooenable geforceerde tunneling op deze subnetten.</span><span class="sxs-lookup"><span data-stu-id="d6874-123">With hello release of user-defined routes, you can create a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="d6874-124">U moet tooset "standaardsite" tussen Hallo cross-premises lokale sites verbonden toohello virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="d6874-124">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span>
* <span data-ttu-id="d6874-125">Geforceerde tunneling moet worden gekoppeld aan een VNet met een VPN-gateway voor dynamische routering (geen statische gateway genoemd).</span><span class="sxs-lookup"><span data-stu-id="d6874-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="d6874-126">ExpressRoute geforceerde tunneling via dit mechanisme niet is geconfigureerd, maar in plaats daarvan wordt ingeschakeld door kondigt een standaardroute via ExpressRoute BGP Hallo peeringsessies.</span><span class="sxs-lookup"><span data-stu-id="d6874-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="d6874-127">Zie Hallo [ExpressRoute-documentatie](https://azure.microsoft.com/documentation/services/expressroute/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d6874-127">Please see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="d6874-128">Configuratie-overzicht</span><span class="sxs-lookup"><span data-stu-id="d6874-128">Configuration overview</span></span>
<span data-ttu-id="d6874-129">In de Hallo voorbeeld te volgen, tunneled Hallo Frontend subnet wordt niet geforceerd.</span><span class="sxs-lookup"><span data-stu-id="d6874-129">In hello following example, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="d6874-130">Hallo werkbelastingen in Hallo Frontend subnet kunnen blijven tooaccept en toocustomer aanvragen rechtstreeks van Internet Hallo reageren.</span><span class="sxs-lookup"><span data-stu-id="d6874-130">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="d6874-131">Hallo middelste laag en back-end subnetten worden gedwongen via een tunnel.</span><span class="sxs-lookup"><span data-stu-id="d6874-131">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="d6874-132">Alle uitgaande verbindingen van deze twee subnetten toohello Internet worden geforceerd of omgeleide terug tooan lokale site via een S2S-VPN-tunnels Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6874-132">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="d6874-133">Hiermee kunt u toorestrict en inspecteren van toegang tot Internet vanaf uw virtuele machines of cloudservices in Azure, maar blijft tooenable uw service met meerdere lagen architectuur die is vereist.</span><span class="sxs-lookup"><span data-stu-id="d6874-133">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="d6874-134">U kunt ook geforceerde tunneling toohello volledige virtuele netwerken toepassen als er geen internetverbinding werkbelastingen in uw virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="d6874-134">You also can apply forced tunneling toohello entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![Geforceerde tunneling](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="d6874-136">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="d6874-136">Before you begin</span></span>
<span data-ttu-id="d6874-137">Controleer of u Hallo volgende voordat de begin-configuratie-items.</span><span class="sxs-lookup"><span data-stu-id="d6874-137">Verify that you have hello following items before beginning configuration.</span></span>

* <span data-ttu-id="d6874-138">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d6874-138">An Azure subscription.</span></span> <span data-ttu-id="d6874-139">Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6874-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d6874-140">Een geconfigureerde virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="d6874-140">A configured virtual network.</span></span> 
* <span data-ttu-id="d6874-141">Hallo meest recente versie van hello Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d6874-141">hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="d6874-142">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van Hallo PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d6874-142">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="d6874-143">Geforceerde tunneling configureren</span><span class="sxs-lookup"><span data-stu-id="d6874-143">Configure forced tunneling</span></span>
<span data-ttu-id="d6874-144">Hallo na procedure kunt u opgeven geforceerde tunneling voor een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="d6874-144">hello following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="d6874-145">Hallo configuratiestappen overeen toohello VNet netwerk configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="d6874-145">hello configuration steps correspond toohello VNet network configuration file.</span></span>

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

<span data-ttu-id="d6874-146">In dit voorbeeld Hallo virtueel netwerk MultiTier-VNet drie subnetten heeft: 'Frontend', 'Midtier' en 'Back-end' subnetten, met vier cross-premises verbindingen: 'DefaultSiteHQ' en drie vertakkingen.</span><span class="sxs-lookup"><span data-stu-id="d6874-146">In this example, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="d6874-147">Hallo stappen Hallo 'DefaultSiteHQ' ingesteld als Hallo standaard site-verbinding voor geforceerde tunneling, en Hallo Midtier en back-end subnetten toouse geforceerde tunneling configureren.</span><span class="sxs-lookup"><span data-stu-id="d6874-147">hello steps will set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello Midtier and Backend subnets toouse forced tunneling.</span></span>

1. <span data-ttu-id="d6874-148">Maak een routeringstabel.</span><span class="sxs-lookup"><span data-stu-id="d6874-148">Create a routing table.</span></span> <span data-ttu-id="d6874-149">Hallo cmdlet toocreate na de routetabel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d6874-149">Use hello following cmdlet toocreate your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="d6874-150">Een standaardrouteringstabel route toohello toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d6874-150">Add a default route toohello routing table.</span></span> 

  <span data-ttu-id="d6874-151">Hallo wordt volgende voorbeeld een route toohello standaardrouteringstabel gemaakt in stap 1.</span><span class="sxs-lookup"><span data-stu-id="d6874-151">hello following example adds a default route toohello routing table created in Step 1.</span></span> <span data-ttu-id="d6874-152">Merk op dat alleen route ondersteund Hallo is Hallo voorvoegsel voor bestemming van '0.0.0.0/0' toohello 'VPNGateway' NextHop.</span><span class="sxs-lookup"><span data-stu-id="d6874-152">Note that hello only route supported is hello destination prefix of "0.0.0.0/0" toohello "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="d6874-153">Hallo routering tabel toohello subnetten koppelen.</span><span class="sxs-lookup"><span data-stu-id="d6874-153">Associate hello routing table toohello subnets.</span></span> 

  <span data-ttu-id="d6874-154">Nadat een routeringstabel is gemaakt en een route is toegevoegd, na voorbeeld tooadd hello gebruiken of Hallo route tabel tooa VNet subnet koppelen.</span><span class="sxs-lookup"><span data-stu-id="d6874-154">After a routing table is created and a route added, use hello following example tooadd or associate hello route table tooa VNet subnet.</span></span> <span data-ttu-id="d6874-155">Hallo voorbeeld voegt Hallo route tabel 'MyRouteTable' toohello Midtier en back-end-subnetten van VNet MultiTier-VNet.</span><span class="sxs-lookup"><span data-stu-id="d6874-155">hello example adds hello route table "MyRouteTable" toohello Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="d6874-156">Wijs een standaardlocatie voor geforceerde tunneling.</span><span class="sxs-lookup"><span data-stu-id="d6874-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="d6874-157">In Hallo vóór stap, Hallo cmdlet voorbeeldscripts Hallo routeringstabel gemaakt en gekoppeld Hallo route tabel tootwo hello VNet subnetten.</span><span class="sxs-lookup"><span data-stu-id="d6874-157">In hello preceding step, hello sample cmdlet scripts created hello routing table and associated hello route table tootwo of hello VNet subnets.</span></span> <span data-ttu-id="d6874-158">Hallo resterende stap is tooselect een lokale site tussen Hallo meerdere site-verbindingen van het virtuele netwerk Hallo als Hallo standaardsite of -tunnel.</span><span class="sxs-lookup"><span data-stu-id="d6874-158">hello remaining step is tooselect a local site among hello multi-site connections of hello virtual network as hello default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="d6874-159">Aanvullende PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="d6874-159">Additional PowerShell cmdlets</span></span>
### <a name="toodelete-a-route-table"></a><span data-ttu-id="d6874-160">een routetabel toodelete</span><span class="sxs-lookup"><span data-stu-id="d6874-160">toodelete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a><span data-ttu-id="d6874-161">een routetabel toolist</span><span class="sxs-lookup"><span data-stu-id="d6874-161">toolist a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a><span data-ttu-id="d6874-162">een route van een routetabel toodelete</span><span class="sxs-lookup"><span data-stu-id="d6874-162">toodelete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a><span data-ttu-id="d6874-163">tooremove een route van een subnet</span><span class="sxs-lookup"><span data-stu-id="d6874-163">tooremove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a><span data-ttu-id="d6874-164">toolist Hallo-routetabel die zijn gekoppeld aan een subnet</span><span class="sxs-lookup"><span data-stu-id="d6874-164">toolist hello route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="d6874-165">tooremove een standaard-site van een VNet VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="d6874-165">tooremove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```