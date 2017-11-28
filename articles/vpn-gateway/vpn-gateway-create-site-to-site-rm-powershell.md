---
title: 'Uw on-premises netwerk verbinden met een virtueel Azure-netwerk: site-naar-site-VPN: PowerShell | Microsoft Docs'
description: Stappen voor het maken van een IPSec-verbinding van uw on-premises netwerk met een virtueel Azure-netwerk via het openbare internet. Deze stappen helpen u een cross-premises site-naar-site-VPN-gatewayverbinding te maken met PowerShell.
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
ms.openlocfilehash: 27f4a8fb9a83b98e99df635bf4c80f6048ce348c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="c5dd3-104">Een VNet met een site-naar-site-VPN-verbinding maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5dd3-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="c5dd3-105">In dit artikel leest u hoe u PowerShell gebruikt om een site-naar-site-VPN-gatewayverbinding te maken vanaf uw lokale netwerk naar het VNet.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-105">This article shows you how to use PowerShell to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="c5dd3-106">De stappen in dit artikel zijn van toepassing op het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="c5dd3-107">U kunt deze configuratie ook maken met een ander implementatiehulpprogramma of een ander implementatiemodel door in de volgende lijst een andere optie te selecteren:</span><span class="sxs-lookup"><span data-stu-id="c5dd3-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c5dd3-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c5dd3-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="c5dd3-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5dd3-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="c5dd3-110">CLI</span><span class="sxs-lookup"><span data-stu-id="c5dd3-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="c5dd3-111">Azure Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="c5dd3-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="c5dd3-112">Klassieke portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="c5dd3-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="c5dd3-113">Een site-naar-site-VPN-gatewayverbinding wordt gebruikt om een on-premises netwerk via een IPsec-/IKE-VPN-tunnel (IKEv1 of IKEv2) te verbinden met een virtueel Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-113">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="c5dd3-114">Voor dit type verbinding moet er on-premises een VPN-apparaat aanwezig zijn waaraan een extern openbaar IP-adres is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="c5dd3-115">Zie [Overzicht van VPN Gateway](vpn-gateway-about-vpngateways.md) voor meer informatie over VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagram: cross-premises site-naar-site-VPN-gatewayverbinding](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="c5dd3-117"><a name="before"></a>Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="c5dd3-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="c5dd3-118">Controleer voordat u met de configuratie begint of u aan de volgende criteria hebt voldaan:</span><span class="sxs-lookup"><span data-stu-id="c5dd3-118">Verify that you have met the following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="c5dd3-119">U hebt een compatibel VPN-apparaat nodig en iemand die dit kan configureren.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-119">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="c5dd3-120">Zie [Over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor meer informatie over compatibele VPN-apparaten en -apparaatconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="c5dd3-121">Controleer of u een extern gericht openbaar IPv4-adres voor het VPN-apparaat hebt.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="c5dd3-122">Dit IP-adres kan zich niet achter een NAT bevinden.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="c5dd3-123">Als u de IP-adresbereiken in uw on-premises netwerkconfiguratie niet kent, moet u contact opnemen met iemand die u hierbij kan helpen en de benodigde gegevens kan verstrekken.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-123">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="c5dd3-124">Wanneer u deze configuratie maakt, moet u de IP-adresbereikvoorvoegsels opgeven die Azure naar uw on-premises locatie doorstuurt.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-124">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="c5dd3-125">Geen van de subnetten van uw on-premises netwerk kan overlappen met de virtuele subnetten waarmee u verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-125">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span>
* <span data-ttu-id="c5dd3-126">Installeer de meest recente versie van de PowerShell-cmdlets van Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-126">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c5dd3-127">PowerShell-cmdlets worden regelmatig bijgewerkt. Doorgaans moet u PowerShell-cmdlets bijwerken om de meest recente functionaliteit op te halen.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-127">PowerShell cmdlets are updated frequently and you will typically need to update your PowerShell cmdlets to get the latest feature functionality.</span></span> <span data-ttu-id="c5dd3-128">Als u uw PowerShell-cmdlets niet bijwerkt, kunnen de opgegeven waarden mislukken.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-128">If you don't update your PowerShell cmdlets, the values specified may fail.</span></span> <span data-ttu-id="c5dd3-129">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor meer informatie over het downloaden en installeren van PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-129">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="c5dd3-130"><a name="example"></a>Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="c5dd3-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="c5dd3-131">In de voorbeelden in dit artikel worden de volgende waarden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-131">The examples in this article use the following values.</span></span> <span data-ttu-id="c5dd3-132">U kunt deze waarden gebruiken om een testomgeving te maken of ze raadplegen om meer inzicht te krijgen in de voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-132">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

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


