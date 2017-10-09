---
title: 'Verbinding maken met Azure VPN-gateways toomultiple on-premises op beleid gebaseerde VPN-apparaten: Azure Resource Manager: PowerShell | Microsoft Docs'
description: In dit artikel begeleidt u bij het configureren van Azure op route gebaseerde VPN-gateway toomultiple op beleid gebaseerde VPN-apparaten met Azure Resource Manager en PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="1031e-103">Verbinding maken met Azure VPN-gateways toomultiple on-premises op beleid gebaseerde VPN-apparaten met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="1031e-103">Connect Azure VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="1031e-104">In dit artikel helpt u bij het configureren van een Azure op route gebaseerde VPN-gateway tooconnect toomultiple on-premises op beleid gebaseerde VPN-apparaten gebruik te maken van aangepaste IPsec/IKE-beleidsregels voor S2S-VPN-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="1031e-104">This article helps you configure an Azure route-based VPN gateway tooconnect toomultiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="1031e-105">Over op beleid gebaseerd en op route gebaseerde VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="1031e-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="1031e-106">Beleid - *versus* op route gebaseerde VPN-apparaten in hoe Hallo IPsec verkeer selectoren zijn ingesteld op een verbinding verschillen:</span><span class="sxs-lookup"><span data-stu-id="1031e-106">Policy- *vs.* route-based VPN devices differ in how hello IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="1031e-107">**Op basis van beleid** VPN-apparaten gebruiken Hallo combinaties van voorvoegsels van beide netwerken toodefine hoe verkeer wordt versleuteld/ontsleuteld via IPsec-tunnels.</span><span class="sxs-lookup"><span data-stu-id="1031e-107">**Policy-based** VPN devices use hello combinations of prefixes from both networks toodefine how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="1031e-108">Dit wordt gewoonlijk samengesteld op de firewallapparaten wordt uitgevoerd met het filteren van netwerkpakketten.</span><span class="sxs-lookup"><span data-stu-id="1031e-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="1031e-109">IPSec-tunnel versleuteling en ontsleuteling toegevoegd toohello pakketfilters en verwerkingsengine.</span><span class="sxs-lookup"><span data-stu-id="1031e-109">IPsec tunnel encryption and decryption are added toohello packet filtering and processing engine.</span></span>
* <span data-ttu-id="1031e-110">**Op route gebaseerde** VPN-apparaten gebruiken any-to-any (jokertekens) verkeer selectoren en laat routering/doorsturen tabellen direct verkeer toodifferent IPSec-tunnels.</span><span class="sxs-lookup"><span data-stu-id="1031e-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic toodifferent IPsec tunnels.</span></span> <span data-ttu-id="1031e-111">Dit wordt gewoonlijk samengesteld op router platforms waarbij elke IPsec-tunnel is gemodelleerd als een netwerkinterface of VTI (virtuele tunnelinterface).</span><span class="sxs-lookup"><span data-stu-id="1031e-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="1031e-112">Hallo markeren volgende diagrammen Hallo twee modellen:</span><span class="sxs-lookup"><span data-stu-id="1031e-112">hello following diagrams highlight hello two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="1031e-113">Op beleid gebaseerde VPN-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1031e-113">Policy-based VPN example</span></span>
![op basis van beleid](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="1031e-115">Op route gebaseerde VPN-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1031e-115">Route-based VPN example</span></span>
![op route gebaseerd](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="1031e-117">Azure-ondersteuning voor VPN op basis van beleid</span><span class="sxs-lookup"><span data-stu-id="1031e-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="1031e-118">Azure ondersteunt momenteel, beide modi van VPN-gateways: op route gebaseerde VPN-gateways en op beleid gebaseerde VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="1031e-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="1031e-119">Ze zijn gebaseerd op verschillende interne platforms, ertoe leiden dat andere specificaties:</span><span class="sxs-lookup"><span data-stu-id="1031e-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="1031e-120">**Beleid gebaseerd VPN-Gateway**</span><span class="sxs-lookup"><span data-stu-id="1031e-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="1031e-121">**Op route gebaseerd VPN-Gateway**</span><span class="sxs-lookup"><span data-stu-id="1031e-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="1031e-122">**Azure-Gateway SKU**</span><span class="sxs-lookup"><span data-stu-id="1031e-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="1031e-123">Basic</span><span class="sxs-lookup"><span data-stu-id="1031e-123">Basic</span></span>                       | <span data-ttu-id="1031e-124">Basic, Standard, HighPerformance</span><span class="sxs-lookup"><span data-stu-id="1031e-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="1031e-125">**IKE-versie**</span><span class="sxs-lookup"><span data-stu-id="1031e-125">**IKE version**</span></span>          | <span data-ttu-id="1031e-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="1031e-126">IKEv1</span></span>                       | <span data-ttu-id="1031e-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="1031e-127">IKEv2</span></span>                                    |
| <span data-ttu-id="1031e-128">**Max. S2S-verbindingen**</span><span class="sxs-lookup"><span data-stu-id="1031e-128">**Max. S2S connections**</span></span> | <span data-ttu-id="1031e-129">**1**</span><span class="sxs-lookup"><span data-stu-id="1031e-129">**1**</span></span>                       | <span data-ttu-id="1031e-130">Basic-/ Standard: 10</span><span class="sxs-lookup"><span data-stu-id="1031e-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="1031e-131">HighPerformance: 30</span><span class="sxs-lookup"><span data-stu-id="1031e-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="1031e-132">Hallo aangepaste IPsec/IKE-beleid, kunt u nu Azure op route gebaseerde VPN-gateways toouse verkeer op basis van het voorvoegsel selectoren met optie configureren '**PolicyBasedTrafficSelectors**', tooconnect tooon-premises op beleid gebaseerde VPN-apparaten.</span><span class="sxs-lookup"><span data-stu-id="1031e-132">With hello custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways toouse prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", tooconnect tooon-premises policy-based VPN devices.</span></span> <span data-ttu-id="1031e-133">Op deze manier kunt u tooconnect van een virtuele Azure-netwerk en VPN-gateway toomultiple on-premises VPN-/ firewall-apparaten op basis van beleid, Hallo één verbindingslimiet verwijderen uit Hallo huidige Azure op beleid gebaseerde VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="1031e-133">This capability allows you tooconnect from an Azure virtual network and VPN gateway toomultiple on-premises policy-based VPN/firewall devices, removing hello single connection limit from hello current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="1031e-134">tooenable deze connectiviteit uw on-premises op beleid gebaseerde VPN-apparaten moeten ondersteunen **IKEv2** tooconnect toohello Azure op route gebaseerde VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="1031e-134">tooenable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** tooconnect toohello Azure route-based VPN gateways.</span></span> <span data-ttu-id="1031e-135">Raadpleeg de specificaties van uw VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="1031e-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="1031e-136">Hallo on-premises netwerken verbinding maken via VPN-apparaten op basis van beleid met deze methode kunnen alleen verbinding maken met toohello virtuele Azure-netwerk; **ze tooother on-premises netwerken kunnen niet doorvoer of virtuele netwerken via dezelfde Azure VPN-gateway Hallo**.</span><span class="sxs-lookup"><span data-stu-id="1031e-136">hello on-premises networks connecting through policy-based VPN devices with this mechanism can only connect toohello Azure virtual network; **they cannot transit tooother on-premises networks or virtual networks via hello same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="1031e-137">de configuratieoptie Hallo maakt deel uit van aangepaste IPsec/IKE-verbindingsbeleid Hallo.</span><span class="sxs-lookup"><span data-stu-id="1031e-137">hello configuration option is part of hello custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="1031e-138">Als u Hallo verkeer op basis van beleid selector-optie inschakelt, moet u de volledige beleid Hallo (IPsec/IKE-algoritmen voor versleuteling en integriteit, kracht en SA-levensduur) opgeven.</span><span class="sxs-lookup"><span data-stu-id="1031e-138">If you enable hello policy-based traffic selector option, you must specify hello complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="1031e-139">Hallo volgende diagram ziet waarom transitroutering via Azure VPN-gateway werkt niet met op beleid gebaseerde Hallo-optie:</span><span class="sxs-lookup"><span data-stu-id="1031e-139">hello following diagram shows why transit routing via Azure VPN gateway doesn't work with hello policy-based option:</span></span>

![doorvoer op basis van beleid](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="1031e-141">Zoals u in het diagram hello, heeft hello Azure VPN-gateway verkeer selectoren van Hallo virtueel netwerk tooeach van Hallo-voorvoegsels voor lokale netwerk, maar niet de voorvoegsels van Hallo-cross-verbinding.</span><span class="sxs-lookup"><span data-stu-id="1031e-141">As shown in hello diagram, hello Azure VPN gateway has traffic selectors from hello virtual network tooeach of hello on-premises network prefixes, but not hello cross-connection prefixes.</span></span> <span data-ttu-id="1031e-142">Kan elk communiceren tooVNet1 respectievelijk maar kan geen verbinding maken via hello Azure VPN-gateway tooeach andere bijvoorbeeld lokale site 2, 3, en site 4.</span><span class="sxs-lookup"><span data-stu-id="1031e-142">For example, on-premises site 2, site 3, and site 4 can each communicate tooVNet1 respectively, but cannot connect via hello Azure VPN gateway tooeach other.</span></span> <span data-ttu-id="1031e-143">Hallo diagram ziet u Hallo verkeer selectoren die niet beschikbaar in hello Azure VPN-gateway in deze configuratie cross-verbinding.</span><span class="sxs-lookup"><span data-stu-id="1031e-143">hello diagram shows hello cross-connect traffic selectors that are not available in hello Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="1031e-144">Op beleid gebaseerde verkeer selectoren configureren op een verbinding</span><span class="sxs-lookup"><span data-stu-id="1031e-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="1031e-145">Hallo instructies in dit artikel volgen Hallo dezelfde voorbeeld zoals beschreven in [configureren IPsec/IKE-beleid voor S2S of VNet-naar-VNet-verbindingen](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish een S2S VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="1031e-145">hello instructions in this article follow hello same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish a S2S VPN connection.</span></span> <span data-ttu-id="1031e-146">Dit wordt weergegeven in het volgende diagram Hallo:</span><span class="sxs-lookup"><span data-stu-id="1031e-146">This is shown in hello following diagram:</span></span>

![s2s-beleid](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="1031e-148">Hallo werkstroom tooenable deze connectiviteit:</span><span class="sxs-lookup"><span data-stu-id="1031e-148">hello workflow tooenable this connectivity:</span></span>
1. <span data-ttu-id="1031e-149">Hallo virtueel netwerk, VPN-gateway en de lokale netwerkgateway voor uw cross-premises-verbinding maken</span><span class="sxs-lookup"><span data-stu-id="1031e-149">Create hello virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="1031e-150">Een IPsec/IKE-beleid maken</span><span class="sxs-lookup"><span data-stu-id="1031e-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="1031e-151">Hallo-beleid toepassen wanneer u een S2S- of VNet-naar-VNet-verbinding maakt en **inschakelen Hallo verkeer op basis van beleid selectoren** op Hallo-verbinding</span><span class="sxs-lookup"><span data-stu-id="1031e-151">Apply hello policy when you create a S2S or VNet-to-VNet connection, and **enable hello policy-based traffic selectors** on hello connection</span></span>
4. <span data-ttu-id="1031e-152">Als al Hallo verbinding is gemaakt, kunt u toepassen of Hallo beleid tooan bestaande verbinding bijwerken</span><span class="sxs-lookup"><span data-stu-id="1031e-152">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="1031e-153">Op beleid gebaseerde verkeer selectoren op een verbinding inschakelen</span><span class="sxs-lookup"><span data-stu-id="1031e-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="1031e-154">Zorg ervoor dat u hebt voltooid [deel 3 van Hallo configureren IPsec/IKE-beleid artikel](vpn-gateway-ipsecikepolicy-rm-powershell.md) voor deze sectie.</span><span class="sxs-lookup"><span data-stu-id="1031e-154">Make sure you have completed [Part 3 of hello Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="1031e-155">Hallo wordt na Hallo dezelfde parameters en stappen:</span><span class="sxs-lookup"><span data-stu-id="1031e-155">hello following example uses hello same parameters and steps:</span></span>

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="1031e-156">Stap 1: Hallo virtueel netwerk, VPN-gateway en de lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="1031e-156">Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a><span data-ttu-id="1031e-157">1. De variabelen declareren & tooyour abonnement verbinding</span><span class="sxs-lookup"><span data-stu-id="1031e-157">1. Declare your variables & connect tooyour subscription</span></span>
<span data-ttu-id="1031e-158">Voor deze oefening eerst we onze variabelen declareren.</span><span class="sxs-lookup"><span data-stu-id="1031e-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="1031e-159">Ervoor tooreplace Hallo waarden door uw eigen worden wanneer u configureert voor productie.</span><span class="sxs-lookup"><span data-stu-id="1031e-159">Be sure tooreplace hello values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
<span data-ttu-id="1031e-160">toouse hello Resource Manager-cmdlets, zorg ervoor dat u overschakelt naar tooPowerShell modus.</span><span class="sxs-lookup"><span data-stu-id="1031e-160">toouse hello Resource Manager cmdlets, make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="1031e-161">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1031e-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="1031e-162">Open de PowerShell-console en tooyour-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="1031e-162">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="1031e-163">Gebruik Hallo volgende steekproef toohelp die u verbinding kunt maken:</span><span class="sxs-lookup"><span data-stu-id="1031e-163">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="1031e-164">2. Hallo virtueel netwerk, VPN-gateway en de lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="1031e-164">2. Create hello virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="1031e-165">Hallo volgende voorbeeld maakt Hallo virtueel netwerk TestVNet1 met drie subnetten en Hallo VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="1031e-165">hello following example creates hello virtual network, TestVNet1 with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="1031e-166">Bij het vervangen van waarden, is het belangrijk dat u altijd de naam het gatewaysubnet bijzonder GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="1031e-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="1031e-167">Als u een andere naam kiest, mislukt het maken van de gateway.</span><span class="sxs-lookup"><span data-stu-id="1031e-167">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="1031e-168">Stap 2: een S2S VPN-verbinding maken met een IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="1031e-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="1031e-169">1. Een IPsec/IKE-beleid maken</span><span class="sxs-lookup"><span data-stu-id="1031e-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1031e-170">U moet een beleid voor IPsec/IKE in volgorde tooenable 'UsePolicyBasedTrafficSelectors' optie op Hallo verbinding toocreate.</span><span class="sxs-lookup"><span data-stu-id="1031e-170">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="1031e-171">Hallo volgende voorbeeld wordt een IPsec/IKE-beleid met deze algoritmen en parameters:</span><span class="sxs-lookup"><span data-stu-id="1031e-171">hello following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="1031e-172">IKEv2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="1031e-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="1031e-173">IPsec: AES256, SHA256, PFS24, SA levensduur 3600 seconden & 2048KB</span><span class="sxs-lookup"><span data-stu-id="1031e-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="1031e-174">2. Hallo S2S VPN-verbinding maken met op beleid gebaseerde verkeer selectoren en IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="1031e-174">2. Create hello S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="1031e-175">Een S2S VPN-verbinding maken en toepassen van Hallo IPsec/IKE-beleid in de vorige stap Hallo hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1031e-175">Create an S2S VPN connection and apply hello IPsec/IKE policy created in hello previous step.</span></span> <span data-ttu-id="1031e-176">Houd rekening met de extra parameter Hallo '-UsePolicyBasedTrafficSelectors $True ' waarmee verkeer op basis van beleid selectoren op Hallo-verbinding.</span><span class="sxs-lookup"><span data-stu-id="1031e-176">Be aware of hello additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on hello connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="1031e-177">Na het voltooien van Hallo stappen wordt Hallo S2S VPN-verbinding gebruik Hallo IPsec/IKE-beleid is gedefinieerd, en schakel verkeer op basis van beleid selectoren op Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="1031e-177">After completing hello steps, hello S2S VPN connection will use hello IPsec/IKE policy defined, and enable policy-based traffic selectors on hello connection.</span></span> <span data-ttu-id="1031e-178">U kunt dezelfde tooadd meer verbindingen tooadditional on-premises op beleid gebaseerde VPN-apparaten van stappen Hallo herhalen Hallo dezelfde Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="1031e-178">You can repeat hello same steps tooadd more connections tooadditional on-premises policy-based VPN devices from hello same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="1031e-179">Selectoren verkeer op basis van beleid voor een verbinding bijwerken</span><span class="sxs-lookup"><span data-stu-id="1031e-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="1031e-180">de laatste sectie Hallo ziet u hoe tooupdate Hallo verkeer op basis van beleid Selector optie voor een bestaande S2S VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="1031e-180">hello last section shows you how tooupdate hello policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-hello-connection"></a><span data-ttu-id="1031e-181">1. Hallo-verbinding ophalen</span><span class="sxs-lookup"><span data-stu-id="1031e-181">1. Get hello connection</span></span>
<span data-ttu-id="1031e-182">Hallo verbindingsbron ophalen.</span><span class="sxs-lookup"><span data-stu-id="1031e-182">Get hello connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a><span data-ttu-id="1031e-183">2. Hallo-verkeer op basis van beleid Selector optie controleren</span><span class="sxs-lookup"><span data-stu-id="1031e-183">2. Check hello policy-based traffic selectors option</span></span>
<span data-ttu-id="1031e-184">Hallo geeft volgende regel aan of Hallo verkeer op basis van beleid selectoren worden gebruikt voor Hallo verbinding:</span><span class="sxs-lookup"><span data-stu-id="1031e-184">hello following line shows whether hello policy-based traffic selectors are used for hello connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="1031e-185">Als Hallo regel retourneert '**True**', vervolgens selectoren verkeer op basis van beleid worden geconfigureerd op Hallo verbinding; anders wordt '**False**. "</span><span class="sxs-lookup"><span data-stu-id="1031e-185">If hello line returns "**True**", then policy-based traffic selectors are configured on hello connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="1031e-186">3. Hallo-verkeer op basis van beleid selectoren op een verbinding bijwerken</span><span class="sxs-lookup"><span data-stu-id="1031e-186">3. Update hello policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="1031e-187">Zodra u Hallo verbindingsbron hebt verkregen, kunt u in- of uitschakelen van Hallo-optie.</span><span class="sxs-lookup"><span data-stu-id="1031e-187">Once you obtain hello connection resource, you can enable or disable hello option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="1031e-188">UsePolicyBasedTrafficSelectors uitschakelen</span><span class="sxs-lookup"><span data-stu-id="1031e-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="1031e-189">Hello volgende voorbeeld wordt uitgeschakeld Hallo verkeer op basis van beleid Selector optie, maar blijft Hallo ongewijzigd IPsec/IKE-beleid:</span><span class="sxs-lookup"><span data-stu-id="1031e-189">hello following example disables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="1031e-190">UsePolicyBasedTrafficSelectors inschakelen</span><span class="sxs-lookup"><span data-stu-id="1031e-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="1031e-191">Hallo volgende voorbeeld wordt Hallo verkeer op basis van beleid Selector-optie ingeschakeld, maar blijft Hallo ongewijzigd IPsec/IKE-beleid:</span><span class="sxs-lookup"><span data-stu-id="1031e-191">hello following example enables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="1031e-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1031e-192">Next steps</span></span>
<span data-ttu-id="1031e-193">Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1031e-193">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="1031e-194">Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.</span><span class="sxs-lookup"><span data-stu-id="1031e-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="1031e-195">Bekijk ook [configureren IPsec/IKE-beleid voor S2S-VPN- of VNet-naar-VNet-verbindingen](vpn-gateway-ipsecikepolicy-rm-powershell.md) voor meer informatie over aangepaste IPsec/IKE-beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="1031e-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
