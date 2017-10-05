---
title: 'Configureren van BGP op Azure VPN-Gateways: Resource Manager: PowerShell | Microsoft Docs'
description: In dit artikel begeleidt u bij het configureren van BGP met Azure VPN-Gateways met Azure Resource Manager en PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: b00a3fe7ba4b12c2e9c486188c292cd6fafb60a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="f052a-103">Het configureren van BGP op Azure VPN-Gateways met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="f052a-103">How to configure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="f052a-104">Dit artikel begeleidt u bij de stappen voor het inschakelen van BGP op een cross-premises Site-naar-Site (S2S) VPN-verbinding en een VNet-naar-VNet-verbinding met het Resource Manager-implementatiemodel en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f052a-104">This article walks you through the steps to enable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="f052a-105">Over BGP</span><span class="sxs-lookup"><span data-stu-id="f052a-105">About BGP</span></span>
<span data-ttu-id="f052a-106">BGP is het standaardprotocol voor routering dat doorgaans op internet wordt gebruikt voor het uitwisselen van routerings- en bereikbaarheidsgegevens tussen twee of meer netwerken.</span><span class="sxs-lookup"><span data-stu-id="f052a-106">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="f052a-107">BGP kunt u de Azure VPN-Gateways en uw on-premises VPN-apparaten, aangeroepen BGP-peers of neighbors, 'routes' exchange die wordt beide gateways over de beschikbaarheid en bereikbaarheid voor deze voorvoegsels informeren zodat ze via de gateways of routers die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="f052a-107">BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span></span> <span data-ttu-id="f052a-108">Met BGP kan ook transitroutering tussen meerdere netwerken worden ingeschakeld door routes die een BGP-gateway leert van één BGP te propageren naar alle andere BGP-peers.</span><span class="sxs-lookup"><span data-stu-id="f052a-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span></span>

<span data-ttu-id="f052a-109">Zie [overzicht van BGP met Azure VPN-Gateways](vpn-gateway-bgp-overview.md) meer discussie over de voordelen van BGP en inzicht in de technische vereisten en overwegingen van het gebruik van BGP.</span><span class="sxs-lookup"><span data-stu-id="f052a-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and to understand the technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="f052a-110">Aan de slag met BGP op Azure VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="f052a-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="f052a-111">Dit artikel begeleidt u bij de stappen voor de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f052a-111">This article walks you through the steps to do the following tasks:</span></span>