## <span data-ttu-id="c5dd3-133"><a name="Login"></a>1. Verbinding maken met uw abonnement</span><span class="sxs-lookup"><span data-stu-id="c5dd3-133"><a name="Login"></a>1. Connect to your subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="c5dd3-134"><a name="VNet"></a>2. Een virtueel netwerk en een gatewaysubnet maken</span><span class="sxs-lookup"><span data-stu-id="c5dd3-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="c5dd3-135">Als u nog geen virtueel netwerk hebt, maakt u er een.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="c5dd3-136">Controleer bij het maken van een virtueel netwerk of de adresruimten die u opgeeft, niet overlappen met adresruimten in uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-136">When creating a virtual network, make sure that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="c5dd3-137"><a name="vnet"></a>Een virtueel netwerk en een gatewaysubnet maken</span><span class="sxs-lookup"><span data-stu-id="c5dd3-137"><a name="vnet"></a>To create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="c5dd3-138">In dit voorbeeld worden een virtueel netwerk en een gatewaysubnet gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="c5dd3-139">Zie [Een gatewaysubnet toevoegen aan een virtueel netwerk dat u al hebt gemaakt](#gatewaysubnet) als u al een virtueel netwerk hebt waaraan u een gatewaysubnet wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-139">If you already have a virtual network that you need to add a gateway subnet to, see [To add a gateway subnet to a virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="c5dd3-140">Een resourcegroep maken:</span><span class="sxs-lookup"><span data-stu-id="c5dd3-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="c5dd3-141">Maak uw virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-141">Create your virtual network.</span></span>

1. <span data-ttu-id="c5dd3-142">Stel de variabelen in.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-142">Set the variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="c5dd3-143">Maak het VNet.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-143">Create the VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="c5dd3-144"><a name="gatewaysubnet"></a>Een gatewaysubnet toevoegen aan een virtueel netwerk dat u al hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="c5dd3-144"><a name="gatewaysubnet"></a>To add a gateway subnet to a virtual network you have already created</span></span>

1. <span data-ttu-id="c5dd3-145">Stel de variabelen in.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-145">Set the variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="c5dd3-146">Maak het gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-146">Create the gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="c5dd3-147">Stel de configuratie in.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-147">Set the configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="c5dd3-148">3. <a name="localnet"></a>De lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="c5dd3-148">3. <a name="localnet"></a>Create the local network gateway</span></span>

<span data-ttu-id="c5dd3-149">De lokale netwerkgateway verwijst doorgaans naar uw on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-149">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="c5dd3-150">U geeft de site een naam waarmee Azure hiernaar kan verwijzen en geeft vervolgens het IP-adres op van het on-premises VPN-apparaat waarmee u verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-150">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="c5dd3-151">U geeft ook de IP-adresvoorvoegsels op die via de VPN-gateway worden doorgestuurd naar het VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-151">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="c5dd3-152">De adresvoorvoegsels die u opgeeft, zijn de voorvoegsels die zich in uw on-premises netwerk bevinden.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-152">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="c5dd3-153">Als uw on-premises netwerk verandert, kunt u de voorvoegsels eenvoudig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-153">If your on-premises network changes, you can easily update the prefixes.</span></span>

<span data-ttu-id="c5dd3-154">Gebruik de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="c5dd3-154">Use the following values:</span></span>

