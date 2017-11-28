---
title: 'Verbinding maken met uw lokale netwerk tooan virtuele Azure-netwerk: Site-naar-Site VPN: Portal | Microsoft Docs'
description: Stappen toocreate een IPsec-verbinding van uw on-premises netwerk tooan virtuele Azure-netwerk via openbaar Internet Hallo. Deze stappen kunt u een cross-premises Site-naar-Site VPN-gatewayverbinding maken met de Hallo-portal.
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
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a><span data-ttu-id="9a016-104">Een Site-naar-Site-verbinding maken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9a016-104">Create a Site-to-Site connection in hello Azure portal</span></span>

<span data-ttu-id="9a016-105">Dit artikel laat zien hoe toouse hello Azure portal toocreate een Site-naar-Site VPN-gatewayverbinding vanuit uw lokale netwerk toohello VNet.</span><span class="sxs-lookup"><span data-stu-id="9a016-105">This article shows you how toouse hello Azure portal toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="9a016-106">Hallo stappen in dit artikel van toepassing toohello Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="9a016-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="9a016-107">Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="9a016-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a016-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9a016-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="9a016-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a016-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="9a016-110">CLI</span><span class="sxs-lookup"><span data-stu-id="9a016-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="9a016-111">Azure Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="9a016-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="9a016-112">Een Site-naar-Site VPN-gatewayverbinding gebruikte tooconnect is uw on-premises netwerk tooan virtuele Azure-netwerk via een VPN-IPsec/IKE (IKEv1 of IKEv2)-tunnel.</span><span class="sxs-lookup"><span data-stu-id="9a016-112">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="9a016-113">Dit type verbinding vereist een VPN-zich on-premises apparaten met een extern gericht openbaar IP-adres toegewezen tooit.</span><span class="sxs-lookup"><span data-stu-id="9a016-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="9a016-114">Zie [Overzicht van VPN Gateway](vpn-gateway-about-vpngateways.md) voor meer informatie over VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="9a016-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagram: cross-premises site-naar-site-VPN-gatewayverbinding](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="9a016-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="9a016-116">Before you begin</span></span>

<span data-ttu-id="9a016-117">Controleer of dat u Hallo criteria volgen voordat u begint met de configuratie hebt voldaan:</span><span class="sxs-lookup"><span data-stu-id="9a016-117">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="9a016-118">Zorg ervoor dat u hebt een compatibel VPN-apparaat en iemand die dit kunnen tooconfigure deze.</span><span class="sxs-lookup"><span data-stu-id="9a016-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="9a016-119">Zie [Over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor meer informatie over compatibele VPN-apparaten en -apparaatconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="9a016-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="9a016-120">Controleer of u een extern gericht openbaar IPv4-adres voor het VPN-apparaat hebt.</span><span class="sxs-lookup"><span data-stu-id="9a016-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="9a016-121">Dit IP-adres kan zich niet achter een NAT bevinden.</span><span class="sxs-lookup"><span data-stu-id="9a016-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="9a016-122">Als u niet bekend bent met de Hallo IP-adresbereiken zich in uw on-premises netwerkconfiguratie, moet u toocoordinate met iemand die deze details voor u verstrekken kan.</span><span class="sxs-lookup"><span data-stu-id="9a016-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="9a016-123">Wanneer u deze configuratie maakt, moet u Hallo IP-bereik adresvoorvoegsels Azure routeert tooyour on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="9a016-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="9a016-124">Geen van de subnetten Hallo van uw on-premises netwerk kunnen via lap met Hallo virtueel netwerksubnetten die u wilt dat tooconnect om te.</span><span class="sxs-lookup"><span data-stu-id="9a016-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span> 

### <span data-ttu-id="9a016-125"><a name="values"></a>Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="9a016-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="9a016-126">Hallo-voorbeelden in dit artikel gebruiken Hallo waarden te volgen.</span><span class="sxs-lookup"><span data-stu-id="9a016-126">hello examples in this article use hello following values.</span></span> <span data-ttu-id="9a016-127">U kunt deze waarden toocreate een testomgeving gebruiken of toothem verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="9a016-127">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

