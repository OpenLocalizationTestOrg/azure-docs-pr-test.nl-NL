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
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="76f20-103">Hoe tooconfigure BGP op Azure VPN-Gateways met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="76f20-103">How tooconfigure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="76f20-104">Dit artikel begeleidt u bij Hallo stappen tooenable BGP op een cross-premises Site-naar-Site (S2S) VPN-verbinding en een VNet-naar-VNet-verbinding met Hallo Resource Manager-implementatiemodel en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76f20-104">This article walks you through hello steps tooenable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="76f20-105">Over BGP</span><span class="sxs-lookup"><span data-stu-id="76f20-105">About BGP</span></span>
<span data-ttu-id="76f20-106">BGP is Hallo standaardprotocol voor routering gebruikte in Hallo Internet tooexchange Routering en bereikbaarheid tussen twee of meer netwerken.</span><span class="sxs-lookup"><span data-stu-id="76f20-106">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="76f20-107">BGP maakt hello Azure VPN-Gateways en uw on-premises VPN-apparaten, BGP-peers of neighbors genoemd, tooexchange 'routes' die wordt beide gateways informeren over Hallo beschikbaarheid en bereikbaarheid voor degenen prefixes toogo via Hallo gateways of routers die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="76f20-107">BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="76f20-108">BGP ook transitroutering tussen meerdere netwerken door routes die een BGP-gateway van één BGP-peer-tooall leert andere BGP-peers.</span><span class="sxs-lookup"><span data-stu-id="76f20-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span>

<span data-ttu-id="76f20-109">Zie [overzicht van BGP met Azure VPN-Gateways](vpn-gateway-bgp-overview.md) meer discussie over de voordelen van BGP- en toounderstand Hallo technische vereisten en overwegingen van het gebruik van BGP.</span><span class="sxs-lookup"><span data-stu-id="76f20-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and toounderstand hello technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="76f20-110">Aan de slag met BGP op Azure VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="76f20-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="76f20-111">Dit artikel begeleidt u bij Hallo stappen toodo Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="76f20-111">This article walks you through hello steps toodo hello following tasks:</span></span>

