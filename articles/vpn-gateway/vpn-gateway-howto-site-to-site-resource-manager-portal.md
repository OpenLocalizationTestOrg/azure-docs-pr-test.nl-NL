---
title: 'Uw on-premises netwerk verbinden met een virtueel Azure-netwerk: site-naar-site-VPN: portal | Microsoft Docs'
description: Stappen voor het maken van een IPSec-verbinding van uw on-premises netwerk met een virtueel Azure-netwerk via het openbare internet. Deze stappen helpen u een cross-premises site-naar-site-VPN-gatewayverbinding te maken met de portal.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 0dec0d3744f76a06313928197f3a5229290ba32b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-site-to-site-connection-in-the-azure-portal"></a><span data-ttu-id="7f867-104">Een site-naar-site-verbinding maken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7f867-104">Create a Site-to-Site connection in the Azure portal</span></span>

<span data-ttu-id="7f867-105">In dit artikel leest u hoe u Azure Portal gebruikt om een site-naar-site-VPN-gatewayverbinding te maken vanaf uw on-premises netwerk naar het VNet.</span><span class="sxs-lookup"><span data-stu-id="7f867-105">This article shows you how to use the Azure portal to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="7f867-106">De stappen in dit artikel zijn van toepassing op het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="7f867-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="7f867-107">U kunt deze configuratie ook maken met een ander implementatiehulpprogramma of een ander implementatiemodel door in de volgende lijst een andere optie te selecteren:</span><span class="sxs-lookup"><span data-stu-id="7f867-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f867-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7f867-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="7f867-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f867-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="7f867-110">CLI</span><span class="sxs-lookup"><span data-stu-id="7f867-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="7f867-111">Azure Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="7f867-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="7f867-112">Een site-naar-site-VPN-gatewayverbinding wordt gebruikt om een on-premises netwerk via een IPsec-/IKE-VPN-tunnel (IKEv1 of IKEv2) te verbinden met een virtueel Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="7f867-112">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="7f867-113">Voor dit type verbinding moet er on-premises een VPN-apparaat aanwezig zijn waaraan een extern openbaar IP-adres is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="7f867-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="7f867-114">Zie [Overzicht van VPN Gateway](vpn-gateway-about-vpngateways.md) voor meer informatie over VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="7f867-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagram: cross-premises site-naar-site-VPN-gatewayverbinding](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="7f867-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="7f867-116">Before you begin</span></span>