* <span data-ttu-id="9a016-128">**VNet-naam:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="9a016-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="9a016-129">**Adresruimte:**</span><span class="sxs-lookup"><span data-stu-id="9a016-129">**Address Space:**</span></span> 
  * <span data-ttu-id="9a016-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9a016-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="9a016-131">10.12.0.0/16 (optioneel voor deze oefening)</span><span class="sxs-lookup"><span data-stu-id="9a016-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="9a016-132">**Subnetten:**</span><span class="sxs-lookup"><span data-stu-id="9a016-132">**Subnets:**</span></span>
  * <span data-ttu-id="9a016-133">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="9a016-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="9a016-134">Back-end: 10.12.0.0/24 (optioneel voor deze oefening)</span><span class="sxs-lookup"><span data-stu-id="9a016-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="9a016-135">**Gatewaysubnet**: 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="9a016-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="9a016-136">**Resourcegroep:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="9a016-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="9a016-137">**Locatie:** VS - oost</span><span class="sxs-lookup"><span data-stu-id="9a016-137">**Location:** East US</span></span>
* <span data-ttu-id="9a016-138">**DNS-server:** optioneel.</span><span class="sxs-lookup"><span data-stu-id="9a016-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="9a016-139">Hallo IP-adres van uw DNS-server.</span><span class="sxs-lookup"><span data-stu-id="9a016-139">hello IP address of your DNS server.</span></span>
* <span data-ttu-id="9a016-140">**Gatewaynaam van het virtuele netwerk:** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="9a016-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="9a016-141">**Openbare IP:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="9a016-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="9a016-142">**VPN-type:** Op route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="9a016-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="9a016-143">**Verbindingstype:** site-naar-site (IPsec)</span><span class="sxs-lookup"><span data-stu-id="9a016-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="9a016-144">**Gatewaytype:** VPN</span><span class="sxs-lookup"><span data-stu-id="9a016-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="9a016-145">**Naam van lokale netwerkgateway:** Site2</span><span class="sxs-lookup"><span data-stu-id="9a016-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="9a016-146">**Verbindingsnaam:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="9a016-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="9a016-147"><a name="CreatVNet"></a>1. Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="9a016-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="9a016-148"><a name="dns"></a>2. Een DNS-server opgeven</span><span class="sxs-lookup"><span data-stu-id="9a016-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="9a016-149">DNS is niet vereist toocreate een Site-naar-Site-verbinding.</span><span class="sxs-lookup"><span data-stu-id="9a016-149">DNS is not required toocreate a Site-to-Site connection.</span></span> <span data-ttu-id="9a016-150">Als u naamomzetting toohave voor resources die geïmplementeerd tooyour virtueel netwerk zijn wilt, moet u een DNS-server opgeven.</span><span class="sxs-lookup"><span data-stu-id="9a016-150">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="9a016-151">Deze instelling kunt u opgeven Hallo DNS-server wilt u toouse voor naamomzetting voor dit virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="9a016-151">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="9a016-152">Hierdoor wordt geen DNS-server aangemaakt.</span><span class="sxs-lookup"><span data-stu-id="9a016-152">It does not create a DNS server.</span></span> <span data-ttu-id="9a016-153">Zie [Naamomzetting voor VM's en rolinstanties](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) voor meer informatie over naamomzetting.</span><span class="sxs-lookup"><span data-stu-id="9a016-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="9a016-154"><a name="gatewaysubnet"></a>3. Hallo gatewaysubnet maken</span><span class="sxs-lookup"><span data-stu-id="9a016-154"><a name="gatewaysubnet"></a>3. Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="9a016-155"><a name="VNetGateway"></a>4. Hallo VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="9a016-155"><a name="VNetGateway"></a>4. Create hello VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="9a016-156"><a name="LocalNetworkGateway"></a>5. Hallo lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="9a016-156"><a name="LocalNetworkGateway"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="9a016-157">Hallo lokale netwerkgateway verwijst doorgaans tooyour on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="9a016-157">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="9a016-158">U geeft Hallo site een naam waarmee Azure kunt tooit verwijzen, geeft u vervolgens Hallo IP-adres van Hallo lokale VPN-apparaat toowhich maakt u een verbinding.</span><span class="sxs-lookup"><span data-stu-id="9a016-158">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="9a016-159">U wordt ook Hallo IP-adresvoorvoegsels worden doorgestuurd via Hallo VPN-gateway toohello VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9a016-159">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="9a016-160">Hallo-adresvoorvoegsels die u opgeeft voorvoegsels Hallo zich op uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="9a016-160">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="9a016-161">Als uw lokale netwerkwijzigingen of u toochange Hallo openbaar IP-adres voor Hallo VPN-apparaat moet, kunt u eenvoudig hello waarden later bijwerken.</span><span class="sxs-lookup"><span data-stu-id="9a016-161">If your on-premises network changes or you need toochange hello public IP address for hello VPN device, you can easily update hello values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="9a016-162"><a name="VPNDevice"></a>6. Uw VPN-apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="9a016-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="9a016-163">Site-naar-Site-verbindingen tooan on-premises netwerk een VPN-apparaat vereist.</span><span class="sxs-lookup"><span data-stu-id="9a016-163">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="9a016-164">In deze stap configureert u het VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9a016-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="9a016-165">Bij het configureren van uw VPN-apparaat, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="9a016-165">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="9a016-166">Een gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="9a016-166">A shared key.</span></span> <span data-ttu-id="9a016-167">Dit is Hallo dezelfde gedeelde sleutel die u opgeeft bij het maken van uw Site-naar-Site VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="9a016-167">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="9a016-168">In onze voorbeelden gebruiken we een eenvoudige gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="9a016-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="9a016-169">Het is raadzaam dat u een complexere sleutel toouse genereert.</span><span class="sxs-lookup"><span data-stu-id="9a016-169">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="9a016-170">Hallo openbare IP-adres van uw virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="9a016-170">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="9a016-171">U kunt het openbare IP-adres Hallo weergeven met behulp van hello Azure-portal, PowerShell of CLI.</span><span class="sxs-lookup"><span data-stu-id="9a016-171">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="9a016-172">toofind hello openbare IP-adres van uw VPN-gateway met behulp van hello Azure-portal te navigeren**gateways voor virtueel netwerk**, klikt u op Hallo-naam van uw gateway.</span><span class="sxs-lookup"><span data-stu-id="9a016-172">toofind hello Public IP address of your VPN gateway using hello Azure portal, navigate too**Virtual network gateways**, then click hello name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="9a016-173"><a name="CreateConnection"></a>7. Hallo VPN-verbinding maken</span><span class="sxs-lookup"><span data-stu-id="9a016-173"><a name="CreateConnection"></a>7. Create hello VPN connection</span></span>

