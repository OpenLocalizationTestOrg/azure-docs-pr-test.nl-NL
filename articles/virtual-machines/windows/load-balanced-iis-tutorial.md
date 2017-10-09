---
title: aaaTutorial - Build een maximaal beschikbare toepassing op Azure Virtual machines | Microsoft Docs
description: Meer informatie over hoe toocreate een maximaal beschikbare en beveiligde toepassing in drie Windows virtuele machines met een load balancer in Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="50ef5-103">Een taakverdeling, maximaal beschikbare toepassing op Windows virtuele machines in Azure bouwen</span><span class="sxs-lookup"><span data-stu-id="50ef5-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="50ef5-104">In deze zelfstudie maakt maken u een maximaal beschikbare toepassing die is robuuste toomaintenance gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="50ef5-104">In this tutorial, you create a highly available application that is resilient toomaintenance events.</span></span> <span data-ttu-id="50ef5-105">Hallo app gebruikmaakt van een load balancer, een beschikbaarheidsset en drie Windows virtuele machines (VM's).</span><span class="sxs-lookup"><span data-stu-id="50ef5-105">hello app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="50ef5-106">Deze zelfstudie IIS installeert, maar u kunt deze zelfstudie toodeploy wordt gebruikt door een andere toepassing framework Hallo dezelfde hoge beschikbaarheid onderdelen en richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="50ef5-106">This tutorial installs IIS, though you can use this tutorial toodeploy a different application framework using hello same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="50ef5-107">Stap 1: vereisten voor Azure</span><span class="sxs-lookup"><span data-stu-id="50ef5-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="50ef5-108">toocomplete in deze zelfstudie maakt voor zorgen Hallo meest recente geïnstalleerd [Azure PowerShell](/powershell/azure/overview) module.</span><span class="sxs-lookup"><span data-stu-id="50ef5-108">toocomplete this tutorial, make sure that you have installed hello latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="50ef5-109">Eerst aanmelden tooyour Azure-abonnement met Hallo Login-AzureRmAccount opdracht en volg Hallo op het scherm aanwijzingen.</span><span class="sxs-lookup"><span data-stu-id="50ef5-109">First, log in tooyour Azure subscription with hello Login-AzureRmAccount command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="50ef5-110">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="50ef5-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="50ef5-111">Voordat u een andere Azure-resources maken kunt, moet u toocreate een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="50ef5-111">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="50ef5-112">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westeurope` regio:</span><span class="sxs-lookup"><span data-stu-id="50ef5-112">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="50ef5-113">Stap 2: beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="50ef5-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="50ef5-114">Virtuele machines kunnen worden gemaakt tussen logische fouttolerantie en domeinen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="50ef5-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="50ef5-115">Elk domein logische vertegenwoordigt een deel van de hardware in Hallo onderliggende Azure-datacenter.</span><span class="sxs-lookup"><span data-stu-id="50ef5-115">Each logical domain represents a portion of hardware in hello underlying Azure datacenter.</span></span> <span data-ttu-id="50ef5-116">Wanneer u twee of meer virtuele machines maakt, worden uw resources berekenings- en verdeeld over deze domeinen.</span><span class="sxs-lookup"><span data-stu-id="50ef5-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="50ef5-117">Deze verdeling onderhoudt Hallo beschikbaarheid van uw app als een hardware-onderdeel onderhoud moet.</span><span class="sxs-lookup"><span data-stu-id="50ef5-117">This distribution maintains hello availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="50ef5-118">Beschikbaarheidssets kunnen u deze logische domeinen met fouten en update definiëren.</span><span class="sxs-lookup"><span data-stu-id="50ef5-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="50ef5-119">Maken van een beschikbaarheidsset met [nieuw AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="50ef5-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="50ef5-120">Hallo volgende voorbeeld maakt u een beschikbaarheidsset benoemde `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="50ef5-120">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="50ef5-121">Stap 3: het maken van de load balancer</span><span class="sxs-lookup"><span data-stu-id="50ef5-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="50ef5-122">Een Azure load balancer wordt verkeer over een reeks gedefinieerde virtuele machines met regels voor load balancer.</span><span class="sxs-lookup"><span data-stu-id="50ef5-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="50ef5-123">Een health test een bepaalde poort op elke virtuele machine bewaakt en distribueert u alleen verkeer tooan operationele VM.</span><span class="sxs-lookup"><span data-stu-id="50ef5-123">A health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="50ef5-124">Openbare IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="50ef5-124">Create public IP address</span></span>

<span data-ttu-id="50ef5-125">tooaccess uw app op Internet, Hallo toewijzen een openbare IP-adres toohello load balancer.</span><span class="sxs-lookup"><span data-stu-id="50ef5-125">tooaccess your app on hello Internet, assign a public IP address toohello load balancer.</span></span> <span data-ttu-id="50ef5-126">Maken van een openbaar IP-adres met [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="50ef5-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="50ef5-127">Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="50ef5-127">hello following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="50ef5-128">Load balancer maken</span><span class="sxs-lookup"><span data-stu-id="50ef5-128">Create load balancer</span></span>

<span data-ttu-id="50ef5-129">Maken van een frontend-IP-adres met [nieuw AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="50ef5-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="50ef5-130">Hallo volgende voorbeeld wordt een frontend-IP-adres met de naam `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="50ef5-130">hello following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="50ef5-131">Maak een back-end-adresgroep met [nieuw AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="50ef5-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="50ef5-132">Hallo volgende voorbeeld wordt een back-end-adresgroep met de naam `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="50ef5-132">hello following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="50ef5-133">Maak nu Hallo load balancer met [nieuw AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="50ef5-133">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="50ef5-134">Hallo volgende voorbeeld maakt u een load balancer met de naam `myLoadBalancer` met Hallo `myPublicIP` adres:</span><span class="sxs-lookup"><span data-stu-id="50ef5-134">hello following example creates a load balancer named `myLoadBalancer` using hello `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="50ef5-135">Maken van de health test</span><span class="sxs-lookup"><span data-stu-id="50ef5-135">Create health probe</span></span>

<span data-ttu-id="50ef5-136">tooallow hello load balancer toomonitor Hallo status van uw app, dat u een health test gebruiken.</span><span class="sxs-lookup"><span data-stu-id="50ef5-136">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="50ef5-137">Hallo health test wordt dynamisch toegevoegd of verwijderd van virtuele machines van Hallo load balancer wisselen op basis van hun antwoord toohealth controles.</span><span class="sxs-lookup"><span data-stu-id="50ef5-137">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="50ef5-138">Standaard wordt een virtuele machine verwijderd uit Hallo load balancer-distributie na twee opeenvolgende fouten met intervallen van 15 seconden.</span><span class="sxs-lookup"><span data-stu-id="50ef5-138">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="50ef5-139">Maken van een health test met [toevoegen AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="50ef5-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="50ef5-140">Hallo volgende voorbeeld wordt een health test met de naam `myHealthProbe` die elke VM bewaakt:</span><span class="sxs-lookup"><span data-stu-id="50ef5-140">hello following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="50ef5-141">Load balancer-regel maken</span><span class="sxs-lookup"><span data-stu-id="50ef5-141">Create load balancer rule</span></span>

<span data-ttu-id="50ef5-142">Een load balancer-regel is gebruikte toodefine hoe verkeer wordt gedistribueerde toohello virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="50ef5-142">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span>

<span data-ttu-id="50ef5-143">Maken van een regel voor load balancer met [toevoegen AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="50ef5-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="50ef5-144">Hallo volgende voorbeeld maakt u een regel voor load balancer met de naam `myLoadBalancerRule` en verkeer op poort sluitend `80`:</span><span class="sxs-lookup"><span data-stu-id="50ef5-144">hello following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="50ef5-145">Hallo load balancer is met bijwerken [Set AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="50ef5-145">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="50ef5-146">Stap 4 - netwerken configureren</span><span class="sxs-lookup"><span data-stu-id="50ef5-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="50ef5-147">Elke virtuele machine heeft een of meer virtuele netwerkinterfacekaarten (NIC's) die tooa virtueel netwerk verbinden.</span><span class="sxs-lookup"><span data-stu-id="50ef5-147">Each VM has one or more virtual network interface cards (NICs) that connect tooa virtual network.</span></span> <span data-ttu-id="50ef5-148">Dit virtuele netwerk, toofilter-verkeer op basis van gedefinieerde toegangsregels is beveiligd.</span><span class="sxs-lookup"><span data-stu-id="50ef5-148">This virtual network is secured toofilter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="50ef5-149">Virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="50ef5-149">Create virtual network</span></span>

<span data-ttu-id="50ef5-150">Configureer eerst een subnet met [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="50ef5-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="50ef5-151">Hallo volgende voorbeeld wordt een subnet met de naam `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="50ef5-151">hello following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="50ef5-152">tooprovide network connectivity tooyour virtuele machines, maak een virtueel netwerk met [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="50ef5-152">tooprovide network connectivity tooyour VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="50ef5-153">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam `myVnet` met `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="50ef5-153">hello following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="50ef5-154">Netwerkbeveiliging configureren</span><span class="sxs-lookup"><span data-stu-id="50ef5-154">Configure network security</span></span>

<span data-ttu-id="50ef5-155">Een Azure [netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md) (NSG) Hiermee wordt bepaald binnenkomend en uitgaand verkeer voor een of meer virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="50ef5-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="50ef5-156">Netwerkbeveiligingsgroepen toestaan of weigeren van netwerkverkeer op een specifieke poort of een poortbereik.</span><span class="sxs-lookup"><span data-stu-id="50ef5-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="50ef5-157">Deze regels kunnen ook een voorvoegsel voor bronadres bevatten, zodat alleen verkeer dat afkomstig is op een vooraf gedefinieerde bron met een virtuele machine communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="50ef5-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="50ef5-158">tooallow web-verkeer tooreach uw app, maakt u een groep van de netwerkbeveiligingsregel met [nieuw AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="50ef5-158">tooallow web traffic tooreach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="50ef5-159">Hallo volgende voorbeeld wordt een groep netwerkbeveiligingsregel met de naam `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="50ef5-159">hello following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow
```

<span data-ttu-id="50ef5-160">Maken van een netwerkbeveiligingsgroep met [nieuw AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="50ef5-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="50ef5-161">Hallo volgende voorbeeld maakt u een NSG met de naam `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="50ef5-161">hello following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="50ef5-162">Toevoegen van Hallo beveiliging groep toohello netwerksubnet met [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="50ef5-162">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="50ef5-163">Update Hallo virtueel netwerk met [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="50ef5-163">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="50ef5-164">Netwerkinterfacekaarten voor virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="50ef5-164">Create virtual network interface cards</span></span>

<span data-ttu-id="50ef5-165">Load balancers-functie met Hallo virtuele NIC-bron in plaats van Hallo werkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="50ef5-165">Load balancers function with hello virtual NIC resource rather than hello actual VM.</span></span> <span data-ttu-id="50ef5-166">Hallo virtuele NIC verbonden toohello load balancer en vervolgens tooa VM gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="50ef5-166">hello virtual NIC is connected toohello load balancer, and then attached tooa VM.</span></span>

<span data-ttu-id="50ef5-167">Maken van een virtuele NIC met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="50ef5-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="50ef5-168">Hallo maakt volgende voorbeeld drie virtuele NIC's.</span><span class="sxs-lookup"><span data-stu-id="50ef5-168">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="50ef5-169">(Een virtuele NIC voor elke VM die u maakt voor uw app in hello te volgen stappen):</span><span class="sxs-lookup"><span data-stu-id="50ef5-169">(One virtual NIC for each VM you create for your app in hello following steps):</span></span>


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="50ef5-170">Stap 5: virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="50ef5-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="50ef5-171">Met alle Hallo onderliggende onderdelen geïmplementeerd, kunt u nu maximaal beschikbare virtuele machines toorun uw app maken.</span><span class="sxs-lookup"><span data-stu-id="50ef5-171">With all hello underlying components in place, you can now create highly available VMs toorun your app.</span></span> 

<span data-ttu-id="50ef5-172">Hallo-gebruikersnaam en wachtwoord nodig voor Hallo-beheerdersaccount op Hallo virtuele machine met ophalen [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="50ef5-172">Get hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="50ef5-173">Maken van Hallo virtuele machines met [nieuw AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Toevoegen AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), en [nieuwe-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="50ef5-173">Create hello VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="50ef5-174">Hallo volgende voorbeeld maakt drie virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="50ef5-174">hello following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

<span data-ttu-id="50ef5-175">Het duurt enkele minuten toocreate en configureer alle drie virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="50ef5-175">It takes several minutes toocreate and configure all three VMs.</span></span> <span data-ttu-id="50ef5-176">Hallo load balancer health test automatisch gedetecteerd wanneer Hallo-app wordt uitgevoerd op elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="50ef5-176">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="50ef5-177">Zodra het Hallo-app wordt uitgevoerd, begint Hallo load balancer-regel toodistribute verkeer.</span><span class="sxs-lookup"><span data-stu-id="50ef5-177">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>

### <a name="install-hello-app"></a><span data-ttu-id="50ef5-178">Hallo-app installeren</span><span class="sxs-lookup"><span data-stu-id="50ef5-178">Install hello app</span></span> 

<span data-ttu-id="50ef5-179">Virtuele machine van Azure-extensies zijn gebruikte tooautomate virtuele machine configuratietaken zoals toepassingen installeren en configureren van het besturingssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="50ef5-179">Azure virtual machine extensions are used tooautomate virtual machine configuration tasks such as installing applications and configuring hello operating system.</span></span> <span data-ttu-id="50ef5-180">Hallo [extensie voor aangepaste scripts voor Windows](./../virtual-machines-windows-extensions-customscript.md) gebruikte toorun is een PowerShell-script op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="50ef5-180">hello [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used toorun any PowerShell script on hello virtual machine.</span></span> <span data-ttu-id="50ef5-181">Hallo script worden opgeslagen in Azure storage, een willekeurig toegankelijk eindpunt van de HTTP- of worden ingesloten in de configuratie voor de uitbreiding van Hallo aangepast script.</span><span class="sxs-lookup"><span data-stu-id="50ef5-181">hello script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in hello custom script extension configuration.</span></span> <span data-ttu-id="50ef5-182">Wanneer u de aangepaste scriptextensie hello, beheert hello Azure VM-agent Hallo script worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="50ef5-182">When using hello custom script extension, hello Azure VM agent manages hello script execution.</span></span>

<span data-ttu-id="50ef5-183">Gebruik [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Hallo aangepaste scriptextensie.</span><span class="sxs-lookup"><span data-stu-id="50ef5-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello custom script extension.</span></span> <span data-ttu-id="50ef5-184">Hallo-extensie wordt uitgevoerd `powershell Add-WindowsFeature Web-Server` tooinstall Hallo IIS-webserver:</span><span class="sxs-lookup"><span data-stu-id="50ef5-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a><span data-ttu-id="50ef5-185">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="50ef5-185">Test your app</span></span>

<span data-ttu-id="50ef5-186">Hallo openbare IP-adres van de load balancer met verkrijgen [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="50ef5-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="50ef5-187">Hallo volgende voorbeeld Hallo IP-adres krijgt voor `myPublicIP` eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="50ef5-187">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="50ef5-188">Voer Hallo openbaar IP-adres in de webbrowser tooa.</span><span class="sxs-lookup"><span data-stu-id="50ef5-188">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="50ef5-189">Met Hallo NSG regel aanwezig, wordt Hallo standaard IIS-website weergegeven.</span><span class="sxs-lookup"><span data-stu-id="50ef5-189">With hello NSG rule in place, hello default IIS website is displayed.</span></span> 

![Standaardsite van IIS](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="50ef5-191">Stap 6 – beheertaken</span><span class="sxs-lookup"><span data-stu-id="50ef5-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="50ef5-192">Mogelijk moet u tooperform onderhoud op Hallo van virtuele machines waarop uw app, zoals het installeren van updates voor het besturingssysteem wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="50ef5-192">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="50ef5-193">toodeal met tooyour-app voor verkeer, moet u mogelijk tooadd extra virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="50ef5-193">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="50ef5-194">Deze sectie leest u hoe tooremove of een virtuele machine van Hallo load balancer toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="50ef5-194">This section shows you how tooremove or add a VM from hello load balancer.</span></span> 

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="50ef5-195">Een virtuele machine van Hallo load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="50ef5-195">Remove a VM from hello load balancer</span></span>

<span data-ttu-id="50ef5-196">Een virtuele machine verwijderen uit Hallo back-endadresgroep hello loadbalancerbackendaddresspools gebruikt de eigenschap van netwerkinterfacekaart Hallo herstelt.</span><span class="sxs-lookup"><span data-stu-id="50ef5-196">Remove a VM from hello backend address pool by resetting hello LoadBalancerBackendAddressPools property of hello network interface card.</span></span>

<span data-ttu-id="50ef5-197">Hallo-netwerkinterfacekaart met ophalen [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="50ef5-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="50ef5-198">Hallo loadbalancerbackendaddresspools gebruikt eigenschap van netwerkinterfacekaart hello te instellen $null:</span><span class="sxs-lookup"><span data-stu-id="50ef5-198">Set hello LoadBalancerBackendAddressPools property of hello network interface card too$null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="50ef5-199">Hallo netwerkinterfacekaart bijwerken:</span><span class="sxs-lookup"><span data-stu-id="50ef5-199">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="50ef5-200">Een VM toohello load balancer toevoegen</span><span class="sxs-lookup"><span data-stu-id="50ef5-200">Add a VM toohello load balancer</span></span>

<span data-ttu-id="50ef5-201">Na het uitvoeren van onderhoud van de virtuele machine of als u tooexpand capaciteit moet, toe te voegen Hallo NIC van een VM toohello back-end-adresgroep Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="50ef5-201">After performing VM maintenance, or if you need tooexpand capacity, adding hello NIC of a VM toohello backend address pool of hello load balancer.</span></span>

<span data-ttu-id="50ef5-202">Hallo load balancer ophalen:</span><span class="sxs-lookup"><span data-stu-id="50ef5-202">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="50ef5-203">Hallo back-endadresgroep van netwerkinterfacekaart van Hallo load balancer toohello toevoegen:</span><span class="sxs-lookup"><span data-stu-id="50ef5-203">Add hello backend address pool of hello load balancer toohello network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="50ef5-204">Hallo netwerkinterfacekaart bijwerken:</span><span class="sxs-lookup"><span data-stu-id="50ef5-204">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="50ef5-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="50ef5-205">Next Steps</span></span>

<span data-ttu-id="50ef5-206">Voorbeelden: [Azure virtuele Machine PowerShell-voorbeeldscripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="50ef5-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