* [<span data-ttu-id="f052a-112">Deel 1 - Enable BGP op uw Azure VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="f052a-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="f052a-113">Deel 2: een cross-premises verbinding maken met BGP</span><span class="sxs-lookup"><span data-stu-id="f052a-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="f052a-114">Deel 3 – een VNet-naar-VNet verbinding maken met BGP</span><span class="sxs-lookup"><span data-stu-id="f052a-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="f052a-115">Elk deel van de instructies vormt een basisbouwsteen voor het inschakelen van BGP in uw netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="f052a-115">Each part of the instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="f052a-116">Als u alle drie delen hebt voltooid, wordt de topologie build zoals weergegeven in het volgende diagram:</span><span class="sxs-lookup"><span data-stu-id="f052a-116">If you complete all three parts, you build the topology as shown in the following diagram:</span></span>

![BGP-topologieën](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="f052a-118">U kunt onderdelen samen om samen te stellen een meer complexe, Multihop, doorvoer-netwerk dat voldoet aan uw behoeften kunt combineren.</span><span class="sxs-lookup"><span data-stu-id="f052a-118">You can combine parts together to build a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="f052a-119"><a name ="enablebgp"></a>Deel 1: BGP configureren op de Azure VPN-Gateway</span><span class="sxs-lookup"><span data-stu-id="f052a-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on the Azure VPN Gateway</span></span>
<span data-ttu-id="f052a-120">De configuratiestappen stelt u de BGP-parameters van de Azure VPN-gateway, zoals wordt weergegeven in het volgende diagram:</span><span class="sxs-lookup"><span data-stu-id="f052a-120">The configuration steps set up the BGP parameters of the Azure VPN gateway as shown in the following diagram:</span></span>

![BGP-Gateway](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="f052a-122">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f052a-122">Before you begin</span></span>
* <span data-ttu-id="f052a-123">Controleer of u een Azure-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="f052a-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="f052a-124">Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f052a-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f052a-125">Installeer de Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f052a-125">Install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="f052a-126">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor meer informatie over het installeren van de PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f052a-126">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="f052a-127">Stap 1: Maak en configureer VNet1</span><span class="sxs-lookup"><span data-stu-id="f052a-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="f052a-128">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="f052a-128">1. Declare your variables</span></span>
<span data-ttu-id="f052a-129">Voor deze oefening eerst we onze variabelen declareren.</span><span class="sxs-lookup"><span data-stu-id="f052a-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="f052a-130">Het volgende voorbeeld declareert de variabelen met de waarden voor deze oefening.</span><span class="sxs-lookup"><span data-stu-id="f052a-130">The following example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="f052a-131">Zorg dat u de waarden door uw eigen waarden vervangt wanneer u configureert voor productie.</span><span class="sxs-lookup"><span data-stu-id="f052a-131">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="f052a-132">U kunt deze variabelen gebruiken als u de stappen wilt doorlopen om vertrouwd te raken met dit type configuratie.</span><span class="sxs-lookup"><span data-stu-id="f052a-132">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="f052a-133">Wijzig de variabelen en kopieer en plak ze in uw PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="f052a-133">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="f052a-134">2. Verbinding maken met uw abonnement en een nieuwe resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="f052a-134">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="f052a-135">Zorg ervoor dat u overschakelt naar de PowerShell-modus voor het gebruik van de Resource Manager-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f052a-135">To use the Resource Manager cmdlets, Make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="f052a-136">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f052a-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="f052a-137">Open de PowerShell-console en maak verbinding met uw account.</span><span class="sxs-lookup"><span data-stu-id="f052a-137">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="f052a-138">Gebruik het volgende voorbeeld als hulp bij het maken van de verbinding:</span><span class="sxs-lookup"><span data-stu-id="f052a-138">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="f052a-139">3. TestVNet1 maken</span><span class="sxs-lookup"><span data-stu-id="f052a-139">3. Create TestVNet1</span></span>
<span data-ttu-id="f052a-140">Het volgende voorbeeld maakt een virtueel netwerk met de naam TestVNet1 en drie subnetten, één naam GatewaySubnet, een opgeroepen FrontEnd en één opgeroepen back-end.</span><span class="sxs-lookup"><span data-stu-id="f052a-140">The following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="f052a-141">Wanneer u de waarden vervangt, is het belangrijk dat u de juiste namen voor de gatewaysubnets gebruikt, in het bijzonder GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="f052a-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="f052a-142">Als u een andere naam kiest, mislukt het maken van de gateway.</span><span class="sxs-lookup"><span data-stu-id="f052a-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="f052a-143">Stap 2: de VPN-Gateway voor TestVNet1 maken met de BGP-parameters</span><span class="sxs-lookup"><span data-stu-id="f052a-143">Step 2 - Create the VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-the-ip-and-subnet-configurations"></a><span data-ttu-id="f052a-144">1. De configuraties van IP-adres en subnet maken</span><span class="sxs-lookup"><span data-stu-id="f052a-144">1. Create the IP and subnet configurations</span></span>
<span data-ttu-id="f052a-145">Vraag om een openbaar IP-adres toe te wijzen aan de gateway die u voor uw VNet gaat maken.</span><span class="sxs-lookup"><span data-stu-id="f052a-145">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="f052a-146">Ook definieert u de vereiste subnet en IP-configuraties.</span><span class="sxs-lookup"><span data-stu-id="f052a-146">You'll also define the required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-the-vpn-gateway-with-the-as-number"></a><span data-ttu-id="f052a-147">2. De VPN-gateway maken met het AS-nummer</span><span class="sxs-lookup"><span data-stu-id="f052a-147">2. Create the VPN gateway with the AS number</span></span>
<span data-ttu-id="f052a-148">Maak de gateway van het virtuele netwerk voor TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="f052a-148">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="f052a-149">BGP is vereist voor een op Route gebaseerde VPN-gateway en de toevoeging parameter, - Asn het ASN (AS-nummer) instellen voor TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="f052a-149">BGP requires a Route-Based VPN gateway, and also the addition parameter, -Asn, to set the ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="f052a-150">Als de ASN-parameter niet is ingesteld, wordt de ASN van 65515 toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f052a-150">If you do not set the ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="f052a-151">Het maken van een gateway kan even duren (30 minuten of langer).</span><span class="sxs-lookup"><span data-stu-id="f052a-151">Creating a gateway can take a while (30 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-the-azure-bgp-peer-ip-address"></a><span data-ttu-id="f052a-152">3. Het Azure BGP-Peer-IP-adres verkrijgen</span><span class="sxs-lookup"><span data-stu-id="f052a-152">3. Obtain the Azure BGP Peer IP address</span></span>
<span data-ttu-id="f052a-153">Zodra de gateway is gemaakt, moet u het BGP-Peer-IP-adres op de Azure VPN-Gateway.</span><span class="sxs-lookup"><span data-stu-id="f052a-153">Once the gateway is created, you need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="f052a-154">Dit adres wordt gebruikt voor de Azure VPN-Gateway configureren als een BGP-Peer voor uw on-premises VPN-apparaten.</span><span class="sxs-lookup"><span data-stu-id="f052a-154">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="f052a-155">De laatste opdracht toont de bijbehorende BGP-configuraties op de Azure VPN-Gateway; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f052a-155">The last command shows the corresponding BGP configurations on the Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="f052a-156">Zodra de gateway is gemaakt, kunt u deze gateway om cross-premises-verbinding of een VNet-naar-VNet-verbinding waarvoor BGP.</span><span class="sxs-lookup"><span data-stu-id="f052a-156">Once the gateway is created, you can use this gateway to establish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="f052a-157">De volgende secties helpt bij de stappen voor het voltooien van de oefening.</span><span class="sxs-lookup"><span data-stu-id="f052a-157">The following sections walk through the steps to complete the exercise.</span></span>

## <span data-ttu-id="f052a-158"><a name ="crossprembbgp"></a>Deel 2: een cross-premises verbinding maken met BGP</span><span class="sxs-lookup"><span data-stu-id="f052a-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="f052a-159">Als u wilt een cross-premises-verbinding tot stand brengen, moet u een lokale netwerkgateway om weer te geven van uw on-premises VPN-apparaat en een verbinding met de VPN-gateway verbinding met de lokale netwerkgateway maken.</span><span class="sxs-lookup"><span data-stu-id="f052a-159">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the VPN gateway with the local network gateway.</span></span> <span data-ttu-id="f052a-160">Hoewel er artikelen die u bij deze stappen helpt, wordt in dit artikel om op te geven van de BGP-configuratieparameters vereiste aanvullende eigenschappen bevat.</span><span class="sxs-lookup"><span data-stu-id="f052a-160">While there are articles that walk you through these steps, this article contains the additional properties required to specify the BGP configuration parameters.</span></span>

![BGP voor Cross-Premises](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="f052a-162">Controleer of u hebt uitgevoerd voordat u doorgaat, [Part 1](#enablebgp) van deze oefening.</span><span class="sxs-lookup"><span data-stu-id="f052a-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="f052a-163">Stap 1 - maken en configureren van de lokale netwerkgateway</span><span class="sxs-lookup"><span data-stu-id="f052a-163">Step 1 - Create and configure the local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="f052a-164">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="f052a-164">1. Declare your variables</span></span>

<span data-ttu-id="f052a-165">In deze oefening blijft het bouwen van de configuratie in het diagram worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f052a-165">This exercise continues to build the configuration shown in the diagram.</span></span> <span data-ttu-id="f052a-166">Zorg ervoor dat u de waarden vervangt door de waarden die u voor uw configuratie wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f052a-166">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="f052a-167">Een aantal dingen om aan te geven met betrekking tot het lokale netwerk gateway-parameters:</span><span class="sxs-lookup"><span data-stu-id="f052a-167">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="f052a-168">De lokale netwerkgateway kan zich in dezelfde of een andere locatie en resourcegroep als de VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="f052a-168">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="f052a-169">Dit voorbeeld ziet u ze in verschillende resourcegroepen op verschillende locaties.</span><span class="sxs-lookup"><span data-stu-id="f052a-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="f052a-170">Het minimum-voorvoegsel moet u opgeven voor de lokale netwerkgateway is het adres van de host van de BGP-Peer-IP-adres op uw VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="f052a-170">The minimum prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="f052a-171">In dit geval is een /32 voorvoegsel "10.52.255.254/32".</span><span class="sxs-lookup"><span data-stu-id="f052a-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="f052a-172">U moet verschillende ASN van BGP tussen uw on-premises netwerken en Azure VNet gebruiken als een herinnering.</span><span class="sxs-lookup"><span data-stu-id="f052a-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="f052a-173">Als ze hetzelfde zijn, moet u uw VNet ASN wijzigen als de ASN in uw on-premises VPN-apparaat al worden gebruikt als peer met andere BGP-neighbors.</span><span class="sxs-lookup"><span data-stu-id="f052a-173">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

<span data-ttu-id="f052a-174">Controleer voordat u verdergaat of u nog bent verbonden met Abonnement 1.</span><span class="sxs-lookup"><span data-stu-id="f052a-174">Before you continue, make sure you are still connected to Subscription 1.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="f052a-175">2. De lokale netwerkgateway voor Site5 maken</span><span class="sxs-lookup"><span data-stu-id="f052a-175">2. Create the local network gateway for Site5</span></span>

<span data-ttu-id="f052a-176">Zorg ervoor dat de resourcegroep maken als deze niet gemaakt is, voordat u de lokale netwerkgateway maakt.</span><span class="sxs-lookup"><span data-stu-id="f052a-176">Be sure to create the resource group if it is not created, before you create the local network gateway.</span></span> <span data-ttu-id="f052a-177">U ziet de twee extra parameters voor de lokale netwerkgateway: Asn en BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="f052a-177">Notice the two additional parameters for the local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="f052a-178">Stap 2: verbinding maken met de VNet-gateway en de lokale netwerkgateway</span><span class="sxs-lookup"><span data-stu-id="f052a-178">Step 2 - Connect the VNet gateway and local network gateway</span></span>

#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="f052a-179">1. Ophalen van de twee gateways</span><span class="sxs-lookup"><span data-stu-id="f052a-179">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="f052a-180">2. De verbinding tussen TestVNet1 en Site5 maken</span><span class="sxs-lookup"><span data-stu-id="f052a-180">2. Create the TestVNet1 to Site5 connection</span></span>

<span data-ttu-id="f052a-181">In deze stap maakt u de verbinding van TestVNet1 naar Site5.</span><span class="sxs-lookup"><span data-stu-id="f052a-181">In this step, you create the connection from TestVNet1 to Site5.</span></span> <span data-ttu-id="f052a-182">U moet opgeven '-EnableBGP $True ' BGP inschakelen voor deze verbinding.</span><span class="sxs-lookup"><span data-stu-id="f052a-182">You must specify "-EnableBGP $True" to enable BGP for this connection.</span></span> <span data-ttu-id="f052a-183">Zoals eerder besproken, is het mogelijk om BGP- en niet-BGP-verbindingen voor dezelfde Azure VPN-Gateway.</span><span class="sxs-lookup"><span data-stu-id="f052a-183">As discussed earlier, it is possible to have both BGP and non-BGP connections for the same Azure VPN Gateway.</span></span> <span data-ttu-id="f052a-184">Tenzij BGP in de eigenschap connection is ingeschakeld, wordt Azure niet BGP inschakelen voor deze verbinding Hoewel BGP-parameters zijn al geconfigureerd op beide gateways.</span><span class="sxs-lookup"><span data-stu-id="f052a-184">Unless BGP is enabled in the connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="f052a-185">Het volgende voorbeeld bevat de parameters die u in de configuratiesectie BGP op uw on-premises VPN-apparaat voor deze oefening:</span><span class="sxs-lookup"><span data-stu-id="f052a-185">The following example lists the parameters you enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being the VPN tunnel interface on your device
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="f052a-186">De verbinding is hersteld na een paar minuten en de BGP-peeringsessie begint eenmaal IPsec-verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="f052a-186">The connection is established after a few minutes, and the BGP peering session starts once the IPsec connection is established.</span></span>

## <span data-ttu-id="f052a-187"><a name ="v2vbgp"></a>Deel 3 – een VNet-naar-VNet verbinding maken met BGP</span><span class="sxs-lookup"><span data-stu-id="f052a-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="f052a-188">In deze sectie voegt een VNet-naar-VNet-verbinding met BGP, zoals wordt weergegeven in het volgende diagram:</span><span class="sxs-lookup"><span data-stu-id="f052a-188">This section adds a VNet-to-VNet connection with BGP, as shown in the following diagram:</span></span>

![BGP voor VNet-naar-VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="f052a-190">De volgende instructies blijven uit de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="f052a-190">The following instructions continue from the previous steps.</span></span> <span data-ttu-id="f052a-191">U moet voltooien [deel I](#enablebgp) maken en configureren van TestVNet1 en de VPN-Gateway met BGP.</span><span class="sxs-lookup"><span data-stu-id="f052a-191">You must complete [Part I](#enablebgp) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="f052a-192">Stap 1: TestVNet2 en de VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="f052a-192">Step 1 - Create TestVNet2 and the VPN gateway</span></span>

<span data-ttu-id="f052a-193">Het is belangrijk om ervoor te zorgen dat de IP-adresruimte van het nieuwe virtuele netwerk TestVNet2, niet met een van uw VNet-bereiken overlapt.</span><span class="sxs-lookup"><span data-stu-id="f052a-193">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="f052a-194">In dit voorbeeld wordt de virtuele netwerken tot hetzelfde abonnement behoren.</span><span class="sxs-lookup"><span data-stu-id="f052a-194">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="f052a-195">U kunt de VNet-naar-VNet-verbindingen tussen de verschillende abonnementen instellen.</span><span class="sxs-lookup"><span data-stu-id="f052a-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="f052a-196">Zie voor meer informatie [een VNet-naar-VNet-verbinding configureren](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f052a-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="f052a-197">Zorg ervoor dat u toevoegt het '-EnableBgp $True "bij het maken van de verbindingen om in te schakelen van BGP.</span><span class="sxs-lookup"><span data-stu-id="f052a-197">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="f052a-198">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="f052a-198">1. Declare your variables</span></span>

<span data-ttu-id="f052a-199">Zorg ervoor dat u de waarden vervangt door de waarden die u voor uw configuratie wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f052a-199">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="f052a-200">2. TestVNet2 in de nieuwe resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="f052a-200">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="f052a-201">3. De VPN-gateway maken voor TestVNet2 met BGP-parameters</span><span class="sxs-lookup"><span data-stu-id="f052a-201">3. Create the VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="f052a-202">Aanvragen van een openbare IP-adres worden toegewezen aan de gateway maakt voor uw VNet en definieer het vereiste subnet en IP-configuraties.</span><span class="sxs-lookup"><span data-stu-id="f052a-202">Request a public IP address to be allocated to the gateway you will create for your VNet and define the required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="f052a-203">Maak de VPN-gateway met het AS-nummer.</span><span class="sxs-lookup"><span data-stu-id="f052a-203">Create the VPN gateway with the AS number.</span></span> <span data-ttu-id="f052a-204">U moet de standaard een ASN overschrijven op uw Azure VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="f052a-204">You must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="f052a-205">De ASN's voor de verbonden VNets moet verschillen van BGP en transitroutering inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f052a-205">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="f052a-206">Stap 2: verbinding maken met de TestVNet1 en TestVNet2 gateways</span><span class="sxs-lookup"><span data-stu-id="f052a-206">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="f052a-207">In dit voorbeeld zijn beide gateways in hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="f052a-207">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="f052a-208">U kunt deze stap voltooien in dezelfde PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="f052a-208">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="f052a-209">1. Beide gateways ophalen</span><span class="sxs-lookup"><span data-stu-id="f052a-209">1. Get both gateways</span></span>

<span data-ttu-id="f052a-210">Zorg dat u zich aanmeldt bij en verbinding maakt met Abonnement 1.</span><span class="sxs-lookup"><span data-stu-id="f052a-210">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="f052a-211">2. Beide verbindingen maken</span><span class="sxs-lookup"><span data-stu-id="f052a-211">2. Create both connections</span></span>

<span data-ttu-id="f052a-212">In deze stap maakt u de verbinding van TestVNet1 naar TestVNet2 en de verbinding van TestVNet2 naar TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="f052a-212">In this step, you create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="f052a-213">Zorg ervoor dat het inschakelen van BGP voor beide verbindingen.</span><span class="sxs-lookup"><span data-stu-id="f052a-213">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="f052a-214">Nadat u deze stappen uitvoert, wordt de verbinding na een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="f052a-214">After completing these steps, the connection is established after a few minutes.</span></span> <span data-ttu-id="f052a-215">De BGP-peeringsessie is nadat de VNet-naar-VNet-verbinding is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f052a-215">The BGP peering session is up once the VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="f052a-216">Als u alle drie de gedeelten van deze oefening hebt voltooid, kunt u de volgende netwerktopologie hebt ingesteld:</span><span class="sxs-lookup"><span data-stu-id="f052a-216">If you completed all three parts of this exercise, you have established the following network topology:</span></span>

![BGP voor VNet-naar-VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="f052a-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f052a-218">Next steps</span></span>

<span data-ttu-id="f052a-219">Wanneer de verbinding is voltooid, kunt u virtuele machines aan uw virtuele netwerken toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f052a-219">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="f052a-220">Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.</span><span class="sxs-lookup"><span data-stu-id="f052a-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>