<span data-ttu-id="9a016-174">Hallo Site-naar-Site VPN-verbinding tussen uw virtuele netwerkgateway en uw on-premises VPN-apparaat maken.</span><span class="sxs-lookup"><span data-stu-id="9a016-174">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="9a016-175"><a name="VerifyConnection"></a>8. Hallo VPN-verbinding controleren</span><span class="sxs-lookup"><span data-stu-id="9a016-175"><a name="VerifyConnection"></a>8. Verify hello VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="9a016-176"><a name="connectVM"></a>tooconnect tooa virtuele machine</span><span class="sxs-lookup"><span data-stu-id="9a016-176"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="9a016-177"><a name="reset"></a>Hoe tooreset een VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="9a016-177"><a name="reset"></a>How tooreset a VPN gateway</span></span>

<span data-ttu-id="9a016-178">Het opnieuw instellen van een Azure VPN-gateway is handig als u cross-premises VPN-connectiviteit verliest in een of meer Site-to-Site VPN-tunnels.</span><span class="sxs-lookup"><span data-stu-id="9a016-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="9a016-179">In dit geval uw on-premises VPN-apparaten zijn alle naar behoren werkt, maar er kan geen tooestablish IPsec-tunnels met hello Azure VPN-gateways zijn.</span><span class="sxs-lookup"><span data-stu-id="9a016-179">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="9a016-180">Zie [Een VPN-gateway opnieuw instellen](vpn-gateway-resetgw-classic.md) voor de stappen.</span><span class="sxs-lookup"><span data-stu-id="9a016-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="9a016-181"><a name="resize"></a>Hoe toochange een gateway-SKU (formaat een gateway)</span><span class="sxs-lookup"><span data-stu-id="9a016-181"><a name="resize"></a>How toochange a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="9a016-182">Voor Hallo toochange een gateway-SKU stappen, Zie [Gateway-SKU's](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="9a016-182">For hello steps toochange a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a016-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a016-183">Next steps</span></span>

* <span data-ttu-id="9a016-184">Zie voor meer informatie over BGP Hallo [BGP-overzicht](vpn-gateway-bgp-overview.md) en [hoe tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9a016-184">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="9a016-185">Zie [Informatie over geforceerde tunneling](vpn-gateway-forced-tunneling-rm.md) voor meer informatie over geforceerde tunneling.</span><span class="sxs-lookup"><span data-stu-id="9a016-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="9a016-186">Zie [Maximaal beschikbare cross-premises en VNet-naar-VNet-connectiviteit](vpn-gateway-highlyavailable.md) voor meer informatie over maximaal beschikbare actieve verbindingen.</span><span class="sxs-lookup"><span data-stu-id="9a016-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