* [<span data-ttu-id="76f20-112">Deel 1 - Enable BGP op uw Azure VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="76f20-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="76f20-113">Deel 2: een cross-premises verbinding maken met BGP</span><span class="sxs-lookup"><span data-stu-id="76f20-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="76f20-114">Deel 3 – een VNet-naar-VNet verbinding maken met BGP</span><span class="sxs-lookup"><span data-stu-id="76f20-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="76f20-115">Elk deel van de instructies Hallo vormt een basisbouwsteen voor het inschakelen van BGP in uw netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="76f20-115">Each part of hello instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="76f20-116">Als u alle drie delen hebt voltooid, build Hallo topologie zoals weergegeven in het volgende diagram Hallo:</span><span class="sxs-lookup"><span data-stu-id="76f20-116">If you complete all three parts, you build hello topology as shown in hello following diagram:</span></span>

![BGP-topologieën](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="76f20-118">U kunt onderdelen samen toobuild een meer complexe, Multihop, doorvoer-netwerk dat voldoet aan uw behoeften kunt combineren.</span><span class="sxs-lookup"><span data-stu-id="76f20-118">You can combine parts together toobuild a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="76f20-119"><a name ="enablebgp"></a>Deel 1: BGP configureren op Hallo Azure VPN-Gateway</span><span class="sxs-lookup"><span data-stu-id="76f20-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on hello Azure VPN Gateway</span></span>
<span data-ttu-id="76f20-120">Hallo configuratiestappen instellen Hallo BGP-parameters van hello Azure VPN-gateway zoals weergegeven in het volgende diagram Hallo:</span><span class="sxs-lookup"><span data-stu-id="76f20-120">hello configuration steps set up hello BGP parameters of hello Azure VPN gateway as shown in hello following diagram:</span></span>

![BGP-Gateway](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="76f20-122">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="76f20-122">Before you begin</span></span>
* <span data-ttu-id="76f20-123">Controleer of u een Azure-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="76f20-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="76f20-124">Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76f20-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="76f20-125">Hello Azure Resource Manager PowerShell-cmdlets installeren.</span><span class="sxs-lookup"><span data-stu-id="76f20-125">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="76f20-126">Zie voor meer informatie over het installeren van de PowerShell-cmdlets Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="76f20-126">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="76f20-127">Stap 1: Maak en configureer VNet1</span><span class="sxs-lookup"><span data-stu-id="76f20-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="76f20-128">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="76f20-128">1. Declare your variables</span></span>
<span data-ttu-id="76f20-129">Voor deze oefening eerst we onze variabelen declareren.</span><span class="sxs-lookup"><span data-stu-id="76f20-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="76f20-130">Hallo volgende voorbeeld Hallo variabelen gedeclareerd met Hallo waarden voor deze oefening.</span><span class="sxs-lookup"><span data-stu-id="76f20-130">hello following example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="76f20-131">Ervoor tooreplace Hallo waarden door uw eigen worden wanneer u configureert voor productie.</span><span class="sxs-lookup"><span data-stu-id="76f20-131">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="76f20-132">U kunt deze variabelen gebruiken als u via Hallo stappen toobecome bekend zijn met dit type configuratie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="76f20-132">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="76f20-133">Wijzig variabelen hello, en kopieert en plakt u in de PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="76f20-133">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="76f20-134">2. Verbinding maken met tooyour abonnement en een nieuwe resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="76f20-134">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="76f20-135">toouse hello Resource Manager-cmdlets, zorg ervoor dat u overschakelt naar tooPowerShell modus.</span><span class="sxs-lookup"><span data-stu-id="76f20-135">toouse hello Resource Manager cmdlets, Make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="76f20-136">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="76f20-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="76f20-137">Open de PowerShell-console en tooyour-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="76f20-137">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="76f20-138">Gebruik Hallo volgende steekproef toohelp die u verbinding kunt maken:</span><span class="sxs-lookup"><span data-stu-id="76f20-138">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="76f20-139">3. TestVNet1 maken</span><span class="sxs-lookup"><span data-stu-id="76f20-139">3. Create TestVNet1</span></span>
<span data-ttu-id="76f20-140">Hallo maakt volgende voorbeeld een virtueel netwerk met de naam TestVNet1 en drie subnetten, één naam GatewaySubnet, een opgeroepen FrontEnd en één opgeroepen back-end.</span><span class="sxs-lookup"><span data-stu-id="76f20-140">hello following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="76f20-141">Wanneer u de waarden vervangt, is het belangrijk dat u de juiste namen voor de gatewaysubnets gebruikt, in het bijzonder GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="76f20-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="76f20-142">Als u een andere naam kiest, mislukt het maken van de gateway.</span><span class="sxs-lookup"><span data-stu-id="76f20-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="76f20-143">Stap 2: Hallo VPN-Gateway voor TestVNet1 maken met de BGP-parameters</span><span class="sxs-lookup"><span data-stu-id="76f20-143">Step 2 - Create hello VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-hello-ip-and-subnet-configurations"></a><span data-ttu-id="76f20-144">1. Hallo IP-adres en subnet configuraties maken</span><span class="sxs-lookup"><span data-stu-id="76f20-144">1. Create hello IP and subnet configurations</span></span>
<span data-ttu-id="76f20-145">Aanvragen van een openbare IP-adres toobe toegewezen toohello gateway u voor uw VNet maakt.</span><span class="sxs-lookup"><span data-stu-id="76f20-145">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="76f20-146">U zult ook Hallo vereist subnet en IP-configuraties definiëren.</span><span class="sxs-lookup"><span data-stu-id="76f20-146">You'll also define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a><span data-ttu-id="76f20-147">2. Hallo VPN-gateway maken met Hallo als getal</span><span class="sxs-lookup"><span data-stu-id="76f20-147">2. Create hello VPN gateway with hello AS number</span></span>
<span data-ttu-id="76f20-148">De virtuele netwerkgateway Hallo voor TestVNet1 maken.</span><span class="sxs-lookup"><span data-stu-id="76f20-148">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="76f20-149">BGP is een op Route gebaseerde VPN-gateway en Hallo toevoeging parameter, - Asn tooset Hallo ASN (AS-nummer) vereist voor TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="76f20-149">BGP requires a Route-Based VPN gateway, and also hello addition parameter, -Asn, tooset hello ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="76f20-150">Als Hallo ASN-parameter niet is ingesteld, wordt de ASN van 65515 toegewezen.</span><span class="sxs-lookup"><span data-stu-id="76f20-150">If you do not set hello ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="76f20-151">Maken van een gateway kan even duren (30 minuten of meer toocomplete).</span><span class="sxs-lookup"><span data-stu-id="76f20-151">Creating a gateway can take a while (30 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a><span data-ttu-id="76f20-152">3. Hello Azure BGP-Peer-IP-adres ophalen</span><span class="sxs-lookup"><span data-stu-id="76f20-152">3. Obtain hello Azure BGP Peer IP address</span></span>
<span data-ttu-id="76f20-153">Nadat het Hallo-gateway is gemaakt, moet u tooobtain Hallo BGP-Peer-IP-adres op Hallo Azure VPN-Gateway.</span><span class="sxs-lookup"><span data-stu-id="76f20-153">Once hello gateway is created, you need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="76f20-154">Dit adres is de benodigde tooconfigure hello Azure VPN-Gateway als een BGP-Peer voor uw on-premises VPN-apparaten.</span><span class="sxs-lookup"><span data-stu-id="76f20-154">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="76f20-155">de laatste opdracht Hallo toont Hallo bijbehorende BGP configuraties op Hallo Azure VPN-Gateway; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="76f20-155">hello last command shows hello corresponding BGP configurations on hello Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="76f20-156">Zodra Hallo gateway is gemaakt, kunt u deze gateway tooestablish cross-premises-verbinding of een VNet-naar-VNet-verbinding met BGP.</span><span class="sxs-lookup"><span data-stu-id="76f20-156">Once hello gateway is created, you can use this gateway tooestablish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="76f20-157">Hallo doorlopen volgende secties Hallo stappen toocomplete Hallo oefening.</span><span class="sxs-lookup"><span data-stu-id="76f20-157">hello following sections walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="76f20-158"><a name ="crossprembbgp"></a>Deel 2: een cross-premises verbinding maken met BGP</span><span class="sxs-lookup"><span data-stu-id="76f20-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="76f20-159">tooestablish een cross-premises-verbinding, moet u een lokale netwerkgateway toorepresent toocreate uw on-premises VPN-apparaat en een verbinding tooconnect Hallo VPN-gateway met de lokale netwerkgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="76f20-159">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="76f20-160">Hoewel er artikelen die u bij deze stappen helpt, wordt in dit artikel Hallo extra eigenschappen vereist toospecify Hallo BGP-configuratieparameters bevat.</span><span class="sxs-lookup"><span data-stu-id="76f20-160">While there are articles that walk you through these steps, this article contains hello additional properties required toospecify hello BGP configuration parameters.</span></span>

![BGP voor Cross-Premises](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="76f20-162">Controleer of u hebt uitgevoerd voordat u doorgaat, [Part 1](#enablebgp) van deze oefening.</span><span class="sxs-lookup"><span data-stu-id="76f20-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="76f20-163">Stap 1 - maken en configureren van de lokale netwerkgateway Hallo</span><span class="sxs-lookup"><span data-stu-id="76f20-163">Step 1 - Create and configure hello local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="76f20-164">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="76f20-164">1. Declare your variables</span></span>

<span data-ttu-id="76f20-165">In deze oefening blijft toobuild Hallo configuratie wordt weergegeven in het Hallo-diagram.</span><span class="sxs-lookup"><span data-stu-id="76f20-165">This exercise continues toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="76f20-166">Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="76f20-166">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="76f20-167">Een aantal dingen toonote met betrekking tot Hallo lokale netwerk gateway parameters:</span><span class="sxs-lookup"><span data-stu-id="76f20-167">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="76f20-168">Hallo lokale netwerkgateway kan zich in dezelfde hello of een andere locatie en resource als Hallo VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="76f20-168">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="76f20-169">Dit voorbeeld ziet u ze in verschillende resourcegroepen op verschillende locaties.</span><span class="sxs-lookup"><span data-stu-id="76f20-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="76f20-170">Hallo minimaal voorvoegsel moet u toodeclare voor de lokale netwerkgateway Hallo is Hallo hostadres van uw BGP-Peer-IP-adres op uw VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="76f20-170">hello minimum prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="76f20-171">In dit geval is een /32 voorvoegsel "10.52.255.254/32".</span><span class="sxs-lookup"><span data-stu-id="76f20-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="76f20-172">U moet verschillende ASN van BGP tussen uw on-premises netwerken en Azure VNet gebruiken als een herinnering.</span><span class="sxs-lookup"><span data-stu-id="76f20-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="76f20-173">Als ze zijn dezelfde hello, moet u toochange uw VNet ASN als Hallo ASN toopeer in uw on-premises VPN-apparaat al worden gebruikt met andere BGP-neighbors.</span><span class="sxs-lookup"><span data-stu-id="76f20-173">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

<span data-ttu-id="76f20-174">Voordat u doorgaat, zorg er dan voor dat u nog steeds verbonden tooSubscription 1 zijn.</span><span class="sxs-lookup"><span data-stu-id="76f20-174">Before you continue, make sure you are still connected tooSubscription 1.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="76f20-175">2. De lokale netwerkgateway Hallo voor Site5 maken</span><span class="sxs-lookup"><span data-stu-id="76f20-175">2. Create hello local network gateway for Site5</span></span>

<span data-ttu-id="76f20-176">Ervoor toocreate Hallo-resourcegroep worden als deze niet gemaakt is, voordat u de lokale netwerkgateway Hallo maakt.</span><span class="sxs-lookup"><span data-stu-id="76f20-176">Be sure toocreate hello resource group if it is not created, before you create hello local network gateway.</span></span> <span data-ttu-id="76f20-177">Let op Hallo twee extra parameters voor de lokale netwerkgateway Hallo: Asn en BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="76f20-177">Notice hello two additional parameters for hello local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="76f20-178">Stap 2: verbinding maken met de Hallo VNet-gateway en de lokale netwerkgateway</span><span class="sxs-lookup"><span data-stu-id="76f20-178">Step 2 - Connect hello VNet gateway and local network gateway</span></span>

#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="76f20-179">1. Hallo twee gateways ophalen</span><span class="sxs-lookup"><span data-stu-id="76f20-179">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="76f20-180">2. Hallo TestVNet1 tooSite5 verbinding maken</span><span class="sxs-lookup"><span data-stu-id="76f20-180">2. Create hello TestVNet1 tooSite5 connection</span></span>

<span data-ttu-id="76f20-181">In deze stap maakt u Hallo verbinding van TestVNet1 tooSite5.</span><span class="sxs-lookup"><span data-stu-id="76f20-181">In this step, you create hello connection from TestVNet1 tooSite5.</span></span> <span data-ttu-id="76f20-182">U moet opgeven '-EnableBGP $True ' tooenable BGP voor deze verbinding.</span><span class="sxs-lookup"><span data-stu-id="76f20-182">You must specify "-EnableBGP $True" tooenable BGP for this connection.</span></span> <span data-ttu-id="76f20-183">Zoals eerder besproken, is het mogelijk toohave BGP- en niet-BGP-verbindingen voor Hallo dezelfde Azure VPN-Gateway.</span><span class="sxs-lookup"><span data-stu-id="76f20-183">As discussed earlier, it is possible toohave both BGP and non-BGP connections for hello same Azure VPN Gateway.</span></span> <span data-ttu-id="76f20-184">Tenzij BGP is ingeschakeld in de eigenschap connection hello, wordt Azure niet BGP inschakelen voor deze verbinding Hoewel BGP-parameters zijn al geconfigureerd op beide gateways.</span><span class="sxs-lookup"><span data-stu-id="76f20-184">Unless BGP is enabled in hello connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="76f20-185">Hallo bevat volgende voorbeeld de parameters van Hallo die Hallo BGP-configuratiesectie aangaan op uw on-premises VPN-apparaat voor deze oefening:</span><span class="sxs-lookup"><span data-stu-id="76f20-185">hello following example lists hello parameters you enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="76f20-186">Hallo-verbinding is gemaakt na een paar minuten en Hallo BGP peering sessie begint zodra Hallo IPsec-verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="76f20-186">hello connection is established after a few minutes, and hello BGP peering session starts once hello IPsec connection is established.</span></span>

## <span data-ttu-id="76f20-187"><a name ="v2vbgp"></a>Deel 3 – een VNet-naar-VNet verbinding maken met BGP</span><span class="sxs-lookup"><span data-stu-id="76f20-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="76f20-188">In deze sectie voegt een VNet-naar-VNet-verbinding met BGP, zoals wordt weergegeven in het volgende diagram Hallo:</span><span class="sxs-lookup"><span data-stu-id="76f20-188">This section adds a VNet-to-VNet connection with BGP, as shown in hello following diagram:</span></span>

![BGP voor VNet-naar-VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="76f20-190">Hallo instructies te volgen blijven uit de vorige stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="76f20-190">hello following instructions continue from hello previous steps.</span></span> <span data-ttu-id="76f20-191">U moet voltooien [deel I](#enablebgp) toocreate en configureer TestVNet1 en VPN-Gateway met BGP Hallo.</span><span class="sxs-lookup"><span data-stu-id="76f20-191">You must complete [Part I](#enablebgp) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="76f20-192">Stap 1: TestVNet2 en Hallo VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="76f20-192">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>

<span data-ttu-id="76f20-193">Het is belangrijk toomake ervoor dat Hallo IP-adresruimte van Hallo nieuw virtueel netwerk, TestVNet2, niet met een van uw VNet-bereiken overlapt.</span><span class="sxs-lookup"><span data-stu-id="76f20-193">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="76f20-194">In dit voorbeeld behoren virtuele netwerken Hallo toohello hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="76f20-194">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="76f20-195">U kunt de VNet-naar-VNet-verbindingen tussen de verschillende abonnementen instellen.</span><span class="sxs-lookup"><span data-stu-id="76f20-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="76f20-196">Zie voor meer informatie [een VNet-naar-VNet-verbinding configureren](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="76f20-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="76f20-197">Zorg ervoor dat u toevoegt Hallo '-EnableBgp $True ' wanneer maken Hallo verbindingen tooenable BGP.</span><span class="sxs-lookup"><span data-stu-id="76f20-197">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="76f20-198">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="76f20-198">1. Declare your variables</span></span>

<span data-ttu-id="76f20-199">Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="76f20-199">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="76f20-200">2. TestVNet2 in Hallo nieuwe resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="76f20-200">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="76f20-201">3. Hallo VPN-gateway maken voor TestVNet2 met BGP-parameters</span><span class="sxs-lookup"><span data-stu-id="76f20-201">3. Create hello VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="76f20-202">Aanvragen van een openbare IP-adres toobe toegewezen toohello gateway maakt voor uw VNet en definieer Hallo vereist subnet en IP-configuraties.</span><span class="sxs-lookup"><span data-stu-id="76f20-202">Request a public IP address toobe allocated toohello gateway you will create for your VNet and define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="76f20-203">Hallo VPN-gateway maken met Hallo AS-nummer.</span><span class="sxs-lookup"><span data-stu-id="76f20-203">Create hello VPN gateway with hello AS number.</span></span> <span data-ttu-id="76f20-204">U moet Hallo standaard een ASN overschrijven op uw Azure VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="76f20-204">You must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="76f20-205">Hallo ASN's voor Hallo VNets verbonden moet zijn verschillende tooenable BGP en transitroutering.</span><span class="sxs-lookup"><span data-stu-id="76f20-205">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="76f20-206">Stap 2: verbinding maken met de Hallo TestVNet1 en TestVNet2 gateways</span><span class="sxs-lookup"><span data-stu-id="76f20-206">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="76f20-207">In dit voorbeeld beide gateways zijn in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="76f20-207">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="76f20-208">U kunt deze stap bij het Hallo voltooien dezelfde PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="76f20-208">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="76f20-209">1. Beide gateways ophalen</span><span class="sxs-lookup"><span data-stu-id="76f20-209">1. Get both gateways</span></span>

<span data-ttu-id="76f20-210">Zorg ervoor dat u zich aanmeldt en verbinding maakt tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="76f20-210">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="76f20-211">2. Beide verbindingen maken</span><span class="sxs-lookup"><span data-stu-id="76f20-211">2. Create both connections</span></span>

<span data-ttu-id="76f20-212">In deze stap maakt u Hallo verbinding van TestVNet1 tooTestVNet2 en Hallo verbinding van TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="76f20-212">In this step, you create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="76f20-213">Ervoor tooenable BGP voor beide verbindingen zijn.</span><span class="sxs-lookup"><span data-stu-id="76f20-213">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="76f20-214">Na het voltooien van deze stappen Hallo-verbinding tot stand is gebracht na een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="76f20-214">After completing these steps, hello connection is established after a few minutes.</span></span> <span data-ttu-id="76f20-215">Hallo BGP-peeringsessie is nadat de Hallo VNet-naar-VNet-verbinding is voltooid.</span><span class="sxs-lookup"><span data-stu-id="76f20-215">hello BGP peering session is up once hello VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="76f20-216">Als u alle drie de gedeelten van deze oefening hebt voltooid, hebt u vastgesteld Hallo netwerktopologie te volgen:</span><span class="sxs-lookup"><span data-stu-id="76f20-216">If you completed all three parts of this exercise, you have established hello following network topology:</span></span>

![BGP voor VNet-naar-VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="76f20-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="76f20-218">Next steps</span></span>

<span data-ttu-id="76f20-219">Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="76f20-219">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="76f20-220">Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.</span><span class="sxs-lookup"><span data-stu-id="76f20-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
