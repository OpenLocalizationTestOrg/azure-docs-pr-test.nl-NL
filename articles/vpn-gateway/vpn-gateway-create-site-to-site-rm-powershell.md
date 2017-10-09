---
title: 'Verbinding maken met uw lokale netwerk tooan virtuele Azure-netwerk: Site-naar-Site VPN: PowerShell | Microsoft Docs'
description: Stappen toocreate een IPsec-verbinding van uw on-premises netwerk tooan virtuele Azure-netwerk via openbaar Internet Hallo. Deze stappen helpen u een cross-premises site-naar-site-VPN-gatewayverbinding te maken met PowerShell.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="6bcc9-104">Een VNet met een site-naar-site-VPN-verbinding maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bcc9-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="6bcc9-105">Dit artikel laat zien hoe toouse PowerShell toocreate een Site-naar-Site VPN-gatewayverbinding vanuit uw on-premises netwerk toohello VNet.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-105">This article shows you how toouse PowerShell toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="6bcc9-106">Hallo stappen in dit artikel van toepassing toohello Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="6bcc9-107">Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="6bcc9-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6bcc9-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6bcc9-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="6bcc9-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bcc9-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="6bcc9-110">CLI</span><span class="sxs-lookup"><span data-stu-id="6bcc9-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="6bcc9-111">Azure Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="6bcc9-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="6bcc9-112">Klassieke portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="6bcc9-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="6bcc9-113">Een Site-naar-Site VPN-gatewayverbinding gebruikte tooconnect is uw on-premises netwerk tooan virtuele Azure-netwerk via een VPN-IPsec/IKE (IKEv1 of IKEv2)-tunnel.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="6bcc9-114">Dit type verbinding vereist een VPN-zich on-premises apparaten met een extern gericht openbaar IP-adres toegewezen tooit.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="6bcc9-115">Zie [Overzicht van VPN Gateway](vpn-gateway-about-vpngateways.md) voor meer informatie over VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagram: cross-premises site-naar-site-VPN-gatewayverbinding](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="6bcc9-117"><a name="before"></a>Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="6bcc9-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="6bcc9-118">Controleer of dat u Hallo criteria volgen voordat u begint met de configuratie hebt voldaan:</span><span class="sxs-lookup"><span data-stu-id="6bcc9-118">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="6bcc9-119">Zorg ervoor dat u hebt een compatibel VPN-apparaat en iemand die dit kunnen tooconfigure deze.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-119">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="6bcc9-120">Zie [Over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor meer informatie over compatibele VPN-apparaten en -apparaatconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="6bcc9-121">Controleer of u een extern gericht openbaar IPv4-adres voor het VPN-apparaat hebt.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="6bcc9-122">Dit IP-adres kan zich niet achter een NAT bevinden.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="6bcc9-123">Als u niet bekend bent met de Hallo IP-adresbereiken zich in uw on-premises netwerkconfiguratie, moet u toocoordinate met iemand die deze details voor u verstrekken kan.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-123">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="6bcc9-124">Wanneer u deze configuratie maakt, moet u Hallo IP-bereik adresvoorvoegsels Azure routeert tooyour on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-124">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="6bcc9-125">Geen van de subnetten Hallo van uw on-premises netwerk kunnen via lap met Hallo virtueel netwerksubnetten die u wilt dat tooconnect om te.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-125">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="6bcc9-126">Installeer de nieuwste versie Hallo Hallo Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-126">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="6bcc9-127">PowerShell-cmdlets worden regelmatig bijgewerkt en normaal gesproken moet u tooupdate uw PowerShell-cmdlets tooget Hallo meest recente functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-127">PowerShell cmdlets are updated frequently and you will typically need tooupdate your PowerShell cmdlets tooget hello latest feature functionality.</span></span> <span data-ttu-id="6bcc9-128">Als u uw PowerShell-cmdlets niet bijwerkt, mislukken Hallo waarden die zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-128">If you don't update your PowerShell cmdlets, hello values specified may fail.</span></span> <span data-ttu-id="6bcc9-129">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het downloaden en installeren van de PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-129">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="6bcc9-130"><a name="example"></a>Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="6bcc9-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="6bcc9-131">Hallo-voorbeelden in dit artikel gebruiken Hallo waarden te volgen.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-131">hello examples in this article use hello following values.</span></span> <span data-ttu-id="6bcc9-132">U kunt deze waarden toocreate een testomgeving gebruiken of toothem verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-132">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <span data-ttu-id="6bcc9-133"><a name="Login"></a>1. Verbinding maken met tooyour abonnement</span><span class="sxs-lookup"><span data-stu-id="6bcc9-133"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="6bcc9-134"><a name="VNet"></a>2. Een virtueel netwerk en een gatewaysubnet maken</span><span class="sxs-lookup"><span data-stu-id="6bcc9-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="6bcc9-135">Als u nog geen virtueel netwerk hebt, maakt u er een.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="6bcc9-136">Wanneer u een virtueel netwerk maakt, zorg dat Hallo-adresruimten die u opgeeft niet overlappen met adresruimten Hallo die u op uw on-premises netwerk hebt.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-136">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="6bcc9-137"><a name="vnet"></a>toocreate een virtueel netwerk en een gatewaysubnet</span><span class="sxs-lookup"><span data-stu-id="6bcc9-137"><a name="vnet"></a>toocreate a virtual network and a gateway subnet</span></span>

<span data-ttu-id="6bcc9-138">In dit voorbeeld worden een virtueel netwerk en een gatewaysubnet gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="6bcc9-139">Als u al een virtueel netwerk die u een gatewaysubnet moet Zie tooadd [tooadd een gateway subnet tooa virtueel netwerk u al hebt gemaakt](#gatewaysubnet).</span><span class="sxs-lookup"><span data-stu-id="6bcc9-139">If you already have a virtual network that you need tooadd a gateway subnet to, see [tooadd a gateway subnet tooa virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="6bcc9-140">Een resourcegroep maken:</span><span class="sxs-lookup"><span data-stu-id="6bcc9-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="6bcc9-141">Maak uw virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-141">Create your virtual network.</span></span>

1. <span data-ttu-id="6bcc9-142">Hallo-variabelen worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-142">Set hello variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="6bcc9-143">Hallo VNet maken.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-143">Create hello VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="6bcc9-144"><a name="gatewaysubnet"></a>een virtueel netwerk voor gateway-subnet tooa tooadd die u al hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="6bcc9-144"><a name="gatewaysubnet"></a>tooadd a gateway subnet tooa virtual network you have already created</span></span>

1. <span data-ttu-id="6bcc9-145">Hallo-variabelen worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-145">Set hello variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="6bcc9-146">Hallo gatewaysubnet maken.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-146">Create hello gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="6bcc9-147">Hallo configuratie instellen.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-147">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="6bcc9-148">3. <a name="localnet"></a>Hallo lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="6bcc9-148">3. <a name="localnet"></a>Create hello local network gateway</span></span>

<span data-ttu-id="6bcc9-149">Hallo lokale netwerkgateway verwijst doorgaans tooyour on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-149">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="6bcc9-150">U geeft Hallo site een naam waarmee Azure kunt tooit verwijzen, geeft u vervolgens Hallo IP-adres van Hallo lokale VPN-apparaat toowhich maakt u een verbinding.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-150">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="6bcc9-151">U wordt ook Hallo IP-adresvoorvoegsels worden doorgestuurd via Hallo VPN-gateway toohello VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-151">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="6bcc9-152">Hallo-adresvoorvoegsels die u opgeeft voorvoegsels Hallo zich op uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-152">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="6bcc9-153">Als uw on-premises netwerk verandert, kunt u Hallo voorvoegsels eenvoudig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-153">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="6bcc9-154">Hallo volgende waarden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6bcc9-154">Use hello following values:</span></span>

* <span data-ttu-id="6bcc9-155">Hallo *GatewayIPAddress* Hallo IP-adres van uw on-premises VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-155">hello *GatewayIPAddress* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="6bcc9-156">Het VPN-apparaat kan zich niet achter een NAT bevinden.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="6bcc9-157">Hallo *AddressPrefix* is uw on-premises-adresruimte.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-157">hello *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="6bcc9-158">een lokale netwerkgateway met één adresvoorvoegsel tooadd:</span><span class="sxs-lookup"><span data-stu-id="6bcc9-158">tooadd a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="6bcc9-159">een lokale netwerkgateway met meerdere adresvoorvoegsels tooadd:</span><span class="sxs-lookup"><span data-stu-id="6bcc9-159">tooadd a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="6bcc9-160">toomodify IP-adresvoorvoegsels voor uw lokale netwerkgateway:</span><span class="sxs-lookup"><span data-stu-id="6bcc9-160">toomodify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="6bcc9-161">Soms veranderen de voorvoegsels voor uw lokale netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="6bcc9-162">Hallo stappen u rekening houden met toomodify uw IP-adres voorvoegsels is afhankelijk van of u een VPN-gatewayverbinding hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-162">hello steps you take toomodify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="6bcc9-163">Zie Hallo [adresvoorvoegsels voor een lokale netwerkgateway wijzigen](#modify) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-163">See hello [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="6bcc9-164"><a name="PublicIP"></a>4. Een openbaar IP-adres aanvragen</span><span class="sxs-lookup"><span data-stu-id="6bcc9-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="6bcc9-165">Een VPN Gateway moet een openbaar IP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="6bcc9-166">U eerst aanvragen Hallo IP-adres resource en vervolgens tooit verwijzen bij het maken van uw virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-166">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="6bcc9-167">Hallo IP-adres dynamisch toegewezen toohello resource wanneer Hallo VPN-gateway is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-167">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="6bcc9-168">VPN Gateway ondersteunt momenteel alleen *dynamische* toewijzing van openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="6bcc9-169">U kunt geen toewijzing van een statisch openbaar IP-adres aanvragen.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="6bcc9-170">Dit betekent echter niet dat dat Hallo IP-adres verandert nadat tooyour VPN-gateway is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-170">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="6bcc9-171">de enige keer Hallo Hallo openbare IP-adreswijzigingen is wanneer Hallo gateway is verwijderd en opnieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-171">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="6bcc9-172">Het verandert niet wanneer de grootte van uw VPN Gateway verandert, wanneer deze gateway opnieuw wordt ingesteld of wanneer andere interne onderhoudswerkzaamheden of upgrades worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="6bcc9-173">Een openbaar IP-adres dat wordt toegewezen tooyour virtueel netwerk VPN-gateway aanvragen.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-173">Request a Public IP address that will be assigned tooyour virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="6bcc9-174"><a name="GatewayIPConfig"></a>5. Hallo-gateway voor IP-adressen van de configuratie maken</span><span class="sxs-lookup"><span data-stu-id="6bcc9-174"><a name="GatewayIPConfig"></a>5. Create hello gateway IP addressing configuration</span></span>

<span data-ttu-id="6bcc9-175">Hallo-gatewayconfiguratie bepaalt Hallo subnet en Hallo openbare IP-adres toouse.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-175">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="6bcc9-176">Hallo voorbeeld toocreate na de configuratie van uw gateway gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6bcc9-176">Use hello following example toocreate your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="6bcc9-177"><a name="CreateGateway"></a>6. Hallo VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="6bcc9-177"><a name="CreateGateway"></a>6. Create hello VPN gateway</span></span>

<span data-ttu-id="6bcc9-178">VPN-gateway van Hallo virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-178">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="6bcc9-179">Maken van een VPN-gateway kan duren too45 minuten of meer toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-179">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="6bcc9-180">Hallo volgende waarden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6bcc9-180">Use hello following values:</span></span>

* <span data-ttu-id="6bcc9-181">Hallo *- GatewayType* voor een Site-naar-Site configuratie is *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-181">hello *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="6bcc9-182">Hallo-Gatewaytype is altijd specifiek toohello configuratie die u implementeert.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-182">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="6bcc9-183">Andere gatewayconfiguraties vereisen misschien -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="6bcc9-184">Hallo *- VpnType* kan *RouteBased* (bedoeld tooas een dynamische Gateway in sommige documentatie), of *PolicyBased* (aangeduid tooas een statische Gateway in sommige documentatie ).</span><span class="sxs-lookup"><span data-stu-id="6bcc9-184">hello *-VpnType* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="6bcc9-185">Voor meer informatie over VPN-gatewaytypen raadpleegt u [Over VPN Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="6bcc9-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="6bcc9-186">Selecteer Hallo dat u wilt dat toouse Gateway-SKU.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-186">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="6bcc9-187">Voor bepaalde SKU's gelden configuratiebeperkingen.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="6bcc9-188">Zie [Gateway-SKU's](vpn-gateway-about-vpn-gateway-settings.md#gwsku) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="6bcc9-189">Als u krijgt een fout bij het maken van VPN-gateway Hallo met betrekking tot Hallo - GatewaySku, controleert u of dat u de meest recente versie van PowerShell-cmdlets Hallo Hallo hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-189">If you get an error when creating hello VPN gateway regarding hello -GatewaySku, verify that you have installed hello latest version of hello PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="6bcc9-190"><a name="ConfigureVPNDevice"></a>7. Uw VPN-apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="6bcc9-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="6bcc9-191">Site-naar-Site-verbindingen tooan on-premises netwerk een VPN-apparaat vereist.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-191">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="6bcc9-192">In deze stap configureert u het VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="6bcc9-193">Bij het configureren van uw VPN-apparaat, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="6bcc9-193">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="6bcc9-194">Een gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-194">A shared key.</span></span> <span data-ttu-id="6bcc9-195">Dit is Hallo dezelfde gedeelde sleutel die u opgeeft bij het maken van uw Site-naar-Site VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-195">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="6bcc9-196">In onze voorbeelden gebruiken we een eenvoudige gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="6bcc9-197">Het is raadzaam dat u een complexere sleutel toouse genereert.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-197">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="6bcc9-198">Hallo openbare IP-adres van uw virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-198">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="6bcc9-199">U kunt het openbare IP-adres Hallo weergeven met behulp van hello Azure-portal, PowerShell of CLI.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-199">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="6bcc9-200">toofind hello openbare IP-adres van uw virtuele netwerkgateway met behulp van PowerShell, gebruik Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="6bcc9-200">toofind hello Public IP address of your virtual network gateway using PowerShell, use hello following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="6bcc9-201"><a name="CreateConnection"></a>8. Hallo VPN-verbinding maken</span><span class="sxs-lookup"><span data-stu-id="6bcc9-201"><a name="CreateConnection"></a>8. Create hello VPN connection</span></span>

<span data-ttu-id="6bcc9-202">Maak vervolgens Hallo Site-naar-Site VPN-verbinding tussen uw virtuele netwerkgateway en uw VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-202">Next, create hello Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="6bcc9-203">Ervoor tooreplace Hallo waarden door uw eigen worden.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-203">Be sure tooreplace hello values with your own.</span></span> <span data-ttu-id="6bcc9-204">Hallo gedeelde sleutel moet overeenkomen met de Hallo-waarde die u voor de configuratie van uw VPN-apparaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-204">hello shared key must match hello value you used for your VPN device configuration.</span></span> <span data-ttu-id="6bcc9-205">U ziet dat Hallo '-ConnectionType' voor Site-naar-Site is *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-205">Notice that hello '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="6bcc9-206">Hallo-variabelen worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-206">Set hello variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="6bcc9-207">Hallo verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-207">Create hello connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="6bcc9-208">Na een korte tijd hello wordt de verbinding worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-208">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="6bcc9-209"><a name="toverify"></a>9. Hallo VPN-verbinding controleren</span><span class="sxs-lookup"><span data-stu-id="6bcc9-209"><a name="toverify"></a>9. Verify hello VPN connection</span></span>

<span data-ttu-id="6bcc9-210">Er zijn een aantal verschillende manieren tooverify uw VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-210">There are a few different ways tooverify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="6bcc9-211"><a name="connectVM"></a>tooconnect tooa virtuele machine</span><span class="sxs-lookup"><span data-stu-id="6bcc9-211"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="6bcc9-212"><a name="modify"></a>IP-adresvoorvoegsels wijzigen voor de gateway van een lokaal netwerk</span><span class="sxs-lookup"><span data-stu-id="6bcc9-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="6bcc9-213">Als Hallo IP-adresvoorvoegsels die u gerouteerd tooyour on-premises locatie wilt wijzigen, kunt u de lokale netwerkgateway Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-213">If hello IP address prefixes that you want routed tooyour on-premises location change, you can modify hello local network gateway.</span></span> <span data-ttu-id="6bcc9-214">Er zijn twee sets met instructies.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="6bcc9-215">Hallo-instructies die u kiest, is afhankelijk van of u al uw gatewayverbinding hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-215">hello instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="6bcc9-216"><a name="modifygwipaddress"></a>Hallo gateway IP-adres voor een lokale netwerkgateway wijzigen</span><span class="sxs-lookup"><span data-stu-id="6bcc9-216"><a name="modifygwipaddress"></a>Modify hello gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="6bcc9-217">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6bcc9-217">Next steps</span></span>

*  <span data-ttu-id="6bcc9-218">Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-218">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="6bcc9-219">Zie [Virtuele machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6bcc9-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="6bcc9-220">Zie voor meer informatie over BGP Hallo [BGP-overzicht](vpn-gateway-bgp-overview.md) en [hoe tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6bcc9-220">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
