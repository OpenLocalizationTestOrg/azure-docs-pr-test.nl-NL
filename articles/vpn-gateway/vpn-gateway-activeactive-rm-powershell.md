---
title: 'Actieve S2S VPN-verbindingen configureren voor VPN-Gateways: Azure Resource Manager: PowerShell | Microsoft Docs'
description: In dit artikel begeleidt u bij het configureren van actieve verbindingen met Azure VPN-Gateways met Azure Resource Manager en PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="5a96d-103">Actieve S2S VPN-verbindingen met Azure VPN-Gateways configureren</span><span class="sxs-lookup"><span data-stu-id="5a96d-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="5a96d-104">Dit artikel begeleidt u bij Hallo stappen toocreate actieve cross-premises en VNet-naar-VNet-verbindingen met Hallo Resource Manager-implementatiemodel en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5a96d-104">This article walks you through hello steps toocreate active-active cross-premises and VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="5a96d-105">Over maximaal beschikbare Cross-Premises verbindingen</span><span class="sxs-lookup"><span data-stu-id="5a96d-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="5a96d-106">hoge beschikbaarheid tooachieve voor cross-premises en VNet-naar-VNet-connectiviteit, moet u meerdere VPN-gateways implementeert en meerdere parallelle verbindingen tussen uw netwerken en Azure tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="5a96d-106">tooachieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="5a96d-107">Zie [maximaal beschikbare Cross-Premises en VNet-naar-VNet-connectiviteit](vpn-gateway-highlyavailable.md) voor een overzicht van opties voor netwerkconnectiviteit en -topologie.</span><span class="sxs-lookup"><span data-stu-id="5a96d-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="5a96d-108">Dit artikel bevat instructies Hallo tooset van een actieve cross-premises VPN-verbinding en de actieve verbinding tussen twee virtuele netwerken:</span><span class="sxs-lookup"><span data-stu-id="5a96d-108">This article provides hello instructions tooset up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="5a96d-109">Deel 1 - maken en configureren van uw Azure VPN-gateway in de actieve-actieve modus</span><span class="sxs-lookup"><span data-stu-id="5a96d-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="5a96d-110">Deel 2: actieve cross-premises verbindingen tot stand brengen</span><span class="sxs-lookup"><span data-stu-id="5a96d-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="5a96d-111">Deel 3 - actief / actief-VNet-naar-VNet-verbindingen tot stand brengen</span><span class="sxs-lookup"><span data-stu-id="5a96d-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="5a96d-112">Deel 4 - bestaande gateway tussen actieve en stand-by active-Update</span><span class="sxs-lookup"><span data-stu-id="5a96d-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="5a96d-113">U kunt deze samen toobuild een meer complexe, maximaal beschikbare netwerktopologie die voldoet aan uw behoeften kunt combineren.</span><span class="sxs-lookup"><span data-stu-id="5a96d-113">You can combine these together toobuild a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a96d-114">Houd er rekening mee dat Hallo actieve-actieve modus maakt gebruik van alleen Hallo SKU's te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a96d-114">Please note that hello active-active mode uses only hello following SKUs:</span></span> 
  * <span data-ttu-id="5a96d-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="5a96d-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="5a96d-116">HighPerformance (voor oude verouderde SKU's)</span><span class="sxs-lookup"><span data-stu-id="5a96d-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="5a96d-117"><a name ="aagateway"></a>Deel 1 - maken en configureren van actieve VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="5a96d-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="5a96d-118">Hallo stappen te volgen configureert in actieve modi uw Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="5a96d-118">hello following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="5a96d-119">Hallo belangrijke verschillen tussen Hallo actieve en stand-by active-gateways:</span><span class="sxs-lookup"><span data-stu-id="5a96d-119">hello key differences between hello active-active and active-standby gateways:</span></span>

* <span data-ttu-id="5a96d-120">U moet twee IP-Gateway-configuraties toocreate met twee openbare IP-adressen</span><span class="sxs-lookup"><span data-stu-id="5a96d-120">You need toocreate two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="5a96d-121">U moet Hallo EnableActiveActiveFeature markering instellen</span><span class="sxs-lookup"><span data-stu-id="5a96d-121">You need set hello EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="5a96d-122">Hallo gateway-SKU moet VpnGw1, VpnGw2, VpnGw3 of HighPerformance (verouderde SKU).</span><span class="sxs-lookup"><span data-stu-id="5a96d-122">hello gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="5a96d-123">Hallo zijn andere eigenschappen Hallo hetzelfde als Hallo actieve actieve gateways.</span><span class="sxs-lookup"><span data-stu-id="5a96d-123">hello other properties are hello same as hello non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="5a96d-124">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="5a96d-124">Before you begin</span></span>
* <span data-ttu-id="5a96d-125">Controleer of u een Azure-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="5a96d-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="5a96d-126">Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a96d-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5a96d-127">U moet tooinstall hello Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5a96d-127">You'll need tooinstall hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="5a96d-128">Zie [overzicht van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van Hallo PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5a96d-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="5a96d-129">Stap 1: Maak en configureer VNet1</span><span class="sxs-lookup"><span data-stu-id="5a96d-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="5a96d-130">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="5a96d-130">1. Declare your variables</span></span>
<span data-ttu-id="5a96d-131">Voor deze oefening declareert u eerst de variabelen.</span><span class="sxs-lookup"><span data-stu-id="5a96d-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="5a96d-132">Hallo onderstaand voorbeeld declareert Hallo variabelen met Hallo waarden voor deze oefening.</span><span class="sxs-lookup"><span data-stu-id="5a96d-132">hello example below declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="5a96d-133">Ervoor tooreplace Hallo waarden door uw eigen worden wanneer u configureert voor productie.</span><span class="sxs-lookup"><span data-stu-id="5a96d-133">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="5a96d-134">U kunt deze variabelen gebruiken als u via Hallo stappen toobecome bekend zijn met dit type configuratie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="5a96d-134">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="5a96d-135">Wijzig variabelen hello, en kopieert en plakt u in de PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="5a96d-135">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
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
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="5a96d-136">2. Verbinding maken met tooyour abonnement en een nieuwe resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="5a96d-136">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="5a96d-137">Zorg ervoor dat u overschakelt tooPowerShell modus toouse Hallo Resource Manager-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5a96d-137">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="5a96d-138">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5a96d-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="5a96d-139">Open de PowerShell-console en tooyour-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="5a96d-139">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="5a96d-140">Gebruik Hallo volgende steekproef toohelp die u verbinding kunt maken:</span><span class="sxs-lookup"><span data-stu-id="5a96d-140">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="5a96d-141">3. TestVNet1 maken</span><span class="sxs-lookup"><span data-stu-id="5a96d-141">3. Create TestVNet1</span></span>
<span data-ttu-id="5a96d-142">Hallo onderstaand voorbeeld maakt een virtueel netwerk met de naam TestVNet1 en drie subnetten, één naam GatewaySubnet, een opgeroepen FrontEnd en één opgeroepen back-end.</span><span class="sxs-lookup"><span data-stu-id="5a96d-142">hello sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="5a96d-143">Wanneer u de waarden vervangt, is het belangrijk dat u de juiste namen voor de gatewaysubnets gebruikt, in het bijzonder GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="5a96d-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="5a96d-144">Als u een andere naam kiest, mislukt het maken van de gateway.</span><span class="sxs-lookup"><span data-stu-id="5a96d-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="5a96d-145">Stap 2: Hallo VPN-gateway voor TestVNet1 maken met de actieve-actieve modus</span><span class="sxs-lookup"><span data-stu-id="5a96d-145">Step 2 - Create hello VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="5a96d-146">1. Hallo openbare IP-adressen en IP-configuraties van gateway maken</span><span class="sxs-lookup"><span data-stu-id="5a96d-146">1. Create hello public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="5a96d-147">Aanvraag twee openbare IP-adressen toobe toegewezen toohello gateway u voor uw VNet maakt.</span><span class="sxs-lookup"><span data-stu-id="5a96d-147">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="5a96d-148">U zult ook definiëren Hallo subnet en IP-configuraties die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="5a96d-148">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="5a96d-149">2. Hallo VPN-gateway maken met een actief / actief-configuratie</span><span class="sxs-lookup"><span data-stu-id="5a96d-149">2. Create hello VPN gateway with active-active configuration</span></span>
<span data-ttu-id="5a96d-150">De virtuele netwerkgateway Hallo voor TestVNet1 maken.</span><span class="sxs-lookup"><span data-stu-id="5a96d-150">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="5a96d-151">Houd er rekening mee dat er twee GatewayIpConfig vermeldingen zijn en Hallo EnableActiveActiveFeature-vlag is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5a96d-151">Note that there are two GatewayIpConfig entries, and hello EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="5a96d-152">Maken van een gateway kan even duren (45 minuten of meer toocomplete).</span><span class="sxs-lookup"><span data-stu-id="5a96d-152">Creating a gateway can take a while (45 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a><span data-ttu-id="5a96d-153">3. Hallo gateway openbare IP-adressen en Hallo BGP-Peer-IP-adres verkrijgen</span><span class="sxs-lookup"><span data-stu-id="5a96d-153">3. Obtain hello gateway public IP addresses and hello BGP Peer IP address</span></span>
<span data-ttu-id="5a96d-154">Zodra Hallo gateway is gemaakt, moet u tooobtain Hallo BGP-Peer-IP-adres op Hallo Azure VPN-Gateway.</span><span class="sxs-lookup"><span data-stu-id="5a96d-154">Once hello gateway is created, you will need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="5a96d-155">Dit adres is de benodigde tooconfigure hello Azure VPN-Gateway als een BGP-Peer voor uw on-premises VPN-apparaten.</span><span class="sxs-lookup"><span data-stu-id="5a96d-155">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="5a96d-156">Gebruik Hallo cmdlets tooshow Hallo twee openbare IP-adressen toegewezen voor uw VPN-gateway en de bijbehorende BGP-Peer-IP-adressen voor elk gatewayexemplaar te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a96d-156">Use hello following cmdlets tooshow hello two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

<span data-ttu-id="5a96d-157">Hallo volgorde van Hallo openbare IP-adressen voor Hallo gatewayexemplaren en bijbehorende BGP-Peering adressen zijn Hallo Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="5a96d-157">hello order of hello public IP addresses for hello gateway instances and hello corresponding BGP Peering Addresses are hello same.</span></span> <span data-ttu-id="5a96d-158">In dit voorbeeld Hallo gateway-VM met openbare IP-adres van 40.112.190.5 10.12.255.4 gebruikt als het adres BGP-Peering en Hallo gateway met 138.91.156.129 10.12.255.5 wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5a96d-158">In this example, hello gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and hello gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="5a96d-159">Deze informatie is nodig bij het instellen van uw on-premises VPN-apparaten toohello actieve gateway verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="5a96d-159">This information is needed when you set up your on premises VPN devices connecting toohello active-active gateway.</span></span> <span data-ttu-id="5a96d-160">Hallo-gateway wordt weergegeven in Hallo diagram hieronder met alle adressen:</span><span class="sxs-lookup"><span data-stu-id="5a96d-160">hello gateway is shown in hello diagram below with all addresses:</span></span>

![actieve-actieve gateway](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="5a96d-162">Zodra Hallo gateway is gemaakt, kunt u deze gateway tooestablish actieve cross-premises of VNet-naar-VNet-verbinding.</span><span class="sxs-lookup"><span data-stu-id="5a96d-162">Once hello gateway is created, you can use this gateway tooestablish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="5a96d-163">Hallo uit te voeren doorlopen Hallo stappen toocomplete Hallo oefening.</span><span class="sxs-lookup"><span data-stu-id="5a96d-163">hello following sections will walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="5a96d-164"><a name ="aacrossprem"></a>Deel 2: een actieve cross-premises-verbinding tot stand brengen</span><span class="sxs-lookup"><span data-stu-id="5a96d-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="5a96d-165">tooestablish een cross-premises-verbinding, moet u een lokale netwerkgateway toorepresent toocreate uw on-premises VPN-apparaat en een verbinding tooconnect hello Azure VPN-gateway met de lokale netwerkgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a96d-165">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello Azure VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="5a96d-166">In dit voorbeeld is hello Azure VPN-gateway actief / actief-actief.</span><span class="sxs-lookup"><span data-stu-id="5a96d-166">In this example, hello Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="5a96d-167">Als gevolg hiervan, zelfs als er slechts één on-premises VPN-apparaat (lokale netwerkgateway) en één verbindingsbron, beide exemplaren van Azure VPN-gateway tot stand brengen S2S VPN-tunnels met Hallo on-premises-apparaat.</span><span class="sxs-lookup"><span data-stu-id="5a96d-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with hello on-premises device.</span></span>

<span data-ttu-id="5a96d-168">Voordat u doorgaat, Controleer of u hebt voltooid [Part 1](#aagateway) van deze oefening.</span><span class="sxs-lookup"><span data-stu-id="5a96d-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="5a96d-169">Stap 1 - maken en configureren van de lokale netwerkgateway Hallo</span><span class="sxs-lookup"><span data-stu-id="5a96d-169">Step 1 - Create and configure hello local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="5a96d-170">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="5a96d-170">1. Declare your variables</span></span>
<span data-ttu-id="5a96d-171">In deze oefening blijven toobuild Hallo configuratie wordt weergegeven in het Hallo-diagram.</span><span class="sxs-lookup"><span data-stu-id="5a96d-171">This exercise will continue toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="5a96d-172">Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="5a96d-172">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="5a96d-173">Een aantal dingen toonote met betrekking tot Hallo lokale netwerk gateway parameters:</span><span class="sxs-lookup"><span data-stu-id="5a96d-173">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="5a96d-174">Hallo lokale netwerkgateway kan zich in dezelfde hello of een andere locatie en resource als Hallo VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="5a96d-174">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="5a96d-175">Dit voorbeeld ziet u ze in verschillende resourcegroepen, maar in Hallo dezelfde Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="5a96d-175">This example shows them in different resource groups but in hello same Azure location.</span></span>
* <span data-ttu-id="5a96d-176">Als er slechts één on-premises VPN-apparaat zoals hierboven beschreven, worden de Hallo actieve verbinding kunt werken met of zonder BGP-protocol.</span><span class="sxs-lookup"><span data-stu-id="5a96d-176">If there is only one on-premises VPN device as shown above, hello active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="5a96d-177">In dit voorbeeld gebruikt BGP voor Hallo cross-premises-verbinding.</span><span class="sxs-lookup"><span data-stu-id="5a96d-177">This example uses BGP for hello cross-premises connection.</span></span>
* <span data-ttu-id="5a96d-178">Als BGP is ingeschakeld, is Hallo voorvoegsel dat u toodeclare nodig voor de lokale netwerkgateway Hallo Hallo host-adres van uw BGP-Peer-IP-adres op uw VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="5a96d-178">If BGP is enabled, hello prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="5a96d-179">In dit geval is een /32 prefix '10.52.255.253/32'.</span><span class="sxs-lookup"><span data-stu-id="5a96d-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="5a96d-180">U moet verschillende ASN van BGP tussen uw on-premises netwerken en Azure VNet gebruiken als een herinnering.</span><span class="sxs-lookup"><span data-stu-id="5a96d-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="5a96d-181">Als ze zijn dezelfde hello, moet u toochange uw VNet ASN als Hallo ASN toopeer in uw on-premises VPN-apparaat al worden gebruikt met andere BGP-neighbors.</span><span class="sxs-lookup"><span data-stu-id="5a96d-181">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="5a96d-182">2. De lokale netwerkgateway Hallo voor Site5 maken</span><span class="sxs-lookup"><span data-stu-id="5a96d-182">2. Create hello local network gateway for Site5</span></span>
<span data-ttu-id="5a96d-183">Controleer of dat u bent nog steeds verbonden tooSubscription 1 voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="5a96d-183">Before you continue, please make sure you are still connected tooSubscription 1.</span></span> <span data-ttu-id="5a96d-184">Hallo-resourcegroep maken als deze nog niet is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a96d-184">Create hello resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="5a96d-185">Stap 2: verbinding maken met de Hallo VNet-gateway en de lokale netwerkgateway</span><span class="sxs-lookup"><span data-stu-id="5a96d-185">Step 2 - Connect hello VNet gateway and local network gateway</span></span>
#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="5a96d-186">1. Hallo twee gateways ophalen</span><span class="sxs-lookup"><span data-stu-id="5a96d-186">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="5a96d-187">2. Hallo TestVNet1 tooSite5 verbinding maken</span><span class="sxs-lookup"><span data-stu-id="5a96d-187">2. Create hello TestVNet1 tooSite5 connection</span></span>
<span data-ttu-id="5a96d-188">In deze stap maakt u Hallo verbinding van TestVNet1 tooSite5_1 met 'EnableBGP' ingesteld te$ True.</span><span class="sxs-lookup"><span data-stu-id="5a96d-188">In this step, you will create hello connection from TestVNet1 tooSite5_1 with "EnableBGP" set too$True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="5a96d-189">3. VPN- en BGP-parameters voor uw on-premises VPN-apparaat</span><span class="sxs-lookup"><span data-stu-id="5a96d-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="5a96d-190">Hallo in het volgende voorbeeld bevat Hallo-parameters u in de configuratiesectie BGP Hallo op uw on-premises VPN-apparaat voor deze oefening voert:</span><span class="sxs-lookup"><span data-stu-id="5a96d-190">hello example below lists hello parameters you will enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="5a96d-191">Site5 ASN: 65050</span><span class="sxs-lookup"><span data-stu-id="5a96d-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="5a96d-192">BGP-IP-Site5: 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="5a96d-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="5a96d-193">Tooannounce-prefixes: (bijvoorbeeld) 10.51.0.0/16 en 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5a96d-193">Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="5a96d-194">Azure VNet ASN: 65010</span><span class="sxs-lookup"><span data-stu-id="5a96d-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="5a96d-195">Azure VNet BGP IP 1: 10.12.255.4 voor tunnel too40.112.190.5</span><span class="sxs-lookup"><span data-stu-id="5a96d-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5</span></span>
    - <span data-ttu-id="5a96d-196">Azure VNet BGP IP 2: 10.12.255.5 voor tunnel too138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="5a96d-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129</span></span>
    - <span data-ttu-id="5a96d-197">Statische routes: bestemming 10.12.255.4/32, nexthop Hallo VPN-tunnel-interface too40.112.190.5 bestemming 10.12.255.5/32, nexthop Hallo VPN-tunnel-interface too138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="5a96d-197">Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5                        Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129</span></span>
    - <span data-ttu-id="5a96d-198">eBGP Multihop: Zorg ervoor dat Hallo "multihop"-optie voor eBGP is ingeschakeld op uw apparaat, indien nodig</span><span class="sxs-lookup"><span data-stu-id="5a96d-198">eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="5a96d-199">Hallo verbinding moet worden gemaakt na een paar minuten en Hallo BGP-peeringsessie wordt gestart zodra Hallo IPsec-verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="5a96d-199">hello connection should be established after a few minutes, and hello BGP peering session will start once hello IPsec connection is established.</span></span> <span data-ttu-id="5a96d-200">In dit voorbeeld is tot nu toe geconfigureerd dat slechts één on-premises VPN-apparaat, wat resulteert in Hallo diagram hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5a96d-200">This example so far has configured only one on-premises VPN device, resulting in hello diagram shown below:</span></span>

![Active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a><span data-ttu-id="5a96d-202">Stap 3: verbinding maken met twee lokale VPN-apparaten toohello actieve VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="5a96d-202">Step 3 - Connect two on-premises VPN devices toohello active-active VPN gateway</span></span>
<span data-ttu-id="5a96d-203">Als u twee VPN-apparaten op Hallo hebt dezelfde lokale netwerk, kunt u dual redundantie bereiken door de verbindende hello Azure VPN-gateway toohello tweede VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="5a96d-203">If you have two VPN devices at hello same on-premises network, you can achieve dual redundancy by connecting hello Azure VPN gateway toohello second VPN device.</span></span>

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a><span data-ttu-id="5a96d-204">1. Hallo tweede lokale-netwerkgateway voor Site5 maken</span><span class="sxs-lookup"><span data-stu-id="5a96d-204">1. Create hello second local network gateway for Site5</span></span>
<span data-ttu-id="5a96d-205">Opmerking dat IP-adres van Hallo gateway adresvoorvoegsel en adres voor BGP-peering voor Hallo tweede lokale-netwerkgateway elkaar niet met Hallo vorige lokale netwerkgateway voor Hallo dezelfde overlappen mogen lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="5a96d-205">Note that hello gateway IP address, address prefix, and BGP peering address for hello second local network gateway must not overlap with hello previous local network gateway for hello same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a><span data-ttu-id="5a96d-206">2. Verbinding maken met de Hallo VNet gateway en Hallo tweede lokale-netwerkgateway</span><span class="sxs-lookup"><span data-stu-id="5a96d-206">2. Connect hello VNet gateway and hello second local network gateway</span></span>
<span data-ttu-id="5a96d-207">Hallo-verbinding van TestVNet1 tooSite5_2 maken met 'EnableBGP' ingesteld te$ True</span><span class="sxs-lookup"><span data-stu-id="5a96d-207">Create hello connection from TestVNet1 tooSite5_2 with "EnableBGP" set too$True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="5a96d-208">3. VPN- en BGP-parameters voor uw tweede on-premises VPN-apparaat</span><span class="sxs-lookup"><span data-stu-id="5a96d-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="5a96d-209">Op deze manier onderstaande lijsten Hallo parameters voert u in Hallo tweede VPN-apparaat:</span><span class="sxs-lookup"><span data-stu-id="5a96d-209">Similarly, below lists hello parameters you will enter into hello second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="5a96d-210">Zodra het Hallo-verbinding (tunnels) worden gemaakt, hebt u twee redundante VPN-apparaten en tunnels verbinding maken met uw on-premises netwerk en Azure:</span><span class="sxs-lookup"><span data-stu-id="5a96d-210">Once hello connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![Dual-redundantie-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="5a96d-212"><a name ="aav2v"></a>Deel 3: een actieve VNet-naar-VNet-verbinding tot stand brengen</span><span class="sxs-lookup"><span data-stu-id="5a96d-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="5a96d-213">Deze sectie maakt een actief / actief-VNet-naar-VNet-verbinding met BGP.</span><span class="sxs-lookup"><span data-stu-id="5a96d-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="5a96d-214">Hallo-instructies die hieronder worden overgenomen van Hallo hierboven beschreven stappen.</span><span class="sxs-lookup"><span data-stu-id="5a96d-214">hello instructions below continue from hello previous steps listed above.</span></span> <span data-ttu-id="5a96d-215">U moet voltooien [Part 1](#aagateway) toocreate en configureer TestVNet1 en VPN-Gateway met BGP Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a96d-215">You must complete [Part 1](#aagateway) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="5a96d-216">Stap 1: TestVNet2 en Hallo VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="5a96d-216">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>
<span data-ttu-id="5a96d-217">Het is belangrijk toomake ervoor dat Hallo IP-adresruimte van Hallo nieuw virtueel netwerk, TestVNet2, niet met een van uw VNet-bereiken overlapt.</span><span class="sxs-lookup"><span data-stu-id="5a96d-217">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="5a96d-218">In dit voorbeeld behoren virtuele netwerken Hallo toohello hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="5a96d-218">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="5a96d-219">U kunt een VNet-naar-VNet-verbindingen tussen de verschillende abonnementen; instellen Raadpleeg het te[een VNet-naar-VNet-verbinding configureren](vpn-gateway-vnet-vnet-rm-ps.md) toolearn om meer details.</span><span class="sxs-lookup"><span data-stu-id="5a96d-219">You can set up VNet-to-VNet connections between different subscriptions; please refer too[Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) toolearn more details.</span></span> <span data-ttu-id="5a96d-220">Zorg ervoor dat u toevoegt Hallo '-EnableBgp $True ' wanneer maken Hallo verbindingen tooenable BGP.</span><span class="sxs-lookup"><span data-stu-id="5a96d-220">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="5a96d-221">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="5a96d-221">1. Declare your variables</span></span>
<span data-ttu-id="5a96d-222">Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="5a96d-222">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
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
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="5a96d-223">2. TestVNet2 in Hallo nieuwe resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="5a96d-223">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="5a96d-224">3. Hallo actieve VPN-gateway voor TestVNet2 maken</span><span class="sxs-lookup"><span data-stu-id="5a96d-224">3. Create hello active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="5a96d-225">Aanvraag twee openbare IP-adressen toobe toegewezen toohello gateway u voor uw VNet maakt.</span><span class="sxs-lookup"><span data-stu-id="5a96d-225">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="5a96d-226">U zult ook definiëren Hallo subnet en IP-configuraties die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="5a96d-226">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="5a96d-227">Hallo VPN-gateway maken met Hallo als getal en Hallo 'EnableActiveActiveFeature' vlag.</span><span class="sxs-lookup"><span data-stu-id="5a96d-227">Create hello VPN gateway with hello AS number and hello "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="5a96d-228">Houd er rekening mee dat u Hallo standaard een ASN op uw Azure VPN-gateways moet overschrijven.</span><span class="sxs-lookup"><span data-stu-id="5a96d-228">Note that you must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="5a96d-229">Hallo ASN's voor Hallo VNets verbonden moet zijn verschillende tooenable BGP en transitroutering.</span><span class="sxs-lookup"><span data-stu-id="5a96d-229">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="5a96d-230">Stap 2: verbinding maken met de Hallo TestVNet1 en TestVNet2 gateways</span><span class="sxs-lookup"><span data-stu-id="5a96d-230">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="5a96d-231">In dit voorbeeld beide gateways zijn in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="5a96d-231">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="5a96d-232">U kunt deze stap bij het Hallo voltooien dezelfde PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="5a96d-232">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="5a96d-233">1. Beide gateways ophalen</span><span class="sxs-lookup"><span data-stu-id="5a96d-233">1. Get both gateways</span></span>
<span data-ttu-id="5a96d-234">Zorg ervoor dat u zich aanmeldt en verbinding maakt tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="5a96d-234">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="5a96d-235">2. Beide verbindingen maken</span><span class="sxs-lookup"><span data-stu-id="5a96d-235">2. Create both connections</span></span>
<span data-ttu-id="5a96d-236">In deze stap maakt u Hallo verbinding van TestVNet1 tooTestVNet2 en Hallo verbinding van TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="5a96d-236">In this step, you will create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="5a96d-237">Ervoor tooenable BGP voor beide verbindingen zijn.</span><span class="sxs-lookup"><span data-stu-id="5a96d-237">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="5a96d-238">Na het voltooien van deze stappen Hallo verbinding maken in een paar minuten en Hallo BGP-peeringsessie zijn nadat Hallo VNet-naar-VNet-verbinding is voltooid met dubbel redundantie:</span><span class="sxs-lookup"><span data-stu-id="5a96d-238">After completing these steps, hello connection will be establish in a few minutes, and hello BGP peering session will be up once hello VNet-to-VNet connection is completed with dual redundancy:</span></span>

![Active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="5a96d-240"><a name ="aaupdate"></a>Deel 4 - bestaande gateway tussen actieve en stand-by active-Update</span><span class="sxs-lookup"><span data-stu-id="5a96d-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="5a96d-241">Hallo laatste sectie wordt beschreven hoe u een bestaande Azure VPN-gateway kunt configureren van de actieve stand-by-tooactive-actieve modus of vice versa.</span><span class="sxs-lookup"><span data-stu-id="5a96d-241">hello last section will describe how you can configure an existing Azure VPN gateway from active-standby tooactive-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="5a96d-242">Deze sectie bevat Hallo stappen tooresize een verouderde SKU (oude SKU) van een bestaande VPN-gateway van de standaard tooHighPerformance.</span><span class="sxs-lookup"><span data-stu-id="5a96d-242">This section includes hello steps tooresize a legacy SKU (old SKU) of an already created VPN gateway from Standard tooHighPerformance.</span></span> <span data-ttu-id="5a96d-243">Deze stappen voert geen upgrade van een oude verouderde SKU tooone Hallo nieuwe SKU's.</span><span class="sxs-lookup"><span data-stu-id="5a96d-243">These steps do not upgrade an old legacy SKU tooone of hello new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a><span data-ttu-id="5a96d-244">Een actieve stand-by-gateway tooactive-actieve gateway configureren</span><span class="sxs-lookup"><span data-stu-id="5a96d-244">Configure an active-standby gateway tooactive-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="5a96d-245">1. Gateway-parameters</span><span class="sxs-lookup"><span data-stu-id="5a96d-245">1. Gateway parameters</span></span>
<span data-ttu-id="5a96d-246">een gateway actief stand-by-converteert Hallo volgt naar een actief / actief-gateway.</span><span class="sxs-lookup"><span data-stu-id="5a96d-246">hello following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="5a96d-247">U moet toocreate een ander openbaar IP-adres en vervolgens een tweede Gateway IP-configuratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5a96d-247">You need toocreate another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="5a96d-248">Hieronder bevat hello parameters gebruikt:</span><span class="sxs-lookup"><span data-stu-id="5a96d-248">Below shows hello parameters used:</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a><span data-ttu-id="5a96d-249">2. Hallo openbare IP-adres maken, en voeg vervolgens Hallo tweede gateway IP-configuratie</span><span class="sxs-lookup"><span data-stu-id="5a96d-249">2. Create hello public IP address, then add hello second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a><span data-ttu-id="5a96d-250">3. Actieve-actieve modus en update Hallo gateway inschakelen</span><span class="sxs-lookup"><span data-stu-id="5a96d-250">3. Enable active-active mode and update hello gateway</span></span>
<span data-ttu-id="5a96d-251">Hallo gateway-object moet u instellen in PowerShell tootrigger Hallo feitelijke update.</span><span class="sxs-lookup"><span data-stu-id="5a96d-251">You must set hello gateway object in PowerShell tootrigger hello actual update.</span></span> <span data-ttu-id="5a96d-252">Hallo SKU van de virtuele netwerkgateway Hallo moet ook worden gewijzigd (formaat is gewijzigd) tooHighPerformance sinds deze eerder is gemaakt als standaard.</span><span class="sxs-lookup"><span data-stu-id="5a96d-252">hello SKU of hello virtual network gateway must also be changed (resized) tooHighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="5a96d-253">Deze update kan 30 too45 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="5a96d-253">This update can take 30 too45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a><span data-ttu-id="5a96d-254">Een actieve gateway tooactive stand-by-gateway configureren</span><span class="sxs-lookup"><span data-stu-id="5a96d-254">Configure an active-active gateway tooactive-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="5a96d-255">1. Gateway-parameters</span><span class="sxs-lookup"><span data-stu-id="5a96d-255">1. Gateway parameters</span></span>
<span data-ttu-id="5a96d-256">Gebruik dezelfde Hallo Hallo-naam van de Hallo IP-configuratie die u wilt dat tooremove parameters zoals hierboven, opvragen.</span><span class="sxs-lookup"><span data-stu-id="5a96d-256">Use hello same parameters as above, get hello name of hello IP configuration you want tooremove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a><span data-ttu-id="5a96d-257">2. Hallo gateway IP-configuratie verwijderen en Hallo actieve-actieve modus uitschakelen</span><span class="sxs-lookup"><span data-stu-id="5a96d-257">2. Remove hello gateway IP configuration and disable hello active-active mode</span></span>
<span data-ttu-id="5a96d-258">U moet op dezelfde manier Hallo gateway object ingesteld in PowerShell tootrigger Hallo feitelijke update.</span><span class="sxs-lookup"><span data-stu-id="5a96d-258">Similarly, you must set hello gateway object in PowerShell tootrigger hello actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="5a96d-259">Deze update kan duren too30 met te 45 minuten.</span><span class="sxs-lookup"><span data-stu-id="5a96d-259">This update can take up too30 too 45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a96d-260">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a96d-260">Next steps</span></span>
<span data-ttu-id="5a96d-261">Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5a96d-261">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="5a96d-262">Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.</span><span class="sxs-lookup"><span data-stu-id="5a96d-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
