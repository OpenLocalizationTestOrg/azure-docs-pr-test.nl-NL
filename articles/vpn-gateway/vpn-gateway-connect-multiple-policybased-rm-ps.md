---
title: 'Verbinding maken met Azure VPN-gateways u meerdere on-premises op beleid gebaseerde VPN-apparaten: Azure Resource Manager: PowerShell | Microsoft Docs'
description: In dit artikel begeleidt u bij het configureren van Azure op route gebaseerde VPN-gateway niet meerdere op beleid gebaseerde VPN-apparaten met behulp van Azure Resource Manager en PowerShell.
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
ms.openlocfilehash: 17211379ec61891982a02efca6730ca0da87c1ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-azure-vpn-gateways-to-multiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="456ea-103">Verbinding maken met Azure VPN-gateways u meerdere on-premises op beleid gebaseerde VPN-apparaten met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="456ea-103">Connect Azure VPN gateways to multiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="456ea-104">In dit artikel helpt u bij het configureren van een Azure op route gebaseerde VPN-gateway verbinding maken met meerdere on-premises op beleid gebaseerde VPN-apparaten gebruik te maken van aangepaste IPsec/IKE-beleidsregels voor S2S-VPN-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="456ea-104">This article helps you configure an Azure route-based VPN gateway to connect to multiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="456ea-105">Over op beleid gebaseerd en op route gebaseerde VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="456ea-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="456ea-106">Beleid - *versus* op route gebaseerde VPN-apparaten in hoe de IPSec-verkeer selectoren zijn ingesteld op een verbinding verschillen:</span><span class="sxs-lookup"><span data-stu-id="456ea-106">Policy- *vs.* route-based VPN devices differ in how the IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="456ea-107">**Op basis van beleid** VPN-apparaten de combinaties van voorvoegsels van beide netwerken gebruiken om te definiëren hoe verkeer wordt versleuteld/ontsleuteld via IPsec-tunnels.</span><span class="sxs-lookup"><span data-stu-id="456ea-107">**Policy-based** VPN devices use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="456ea-108">Dit wordt gewoonlijk samengesteld op de firewallapparaten wordt uitgevoerd met het filteren van netwerkpakketten.</span><span class="sxs-lookup"><span data-stu-id="456ea-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="456ea-109">IPSec-tunnel versleuteling en ontsleuteling worden toegevoegd aan het pakket voor het filteren en het verwerken van de engine.</span><span class="sxs-lookup"><span data-stu-id="456ea-109">IPsec tunnel encryption and decryption are added to the packet filtering and processing engine.</span></span>
* <span data-ttu-id="456ea-110">**Op route gebaseerde** VPN-apparaten gebruiken any-to-any (jokertekens) verkeer selectoren en IPsec-tunnels laten direct verkeer naar andere tabellen routering/doorsturen.</span><span class="sxs-lookup"><span data-stu-id="456ea-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels.</span></span> <span data-ttu-id="456ea-111">Dit wordt gewoonlijk samengesteld op router platforms waarbij elke IPsec-tunnel is gemodelleerd als een netwerkinterface of VTI (virtuele tunnelinterface).</span><span class="sxs-lookup"><span data-stu-id="456ea-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="456ea-112">De volgende diagrammen Markeer twee modellen:</span><span class="sxs-lookup"><span data-stu-id="456ea-112">The following diagrams highlight the two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="456ea-113">Op beleid gebaseerde VPN-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="456ea-113">Policy-based VPN example</span></span>
![op basis van beleid](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="456ea-115">Op route gebaseerde VPN-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="456ea-115">Route-based VPN example</span></span>
![op route gebaseerd](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="456ea-117">Azure-ondersteuning voor VPN op basis van beleid</span><span class="sxs-lookup"><span data-stu-id="456ea-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="456ea-118">Azure ondersteunt momenteel, beide modi van VPN-gateways: op route gebaseerde VPN-gateways en op beleid gebaseerde VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="456ea-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="456ea-119">Ze zijn gebaseerd op verschillende interne platforms, ertoe leiden dat andere specificaties:</span><span class="sxs-lookup"><span data-stu-id="456ea-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="456ea-120">**Beleid gebaseerd VPN-Gateway**</span><span class="sxs-lookup"><span data-stu-id="456ea-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="456ea-121">**Op route gebaseerd VPN-Gateway**</span><span class="sxs-lookup"><span data-stu-id="456ea-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="456ea-122">**Azure-Gateway SKU**</span><span class="sxs-lookup"><span data-stu-id="456ea-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="456ea-123">Basic</span><span class="sxs-lookup"><span data-stu-id="456ea-123">Basic</span></span>                       | <span data-ttu-id="456ea-124">Basic, Standard, HighPerformance</span><span class="sxs-lookup"><span data-stu-id="456ea-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="456ea-125">**IKE-versie**</span><span class="sxs-lookup"><span data-stu-id="456ea-125">**IKE version**</span></span>          | <span data-ttu-id="456ea-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="456ea-126">IKEv1</span></span>                       | <span data-ttu-id="456ea-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="456ea-127">IKEv2</span></span>                                    |
| <span data-ttu-id="456ea-128">**Max. S2S-verbindingen**</span><span class="sxs-lookup"><span data-stu-id="456ea-128">**Max. S2S connections**</span></span> | <span data-ttu-id="456ea-129">**1**</span><span class="sxs-lookup"><span data-stu-id="456ea-129">**1**</span></span>                       | <span data-ttu-id="456ea-130">Basic-/ Standard: 10</span><span class="sxs-lookup"><span data-stu-id="456ea-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="456ea-131">HighPerformance: 30</span><span class="sxs-lookup"><span data-stu-id="456ea-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="456ea-132">Het aangepaste IPsec/IKE-beleid, kunt u nu Azure op route gebaseerde VPN-gateways voor het gebruik van selectoren verkeer op basis van het voorvoegsel met de optie configureren '**PolicyBasedTrafficSelectors**', verbinding maken met on-premises op beleid gebaseerde VPN-apparaten.</span><span class="sxs-lookup"><span data-stu-id="456ea-132">With the custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways to use prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", to connect to on-premises policy-based VPN devices.</span></span> <span data-ttu-id="456ea-133">Deze manier kunt u verbinding maken vanaf een virtuele Azure-netwerk en VPN-gateway naar meerdere on-premises VPN-/ firewall-apparaten op basis van beleid, de limiet van één verbinding verwijderen uit de huidige Azure op beleid gebaseerde VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="456ea-133">This capability allows you to connect from an Azure virtual network and VPN gateway to multiple on-premises policy-based VPN/firewall devices, removing the single connection limit from the current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="456ea-134">Schakel deze connectiviteit door uw on-premises op beleid gebaseerde VPN-apparaten moeten ondersteunen **IKEv2** verbinding maken met de Azure op route gebaseerde VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="456ea-134">To enable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** to connect to the Azure route-based VPN gateways.</span></span> <span data-ttu-id="456ea-135">Raadpleeg de specificaties van uw VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="456ea-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="456ea-136">De on-premises netwerken verbinding maken via de VPN-apparaten op basis van beleid met dit mechanisme, kunnen u alleen verbinding maken met Azure virtual network; **ze doorvoer kunnen niet naar andere on-premises netwerken of virtuele netwerken via dezelfde Azure VPN-gateway**.</span><span class="sxs-lookup"><span data-stu-id="456ea-136">The on-premises networks connecting through policy-based VPN devices with this mechanism can only connect to the Azure virtual network; **they cannot transit to other on-premises networks or virtual networks via the same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="456ea-137">De configuratieoptie maakt deel uit van het aangepaste beleid voor IPsec/IKE-verbinding.</span><span class="sxs-lookup"><span data-stu-id="456ea-137">The configuration option is part of the custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="456ea-138">Als u het verkeer op basis van beleid selector-optie inschakelt, moet u het volledige beleid (IPsec/IKE-algoritmen voor versleuteling en integriteit, kracht en SA-levensduur).</span><span class="sxs-lookup"><span data-stu-id="456ea-138">If you enable the policy-based traffic selector option, you must specify the complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="456ea-139">Het volgende diagram laat zien waarom transitroutering via Azure VPN-gateway niet met de optie op basis van beleid werkt:</span><span class="sxs-lookup"><span data-stu-id="456ea-139">The following diagram shows why transit routing via Azure VPN gateway doesn't work with the policy-based option:</span></span>

![doorvoer op basis van beleid](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="456ea-141">Zoals u in het diagram, is de Azure VPN-gateway selectoren verkeer van het virtuele netwerk aan elk van de voorvoegsels van het lokale netwerk, maar niet de voorvoegsels voor cross-verbinding.</span><span class="sxs-lookup"><span data-stu-id="456ea-141">As shown in the diagram, the Azure VPN gateway has traffic selectors from the virtual network to each of the on-premises network prefixes, but not the cross-connection prefixes.</span></span> <span data-ttu-id="456ea-142">Bijvoorbeeld: lokale site 2, 3, en site 4 kan elk communiceren met VNet1 respectievelijk, maar kan geen verbinding maken via de Azure VPN-gateway met elkaar.</span><span class="sxs-lookup"><span data-stu-id="456ea-142">For example, on-premises site 2, site 3, and site 4 can each communicate to VNet1 respectively, but cannot connect via the Azure VPN gateway to each other.</span></span> <span data-ttu-id="456ea-143">Het diagram toont de cross-connect verkeer selectoren die niet beschikbaar in de Azure VPN-gateway in deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="456ea-143">The diagram shows the cross-connect traffic selectors that are not available in the Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="456ea-144">Op beleid gebaseerde verkeer selectoren configureren op een verbinding</span><span class="sxs-lookup"><span data-stu-id="456ea-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="456ea-145">De instructies in dit artikel Volg het hetzelfde voorbeeld zoals beschreven in [configureren IPsec/IKE-beleid voor S2S of VNet-naar-VNet-verbindingen](vpn-gateway-ipsecikepolicy-rm-powershell.md) een S2S VPN-verbinding tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="456ea-145">The instructions in this article follow the same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) to establish a S2S VPN connection.</span></span> <span data-ttu-id="456ea-146">Dit wordt weergegeven in het volgende diagram:</span><span class="sxs-lookup"><span data-stu-id="456ea-146">This is shown in the following diagram:</span></span>

![s2s-beleid](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="456ea-148">De werkstroom voor deze verbindingen:</span><span class="sxs-lookup"><span data-stu-id="456ea-148">The workflow to enable this connectivity:</span></span>
1. <span data-ttu-id="456ea-149">Het virtuele netwerk, de VPN-gateway en de lokale netwerkgateway voor uw cross-premises-verbinding maken</span><span class="sxs-lookup"><span data-stu-id="456ea-149">Create the virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="456ea-150">Een IPsec/IKE-beleid maken</span><span class="sxs-lookup"><span data-stu-id="456ea-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="456ea-151">Het beleid van toepassing wanneer u een S2S of VNet-naar-VNet-verbinding maken en **inschakelen van het verkeer op basis van beleid selectoren** op de verbinding</span><span class="sxs-lookup"><span data-stu-id="456ea-151">Apply the policy when you create a S2S or VNet-to-VNet connection, and **enable the policy-based traffic selectors** on the connection</span></span>
4. <span data-ttu-id="456ea-152">Als de verbinding al gemaakt is, kunt u deze toepassing of het beleid bijwerken naar een bestaande verbinding</span><span class="sxs-lookup"><span data-stu-id="456ea-152">If the connection is already created, you can apply or update the policy to an existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="456ea-153">Op beleid gebaseerde verkeer selectoren op een verbinding inschakelen</span><span class="sxs-lookup"><span data-stu-id="456ea-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="456ea-154">Zorg ervoor dat u hebt voltooid [deel 3 van het beleid configureren IPsec/IKE artikel](vpn-gateway-ipsecikepolicy-rm-powershell.md) voor deze sectie.</span><span class="sxs-lookup"><span data-stu-id="456ea-154">Make sure you have completed [Part 3 of the Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="456ea-155">Het volgende voorbeeld wordt de parameters en de stappen uit:</span><span class="sxs-lookup"><span data-stu-id="456ea-155">The following example uses the same parameters and steps:</span></span>

### <a name="step-1---create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="456ea-156">Stap 1: het virtuele netwerk, de VPN-gateway en de lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="456ea-156">Step 1 - Create the virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-to-your-subscription"></a><span data-ttu-id="456ea-157">1. De variabelen declareren & verbinding maken met uw abonnement</span><span class="sxs-lookup"><span data-stu-id="456ea-157">1. Declare your variables & connect to your subscription</span></span>
<span data-ttu-id="456ea-158">Voor deze oefening eerst we onze variabelen declareren.</span><span class="sxs-lookup"><span data-stu-id="456ea-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="456ea-159">Zorg dat u de waarden door uw eigen waarden vervangt wanneer u configureert voor productie.</span><span class="sxs-lookup"><span data-stu-id="456ea-159">Be sure to replace the values with your own when configuring for production.</span></span>

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
<span data-ttu-id="456ea-160">Zorg ervoor dat u overschakelt naar de PowerShell-modus voor het gebruik van de Resource Manager-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="456ea-160">To use the Resource Manager cmdlets, make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="456ea-161">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="456ea-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="456ea-162">Open de PowerShell-console en maak verbinding met uw account.</span><span class="sxs-lookup"><span data-stu-id="456ea-162">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="456ea-163">Gebruik het volgende voorbeeld als hulp bij het maken van de verbinding:</span><span class="sxs-lookup"><span data-stu-id="456ea-163">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="456ea-164">2. Het virtuele netwerk, de VPN-gateway en de lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="456ea-164">2. Create the virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="456ea-165">Het volgende voorbeeld wordt het virtuele netwerk TestVNet1 met drie subnetten en de VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="456ea-165">The following example creates the virtual network, TestVNet1 with three subnets, and the VPN gateway.</span></span> <span data-ttu-id="456ea-166">Bij het vervangen van waarden, is het belangrijk dat u altijd de naam het gatewaysubnet bijzonder GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="456ea-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="456ea-167">Als u een andere naam kiest, mislukt het maken van de gateway.</span><span class="sxs-lookup"><span data-stu-id="456ea-167">If you name it something else, your gateway creation fails.</span></span>

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="456ea-168">Stap 2: een S2S VPN-verbinding maken met een IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="456ea-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="456ea-169">1. Een IPsec/IKE-beleid maken</span><span class="sxs-lookup"><span data-stu-id="456ea-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="456ea-170">U moet een IPsec/IKE-beleid maken om in te schakelen, de optie 'UsePolicyBasedTrafficSelectors' op de verbinding.</span><span class="sxs-lookup"><span data-stu-id="456ea-170">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="456ea-171">Het volgende voorbeeld wordt een IPsec/IKE-beleid met deze algoritmen en parameters:</span><span class="sxs-lookup"><span data-stu-id="456ea-171">The following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="456ea-172">IKEv2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="456ea-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="456ea-173">IPsec: AES256, SHA256, PFS24, SA levensduur 3600 seconden & 2048KB</span><span class="sxs-lookup"><span data-stu-id="456ea-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-the-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="456ea-174">2. De S2S VPN-verbinding maken met op beleid gebaseerde verkeer selectoren en IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="456ea-174">2. Create the S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="456ea-175">Een S2S VPN-verbinding maken en toepassen van het IPsec/IKE-beleid in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="456ea-175">Create an S2S VPN connection and apply the IPsec/IKE policy created in the previous step.</span></span> <span data-ttu-id="456ea-176">Houd rekening met de extra parameter '-UsePolicyBasedTrafficSelectors $True ' waardoor selectoren verkeer op basis van beleid op de verbinding.</span><span class="sxs-lookup"><span data-stu-id="456ea-176">Be aware of the additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on the connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="456ea-177">Nadat de stappen is voltooid, wordt de S2S VPN-verbinding gebruik van de IPsec/IKE-beleid dat is gedefinieerd en schakel selectoren verkeer op basis van beleid op de verbinding.</span><span class="sxs-lookup"><span data-stu-id="456ea-177">After completing the steps, the S2S VPN connection will use the IPsec/IKE policy defined, and enable policy-based traffic selectors on the connection.</span></span> <span data-ttu-id="456ea-178">U kunt dezelfde stappen om meer verbindingen toevoegen aan extra on-premises op beleid gebaseerde VPN-apparaten van dezelfde Azure VPN-gateway herhalen.</span><span class="sxs-lookup"><span data-stu-id="456ea-178">You can repeat the same steps to add more connections to additional on-premises policy-based VPN devices from the same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="456ea-179">Selectoren verkeer op basis van beleid voor een verbinding bijwerken</span><span class="sxs-lookup"><span data-stu-id="456ea-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="456ea-180">De laatste sectie laat zien hoe het verkeer op basis van beleid Selector-optie voor een bestaande S2S VPN-verbinding bijwerken.</span><span class="sxs-lookup"><span data-stu-id="456ea-180">The last section shows you how to update the policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-the-connection"></a><span data-ttu-id="456ea-181">1. De verbinding ophalen</span><span class="sxs-lookup"><span data-stu-id="456ea-181">1. Get the connection</span></span>
<span data-ttu-id="456ea-182">De verbindingsbron ophalen.</span><span class="sxs-lookup"><span data-stu-id="456ea-182">Get the connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-the-policy-based-traffic-selectors-option"></a><span data-ttu-id="456ea-183">2. Controleer de Selector-optie van verkeer op basis van beleid</span><span class="sxs-lookup"><span data-stu-id="456ea-183">2. Check the policy-based traffic selectors option</span></span>
<span data-ttu-id="456ea-184">De volgende regel geeft aan of de selectoren verkeer op basis van beleid worden gebruikt voor de verbinding:</span><span class="sxs-lookup"><span data-stu-id="456ea-184">The following line shows whether the policy-based traffic selectors are used for the connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="456ea-185">Als de regel retourneert '**True**', vervolgens selectoren verkeer op basis van beleid zijn geconfigureerd op de verbinding; anders wordt '**False**. "</span><span class="sxs-lookup"><span data-stu-id="456ea-185">If the line returns "**True**", then policy-based traffic selectors are configured on the connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-the-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="456ea-186">3. Bijwerken van de selectoren verkeer op basis van beleid voor een verbinding</span><span class="sxs-lookup"><span data-stu-id="456ea-186">3. Update the policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="456ea-187">Zodra u de verbindingsbron hebt verkregen, kunt u in- of uitschakelen van de optie.</span><span class="sxs-lookup"><span data-stu-id="456ea-187">Once you obtain the connection resource, you can enable or disable the option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="456ea-188">UsePolicyBasedTrafficSelectors uitschakelen</span><span class="sxs-lookup"><span data-stu-id="456ea-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="456ea-189">Het volgende voorbeeld wordt de verkeer op basis van beleid Selector-optie uitgeschakeld, maar het beleid voor IPsec/IKE ongewijzigd blijft:</span><span class="sxs-lookup"><span data-stu-id="456ea-189">The following example disables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="456ea-190">UsePolicyBasedTrafficSelectors inschakelen</span><span class="sxs-lookup"><span data-stu-id="456ea-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="456ea-191">Het volgende voorbeeld wordt de verkeer op basis van beleid Selector-optie ingeschakeld, maar het beleid voor IPsec/IKE ongewijzigd blijft:</span><span class="sxs-lookup"><span data-stu-id="456ea-191">The following example enables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="456ea-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="456ea-192">Next steps</span></span>
<span data-ttu-id="456ea-193">Wanneer de verbinding is voltooid, kunt u virtuele machines aan uw virtuele netwerken toevoegen.</span><span class="sxs-lookup"><span data-stu-id="456ea-193">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="456ea-194">Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.</span><span class="sxs-lookup"><span data-stu-id="456ea-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="456ea-195">Bekijk ook [configureren IPsec/IKE-beleid voor S2S-VPN- of VNet-naar-VNet-verbindingen](vpn-gateway-ipsecikepolicy-rm-powershell.md) voor meer informatie over aangepaste IPsec/IKE-beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="456ea-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