* <span data-ttu-id="c5dd3-155">*GatewayIPAddress* is het IP-adres van uw on-premises VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-155">The *GatewayIPAddress* is the IP address of your on-premises VPN device.</span></span> <span data-ttu-id="c5dd3-156">Het VPN-apparaat kan zich niet achter een NAT bevinden.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="c5dd3-157">*AddressPrefix* is uw on-premises adresruimte.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-157">The *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="c5dd3-158">Ga als volgt te werk als u een lokale netwerkgateway met één adresvoorvoegsel wilt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="c5dd3-158">To add a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="c5dd3-159">Ga als volgt te werk als u een lokale netwerkgateway met meerdere adresvoorvoegsels wilt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="c5dd3-159">To add a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="c5dd3-160">IP-adresvoorvoegsels wijzigen voor uw lokale netwerkgateway:</span><span class="sxs-lookup"><span data-stu-id="c5dd3-160">To modify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="c5dd3-161">Soms veranderen de voorvoegsels voor uw lokale netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="c5dd3-162">De stappen waarmee u de IP-adresvoorvoegsels moet wijzigen, zijn afhankelijk van het feit of u een VPN-gatewayverbinding hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-162">The steps you take to modify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="c5dd3-163">Raadpleeg de sectie [Adresvoorvoegsels voor een lokale netwerkgateway wijzigen](#modify) van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-163">See the [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="c5dd3-164"><a name="PublicIP"></a>4. Een openbaar IP-adres aanvragen</span><span class="sxs-lookup"><span data-stu-id="c5dd3-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="c5dd3-165">Een VPN Gateway moet een openbaar IP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="c5dd3-166">U vraagt eerst de resource van het IP-adres aan en verwijst hier vervolgens naar bij het maken van uw virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-166">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="c5dd3-167">Het IP-adres wordt dynamisch aan de resource toegewezen wanneer de VPN Gateway wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-167">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="c5dd3-168">VPN Gateway ondersteunt momenteel alleen *dynamische* toewijzing van openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="c5dd3-169">U kunt geen toewijzing van een statisch openbaar IP-adres aanvragen.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="c5dd3-170">Dit betekent echter niet dat het IP-adres wordt gewijzigd nadat het aan uw VPN Gateway is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-170">However, this does not mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="c5dd3-171">Het openbare IP-adres verandert alleen wanneer de gateway wordt verwijderd en opnieuw wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-171">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="c5dd3-172">Het verandert niet wanneer de grootte van uw VPN Gateway verandert, wanneer deze gateway opnieuw wordt ingesteld of wanneer andere interne onderhoudswerkzaamheden of upgrades worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="c5dd3-173">Vraag een openbaar IP-adres aan dat wordt toegewezen aan de VPN Gateway van uw virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-173">Request a Public IP address that will be assigned to your virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="c5dd3-174"><a name="GatewayIPConfig"></a>5. De IP-adresseringsconfiguratie voor de gateway maken</span><span class="sxs-lookup"><span data-stu-id="c5dd3-174"><a name="GatewayIPConfig"></a>5. Create the gateway IP addressing configuration</span></span>

<span data-ttu-id="c5dd3-175">De gatewayconfiguratie bepaalt welk subnet en openbaar IP-adres moeten worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-175">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="c5dd3-176">Gebruik het volgende voorbeeld om de gatewayconfiguratie te maken:</span><span class="sxs-lookup"><span data-stu-id="c5dd3-176">Use the following example to create your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="c5dd3-177"><a name="CreateGateway"></a>6. De VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="c5dd3-177"><a name="CreateGateway"></a>6. Create the VPN gateway</span></span>

<span data-ttu-id="c5dd3-178">Maak de VPN-gateway van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-178">Create the virtual network VPN gateway.</span></span> <span data-ttu-id="c5dd3-179">Het maken van een VPN-gateway kan 45 minuten of langer duren.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-179">Creating a VPN gateway can take up to 45 minutes or more to complete.</span></span>

<span data-ttu-id="c5dd3-180">Gebruik de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="c5dd3-180">Use the following values:</span></span>

* <span data-ttu-id="c5dd3-181">Het *-GatewayType* voor een site-naar-site-configuratie is *VPN*.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-181">The *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="c5dd3-182">Het gatewaytype is altijd specifiek voor de configuratie die u implementeert.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-182">The gateway type is always specific to the configuration that you are implementing.</span></span> <span data-ttu-id="c5dd3-183">Andere gatewayconfiguraties vereisen misschien -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="c5dd3-184">Het *-VpnType* kan *RouteBased* (in sommige documentatie een dynamische gateway genoemd) of *PolicyBased* (in sommige documentatie een statische gateway genoemd) zijn.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-184">The *-VpnType* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span></span> <span data-ttu-id="c5dd3-185">Voor meer informatie over VPN-gatewaytypen raadpleegt u [Over VPN Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="c5dd3-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="c5dd3-186">Selecteer de gateway-SKU die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-186">Select the Gateway SKU that you want to use.</span></span> <span data-ttu-id="c5dd3-187">Voor bepaalde SKU's gelden configuratiebeperkingen.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="c5dd3-188">Zie [Gateway-SKU's](vpn-gateway-about-vpn-gateway-settings.md#gwsku) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="c5dd3-189">Als er een fout optreedt bij het maken van de VPN-gateway met betrekking tot de GatewaySku, controleert u of u de nieuwste versie van de PowerShell-cmdlets hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-189">If you get an error when creating the VPN gateway regarding the -GatewaySku, verify that you have installed the latest version of the PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="c5dd3-190"><a name="ConfigureVPNDevice"></a>7. Uw VPN-apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="c5dd3-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="c5dd3-191">Voor site-naar-site-verbindingen met een on-premises netwerk is een VPN-apparaat vereist.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-191">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="c5dd3-192">In deze stap configureert u het VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="c5dd3-193">Bij de configuratie van uw VPN-apparaat hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="c5dd3-193">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="c5dd3-194">Een gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-194">A shared key.</span></span> <span data-ttu-id="c5dd3-195">Dit is dezelfde gedeelde sleutel die u opgeeft wanneer u uw site-naar-site-VPN-verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-195">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="c5dd3-196">In onze voorbeelden gebruiken we een eenvoudige gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="c5dd3-197">We raden u aan een complexere sleutel te genereren.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-197">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="c5dd3-198">Het openbare IP-adres van de gateway van uw virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-198">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="c5dd3-199">U kunt het openbare IP-adres weergeven met behulp van Azure Portal, PowerShell of de CLI.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-199">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="c5dd3-200">Gebruik het volgende voorbeeld om het openbare IP-adres van uw virtuele netwerkgateway te vinden met behulp van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c5dd3-200">To find the Public IP address of your virtual network gateway using PowerShell, use the following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="c5dd3-201"><a name="CreateConnection"></a>8. De VPN-verbinding maken</span><span class="sxs-lookup"><span data-stu-id="c5dd3-201"><a name="CreateConnection"></a>8. Create the VPN connection</span></span>

<span data-ttu-id="c5dd3-202">Maak vervolgens de site-naar-site-VPN-verbinding tussen de gateway van uw virtuele netwerk en het VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-202">Next, create the Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="c5dd3-203">Zorg dat u de waarden vervangt door die van uzelf.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-203">Be sure to replace the values with your own.</span></span> <span data-ttu-id="c5dd3-204">De gedeelde sleutel moet overeenkomen met de waarde die u hebt gebruikt voor de configuratie van uw VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-204">The shared key must match the value you used for your VPN device configuration.</span></span> <span data-ttu-id="c5dd3-205">Het '-ConnectionType' voor site-naar-site is *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-205">Notice that the '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="c5dd3-206">Stel de variabelen in.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-206">Set the variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="c5dd3-207">Maak de verbinding.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-207">Create the connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="c5dd3-208">Na een korte tijd wordt de verbinding tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-208">After a short while, the connection will be established.</span></span>

## <span data-ttu-id="c5dd3-209"><a name="toverify"></a>9. De VPN-verbinding controleren</span><span class="sxs-lookup"><span data-stu-id="c5dd3-209"><a name="toverify"></a>9. Verify the VPN connection</span></span>

<span data-ttu-id="c5dd3-210">Er zijn een aantal verschillende manieren om uw VPN-verbinding te controleren.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-210">There are a few different ways to verify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="c5dd3-211"><a name="connectVM"></a>Verbinding maken met een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c5dd3-211"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="c5dd3-212"><a name="modify"></a>IP-adresvoorvoegsels wijzigen voor de gateway van een lokaal netwerk</span><span class="sxs-lookup"><span data-stu-id="c5dd3-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="c5dd3-213">Als de IP-adresvoorvoegsels die u wilt routeren naar de locatie van uw on-premises wijzigen, kunt u de gateway van het lokale netwerk wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-213">If the IP address prefixes that you want routed to your on-premises location change, you can modify the local network gateway.</span></span> <span data-ttu-id="c5dd3-214">Er zijn twee sets met instructies.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="c5dd3-215">Welke instructies u kiest, is afhankelijk van de vraag of u uw gatewayverbinding al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-215">The instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="c5dd3-216"><a name="modifygwipaddress"></a>Het gateway-IP-adres wijzigen voor de gateway van een lokaal netwerk</span><span class="sxs-lookup"><span data-stu-id="c5dd3-216"><a name="modifygwipaddress"></a>Modify the gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c5dd3-217">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c5dd3-217">Next steps</span></span>

*  <span data-ttu-id="c5dd3-218">Wanneer de verbinding is voltooid, kunt u virtuele machines aan uw virtuele netwerken toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-218">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="c5dd3-219">Zie [Virtuele machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c5dd3-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="c5dd3-220">Voor meer informatie over BGP raadpleegt u [BGP Overview](vpn-gateway-bgp-overview.md) (BGP-overzicht) en [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md) (BGP configureren).</span><span class="sxs-lookup"><span data-stu-id="c5dd3-220">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