<span data-ttu-id="7f867-117">Controleer voordat u met de configuratie begint of u aan de volgende criteria hebt voldaan:</span><span class="sxs-lookup"><span data-stu-id="7f867-117">Verify that you have met the following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="7f867-118">U hebt een compatibel VPN-apparaat nodig en iemand die dit kan configureren.</span><span class="sxs-lookup"><span data-stu-id="7f867-118">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="7f867-119">Zie [Over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor meer informatie over compatibele VPN-apparaten en -apparaatconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="7f867-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="7f867-120">Controleer of u een extern gericht openbaar IPv4-adres voor het VPN-apparaat hebt.</span><span class="sxs-lookup"><span data-stu-id="7f867-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="7f867-121">Dit IP-adres kan zich niet achter een NAT bevinden.</span><span class="sxs-lookup"><span data-stu-id="7f867-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="7f867-122">Als u de IP-adresbereiken in uw on-premises netwerkconfiguratie niet kent, moet u contact opnemen met iemand die u hierbij kan helpen en de benodigde gegevens kan verstrekken.</span><span class="sxs-lookup"><span data-stu-id="7f867-122">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="7f867-123">Wanneer u deze configuratie maakt, moet u de IP-adresbereikvoorvoegsels opgeven die Azure naar uw on-premises locatie doorstuurt.</span><span class="sxs-lookup"><span data-stu-id="7f867-123">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="7f867-124">Geen van de subnetten van uw on-premises netwerk kan overlappen met de virtuele subnetten waarmee u verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="7f867-124">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span> 

### <span data-ttu-id="7f867-125"><a name="values"></a>Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="7f867-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="7f867-126">In de voorbeelden in dit artikel worden de volgende waarden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7f867-126">The examples in this article use the following values.</span></span> <span data-ttu-id="7f867-127">U kunt deze waarden gebruiken om een testomgeving te maken of ze raadplegen om meer inzicht te krijgen in de voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="7f867-127">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

* <span data-ttu-id="7f867-128">**VNet-naam:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="7f867-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="7f867-129">**Adresruimte:**</span><span class="sxs-lookup"><span data-stu-id="7f867-129">**Address Space:**</span></span> 
  * <span data-ttu-id="7f867-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="7f867-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="7f867-131">10.12.0.0/16 (optioneel voor deze oefening)</span><span class="sxs-lookup"><span data-stu-id="7f867-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="7f867-132">**Subnetten:**</span><span class="sxs-lookup"><span data-stu-id="7f867-132">**Subnets:**</span></span>
  * <span data-ttu-id="7f867-133">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="7f867-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="7f867-134">Back-end: 10.12.0.0/24 (optioneel voor deze oefening)</span><span class="sxs-lookup"><span data-stu-id="7f867-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="7f867-135">**Gatewaysubnet**: 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="7f867-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="7f867-136">**Resourcegroep:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="7f867-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="7f867-137">**Locatie:** VS - oost</span><span class="sxs-lookup"><span data-stu-id="7f867-137">**Location:** East US</span></span>
* <span data-ttu-id="7f867-138">**DNS-server:** optioneel.</span><span class="sxs-lookup"><span data-stu-id="7f867-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="7f867-139">Het IP-adres van de DNS-server.</span><span class="sxs-lookup"><span data-stu-id="7f867-139">The IP address of your DNS server.</span></span>
* <span data-ttu-id="7f867-140">**Gatewaynaam van het virtuele netwerk:** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="7f867-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="7f867-141">**Openbare IP:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="7f867-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="7f867-142">**VPN-type:** Op route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="7f867-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="7f867-143">**Verbindingstype:** site-naar-site (IPsec)</span><span class="sxs-lookup"><span data-stu-id="7f867-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="7f867-144">**Gatewaytype:** VPN</span><span class="sxs-lookup"><span data-stu-id="7f867-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="7f867-145">**Naam van lokale netwerkgateway:** Site2</span><span class="sxs-lookup"><span data-stu-id="7f867-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="7f867-146">**Verbindingsnaam:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="7f867-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="7f867-147"><a name="CreatVNet"></a>1. Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="7f867-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="7f867-148"><a name="dns"></a>2. Een DNS-server opgeven</span><span class="sxs-lookup"><span data-stu-id="7f867-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="7f867-149">DNS is niet vereist om site-naar-site-verbindingen te maken.</span><span class="sxs-lookup"><span data-stu-id="7f867-149">DNS is not required to create a Site-to-Site connection.</span></span> <span data-ttu-id="7f867-150">Als u echter naamomzetting wilt instellen voor resources die in uw virtuele netwerk worden geïmplementeerd, moet u een DNS-server opgeven.</span><span class="sxs-lookup"><span data-stu-id="7f867-150">However, if you want to have name resolution for resources that are deployed to your virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="7f867-151">Met deze instelling kunt u de DNS-server opgeven die u wilt gebruiken voor de naamomzetting voor dit virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="7f867-151">This setting lets you specify the DNS server that you want to use for name resolution for this virtual network.</span></span> <span data-ttu-id="7f867-152">Hierdoor wordt geen DNS-server aangemaakt.</span><span class="sxs-lookup"><span data-stu-id="7f867-152">It does not create a DNS server.</span></span> <span data-ttu-id="7f867-153">Zie [Naamomzetting voor VM's en rolinstanties](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) voor meer informatie over naamomzetting.</span><span class="sxs-lookup"><span data-stu-id="7f867-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="7f867-154"><a name="gatewaysubnet"></a>3. Her gatewaysubnet maken</span><span class="sxs-lookup"><span data-stu-id="7f867-154"><a name="gatewaysubnet"></a>3. Create the gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="7f867-155"><a name="VNetGateway"></a>4. De VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="7f867-155"><a name="VNetGateway"></a>4. Create the VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="7f867-156"><a name="LocalNetworkGateway"></a>5. De lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="7f867-156"><a name="LocalNetworkGateway"></a>5. Create the local network gateway</span></span>

<span data-ttu-id="7f867-157">De lokale netwerkgateway verwijst doorgaans naar uw on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="7f867-157">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="7f867-158">U geeft de site een naam waarmee Azure hiernaar kan verwijzen en geeft vervolgens het IP-adres op van het on-premises VPN-apparaat waarmee u verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="7f867-158">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="7f867-159">U geeft ook de IP-adresvoorvoegsels op die via de VPN-gateway worden doorgestuurd naar het VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7f867-159">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="7f867-160">De adresvoorvoegsels die u opgeeft, zijn de voorvoegsels die zich in uw on-premises netwerk bevinden.</span><span class="sxs-lookup"><span data-stu-id="7f867-160">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="7f867-161">Als uw on-premises netwerk verandert of als u het openbare IP-adres voor het VPN-apparaat moet wijzigen, kunt u de waarden later eenvoudig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7f867-161">If your on-premises network changes or you need to change the public IP address for the VPN device, you can easily update the values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="7f867-162"><a name="VPNDevice"></a>6. Uw VPN-apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="7f867-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="7f867-163">Voor site-naar-site-verbindingen met een on-premises netwerk is een VPN-apparaat vereist.</span><span class="sxs-lookup"><span data-stu-id="7f867-163">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="7f867-164">In deze stap configureert u het VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7f867-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="7f867-165">Bij de configuratie van uw VPN-apparaat hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="7f867-165">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="7f867-166">Een gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="7f867-166">A shared key.</span></span> <span data-ttu-id="7f867-167">Dit is dezelfde gedeelde sleutel die u opgeeft wanneer u uw site-naar-site-VPN-verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="7f867-167">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="7f867-168">In onze voorbeelden gebruiken we een eenvoudige gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="7f867-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="7f867-169">We raden u aan een complexere sleutel te genereren.</span><span class="sxs-lookup"><span data-stu-id="7f867-169">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="7f867-170">Het openbare IP-adres van de gateway van uw virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="7f867-170">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="7f867-171">U kunt het openbare IP-adres weergeven met behulp van Azure Portal, PowerShell of de CLI.</span><span class="sxs-lookup"><span data-stu-id="7f867-171">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="7f867-172">Navigeer naar **Virtuele netwerkgateways** en klik op de naam van uw VPN-gateway om het openbare IP-adres dat gebruikmaakt van Azure Portal te achterhalen.</span><span class="sxs-lookup"><span data-stu-id="7f867-172">To find the Public IP address of your VPN gateway using the Azure portal, navigate to **Virtual network gateways**, then click the name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="7f867-173"><a name="CreateConnection"></a>7. De VPN-verbinding maken</span><span class="sxs-lookup"><span data-stu-id="7f867-173"><a name="CreateConnection"></a>7. Create the VPN connection</span></span>

<span data-ttu-id="7f867-174">Maak de site-naar-site-VPN-verbinding tussen de gateway van uw virtuele netwerk en het on-premises VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7f867-174">Create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="7f867-175"><a name="VerifyConnection"></a>8. De VPN-verbinding controleren</span><span class="sxs-lookup"><span data-stu-id="7f867-175"><a name="VerifyConnection"></a>8. Verify the VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="7f867-176"><a name="connectVM"></a>Verbinding maken met een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="7f867-176"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="7f867-177"><a name="reset"></a>Een VPN-gateway opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="7f867-177"><a name="reset"></a>How to reset a VPN gateway</span></span>

<span data-ttu-id="7f867-178">Het opnieuw instellen van een Azure VPN-gateway is handig als u cross-premises VPN-connectiviteit verliest in een of meer Site-to-Site VPN-tunnels.</span><span class="sxs-lookup"><span data-stu-id="7f867-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="7f867-179">In een dergelijke situatie functioneren al uw on-premises VPN-apparaten naar behoren, maar kunnen ze geen IPSec-tunnels tot stand brengen met de Azure VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="7f867-179">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="7f867-180">Zie [Een VPN-gateway opnieuw instellen](vpn-gateway-resetgw-classic.md) voor de stappen.</span><span class="sxs-lookup"><span data-stu-id="7f867-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="7f867-181"><a name="resize"></a>Een gateway-SKU wijzigen (formaat van een gateway wijzigen)</span><span class="sxs-lookup"><span data-stu-id="7f867-181"><a name="resize"></a>How to change a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="7f867-182">Zie [Gateway-SKU's](vpn-gateway-about-vpn-gateway-settings.md#gwsku) voor de stappen voor het wijzigen van een gateway-SKU.</span><span class="sxs-lookup"><span data-stu-id="7f867-182">For the steps to change a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f867-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f867-183">Next steps</span></span>

* <span data-ttu-id="7f867-184">Voor meer informatie over BGP raadpleegt u [BGP Overview](vpn-gateway-bgp-overview.md) (BGP-overzicht) en [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md) (BGP configureren).</span><span class="sxs-lookup"><span data-stu-id="7f867-184">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="7f867-185">Zie [Informatie over geforceerde tunneling](vpn-gateway-forced-tunneling-rm.md) voor meer informatie over geforceerde tunneling.</span><span class="sxs-lookup"><span data-stu-id="7f867-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="7f867-186">Zie [Maximaal beschikbare cross-premises en VNet-naar-VNet-connectiviteit](vpn-gateway-highlyavailable.md) voor meer informatie over maximaal beschikbare actieve verbindingen.</span><span class="sxs-lookup"><span data-stu-id="7f867-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
