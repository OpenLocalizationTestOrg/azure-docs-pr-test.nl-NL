---
title: aaaHow tooload saldo Windows virtuele machines in Azure | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure balancer toocreate een maximaal beschikbare en beveiligde toepassing geladen over drie Windows VM 's
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="43e20-103">Hoe tooload balans vinden tussen Windows virtuele machines in Azure toocreate een maximaal beschikbare toepassing</span><span class="sxs-lookup"><span data-stu-id="43e20-103">How tooload balance Windows virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="43e20-104">Taakverdeling biedt een hoger niveau van de beschikbaarheid van binnenkomende aanvragen verspreid over meerdere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="43e20-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="43e20-105">In deze zelfstudie leert u Hallo verschillende onderdelen van hello Azure load balancer die verkeer distribueren en bieden hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="43e20-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="43e20-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="43e20-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="43e20-107">Een Azure load balancer maken</span><span class="sxs-lookup"><span data-stu-id="43e20-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="43e20-108">Een load balancer health test maken</span><span class="sxs-lookup"><span data-stu-id="43e20-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="43e20-109">Regels voor netwerkverkeer voor de load balancer maken</span><span class="sxs-lookup"><span data-stu-id="43e20-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="43e20-110">Hallo aangepaste Scriptextensie toocreate een normale IIS-website gebruiken</span><span class="sxs-lookup"><span data-stu-id="43e20-110">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="43e20-111">Virtuele machines maken en koppelen tooa load balancer</span><span class="sxs-lookup"><span data-stu-id="43e20-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="43e20-112">Een load balancer in actie weergeven</span><span class="sxs-lookup"><span data-stu-id="43e20-112">View a load balancer in action</span></span>
> * <span data-ttu-id="43e20-113">Toevoegen of virtuele machines van een load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="43e20-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="43e20-114">Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="43e20-114">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="43e20-115">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="43e20-115">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="43e20-116">Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="43e20-116">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="43e20-117">Overzicht van Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="43e20-117">Azure load balancer overview</span></span>
<span data-ttu-id="43e20-118">Een Azure load balancer is een Layer-4 (TCP, UDP) load balancer die zorgt voor hoge beschikbaarheid door het distribueren van inkomend verkeer tussen orde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="43e20-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="43e20-119">Een load balancer health test een bepaalde poort op elke virtuele machine bewaakt en distribueert u alleen verkeer tooan operationele VM.</span><span class="sxs-lookup"><span data-stu-id="43e20-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="43e20-120">U definieert een front-end-IP-configuratie met een of meer openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="43e20-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="43e20-121">Deze front-end-IP-configuratie kan de load balancer en toepassingen toobe toegankelijk via Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="43e20-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="43e20-122">Virtuele machines verbinding tooa load balancer met behulp van de virtuele netwerkinterfacekaart (NIC).</span><span class="sxs-lookup"><span data-stu-id="43e20-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="43e20-123">toodistribute verkeer toohello VM's, een back-end-adresgroep bevat Hallo IP-adressen van Hallo virtuele (NIC's) verbonden toohello load balancer.</span><span class="sxs-lookup"><span data-stu-id="43e20-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="43e20-124">toocontrol hello stroom van verkeer, kunt u definiëren load balancerregels voor specifieke poorten en protocollen die zijn toegewezen tooyour virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="43e20-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="43e20-125">Azure load balancer maken</span><span class="sxs-lookup"><span data-stu-id="43e20-125">Create Azure load balancer</span></span>
<span data-ttu-id="43e20-126">In deze sectie beschrijft hoe u kunt maken en configureren van elk onderdeel Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="43e20-126">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="43e20-127">Voordat u de load balancer maken kunt, maakt u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="43e20-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="43e20-128">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupLoadBalancer* in Hallo *EastUS* locatie:</span><span class="sxs-lookup"><span data-stu-id="43e20-128">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="43e20-129">Een openbaar IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="43e20-129">Create a public IP address</span></span>
<span data-ttu-id="43e20-130">tooaccess uw app op Hallo Internet, moet u een openbaar IP-adres voor Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="43e20-130">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="43e20-131">Maken van een openbaar IP-adres met [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="43e20-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="43e20-132">Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam *myPublicIP* in Hallo *myResourceGroupLoadBalancer* resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="43e20-132">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="43e20-133">Een load balancer maken</span><span class="sxs-lookup"><span data-stu-id="43e20-133">Create a load balancer</span></span>
<span data-ttu-id="43e20-134">Maken van een frontend-IP-adres met [nieuw AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="43e20-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="43e20-135">Hallo volgende voorbeeld wordt een frontend-IP-adres met de naam *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="43e20-135">hello following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="43e20-136">Maak een back-end-adresgroep met [nieuw AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="43e20-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="43e20-137">Hallo volgende voorbeeld wordt een back-end-adresgroep met de naam *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="43e20-137">hello following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="43e20-138">Maak nu Hallo load balancer met [nieuw AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="43e20-138">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="43e20-139">Hallo volgende voorbeeld maakt u een load balancer met de naam *myLoadBalancer* met Hallo *myPublicIP* adres:</span><span class="sxs-lookup"><span data-stu-id="43e20-139">hello following example creates a load balancer named *myLoadBalancer* using hello *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="43e20-140">Een health test maken</span><span class="sxs-lookup"><span data-stu-id="43e20-140">Create a health probe</span></span>
<span data-ttu-id="43e20-141">tooallow hello load balancer toomonitor Hallo status van uw app, dat u een health test gebruiken.</span><span class="sxs-lookup"><span data-stu-id="43e20-141">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="43e20-142">Hallo health test wordt dynamisch toegevoegd of verwijderd van virtuele machines van Hallo load balancer wisselen op basis van hun antwoord toohealth controles.</span><span class="sxs-lookup"><span data-stu-id="43e20-142">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="43e20-143">Standaard wordt een virtuele machine verwijderd uit Hallo load balancer-distributie na twee opeenvolgende fouten met intervallen van 15 seconden.</span><span class="sxs-lookup"><span data-stu-id="43e20-143">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="43e20-144">U maakt een health test op basis van een protocol of de pagina voor de controle van een specifieke status voor uw app.</span><span class="sxs-lookup"><span data-stu-id="43e20-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="43e20-145">Hallo volgende voorbeeld wordt een TCP-test.</span><span class="sxs-lookup"><span data-stu-id="43e20-145">hello following example creates a TCP probe.</span></span> <span data-ttu-id="43e20-146">U kunt ook aangepaste HTTP-tests voor meer fijnmazige statuscontroles maken.</span><span class="sxs-lookup"><span data-stu-id="43e20-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="43e20-147">Wanneer u een aangepaste HTTP-test, moet u Hallo selectievakje statuspagina, zoals *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="43e20-147">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="43e20-148">Hallo test moet retourneren een **HTTP 200 OK** antwoord voor Hallo load balancer tookeep Hallo host in de draaihoek.</span><span class="sxs-lookup"><span data-stu-id="43e20-148">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="43e20-149">toocreate een TCP health test, die u gebruikt [toevoegen AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="43e20-149">toocreate a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="43e20-150">Hallo volgende voorbeeld wordt een health test met de naam *myHealthProbe* die elke VM bewaakt:</span><span class="sxs-lookup"><span data-stu-id="43e20-150">hello following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="43e20-151">Hallo load balancer is met bijwerken [Set AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="43e20-151">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="43e20-152">Een load balancer-regel maken</span><span class="sxs-lookup"><span data-stu-id="43e20-152">Create a load balancer rule</span></span>
<span data-ttu-id="43e20-153">Een load balancer-regel is gebruikte toodefine hoe verkeer wordt gedistribueerde toohello virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="43e20-153">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="43e20-154">U definieert Hallo front-end-IP-configuratie voor Hallo binnenkomende verkeer en Hallo backend-IP-adresgroep tooreceive Hallo, samen met de vereiste bron Hallo en doelpoort.</span><span class="sxs-lookup"><span data-stu-id="43e20-154">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="43e20-155">toomake zorgen dat alleen orde virtuele machines verkeer ontvangt, u Hallo health test toouse ook definiëren.</span><span class="sxs-lookup"><span data-stu-id="43e20-155">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="43e20-156">Maken van een regel voor load balancer met [toevoegen AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="43e20-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="43e20-157">Hallo volgende voorbeeld maakt u een regel voor load balancer met de naam *myLoadBalancerRule* en verkeer op poort sluitend *80*:</span><span class="sxs-lookup"><span data-stu-id="43e20-157">hello following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

<span data-ttu-id="43e20-158">Hallo load balancer is met bijwerken [Set AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="43e20-158">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="43e20-159">Virtueel netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="43e20-159">Configure virtual network</span></span>
<span data-ttu-id="43e20-160">Voordat u een aantal virtuele machines implementeren en uw balancer kunt testen, maak Hallo ondersteunende resources van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="43e20-160">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="43e20-161">Zie voor meer informatie over virtuele netwerken Hallo [Azure Virtual Networks beheren](tutorial-virtual-network.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="43e20-161">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="43e20-162">Maken van netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="43e20-162">Create network resources</span></span>
<span data-ttu-id="43e20-163">Maak een virtueel netwerk met [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="43e20-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="43e20-164">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* met *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="43e20-164">hello following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="43e20-165">Maken van een groep van de netwerkbeveiligingsregel met [nieuw AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), maakt u een netwerkbeveiligingsgroep met [nieuw AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="43e20-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="43e20-166">Toevoegen van Hallo beveiliging groep toohello netwerksubnet met [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) en werk vervolgens Hallo virtueel netwerk met [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="43e20-166">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="43e20-167">Hallo volgende voorbeeld wordt een groep netwerkbeveiligingsregel met de naam *myNetworkSecurityGroup* en past u deze te*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="43e20-167">hello following example creates a network security group rule named *myNetworkSecurityGroup* and applies it too*mySubnet*:</span></span>

```powershell
# Create security rule config
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

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="43e20-168">Virtuele NIC's zijn gemaakt met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="43e20-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="43e20-169">Hallo maakt volgende voorbeeld drie virtuele NIC's.</span><span class="sxs-lookup"><span data-stu-id="43e20-169">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="43e20-170">(Een virtuele NIC voor elke VM die u maakt voor uw app in hello te volgen stappen.)</span><span class="sxs-lookup"><span data-stu-id="43e20-170">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="43e20-171">U kunt extra virtuele NIC's en virtuele machines maken op elk gewenst moment en ze toohello load balancer toevoegen:</span><span class="sxs-lookup"><span data-stu-id="43e20-171">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a><span data-ttu-id="43e20-172">Virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="43e20-172">Create virtual machines</span></span>
<span data-ttu-id="43e20-173">tooimprove hello hoge beschikbaarheid van uw app, uw virtuele machines in een beschikbaarheidsset plaatst.</span><span class="sxs-lookup"><span data-stu-id="43e20-173">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="43e20-174">Maken van een beschikbaarheidsset met [nieuw AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="43e20-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="43e20-175">Hallo volgende voorbeeld maakt u een beschikbaarheidsset benoemde *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="43e20-175">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="43e20-176">Stel dat een beheerder gebruikersnaam en wachtwoord voor Hallo VM's met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="43e20-176">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="43e20-177">Nu kunt u virtuele machines Hallo met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="43e20-177">Now you can create hello VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="43e20-178">Hallo volgende voorbeeld maakt drie virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="43e20-178">hello following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

<span data-ttu-id="43e20-179">Het duurt enkele minuten toocreate en configureer alle drie virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="43e20-179">It takes a few minutes toocreate and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="43e20-180">IIS installeren met de extensie voor aangepaste scripts</span><span class="sxs-lookup"><span data-stu-id="43e20-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="43e20-181">In een vorige zelfstudie over [hoe toocustomize virtuele Windows-machine](tutorial-automate-vm-deployment.md), hebt u geleerd hoe tooautomate VM aanpassing met aangepaste Script uitbreiding voor Windows hello.</span><span class="sxs-lookup"><span data-stu-id="43e20-181">In a previous tutorial on [How toocustomize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with hello Custom Script Extension for Windows.</span></span> <span data-ttu-id="43e20-182">U kunt Hallo dezelfde tooinstall benadering en IIS configureren op uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="43e20-182">You can use hello same approach tooinstall and configure IIS on your VMs.</span></span>

<span data-ttu-id="43e20-183">Gebruik [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Hallo extensie voor aangepaste scripts.</span><span class="sxs-lookup"><span data-stu-id="43e20-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="43e20-184">Hallo-extensie wordt uitgevoerd `powershell Add-WindowsFeature Web-Server` tooinstall Hallo IIS-webserver en klik vervolgens op updates Hallo *Default.htm* pagina tooshow Hallo hostnaam Hallo VM:</span><span class="sxs-lookup"><span data-stu-id="43e20-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a><span data-ttu-id="43e20-185">Test load balancer</span><span class="sxs-lookup"><span data-stu-id="43e20-185">Test load balancer</span></span>
<span data-ttu-id="43e20-186">Hallo openbare IP-adres van de load balancer met verkrijgen [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="43e20-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="43e20-187">Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myPublicIP* eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="43e20-187">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="43e20-188">Vervolgens kunt u in de webbrowser tooa Hallo openbaar IP-adres invoeren.</span><span class="sxs-lookup"><span data-stu-id="43e20-188">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="43e20-189">Hallo-website wordt weergegeven, inclusief Hallo hostnaam Hallo VM die Hallo load balancer gedistribueerde tooas verkeer in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="43e20-189">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Actieve IIS-website](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="43e20-191">toosee hello load balancer verkeer verdelen over alle drie virtuele machines waarop uw app wordt uitgevoerd, u kunt force vernieuwen van uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="43e20-191">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="43e20-192">Toevoegen en verwijderen van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="43e20-192">Add and remove VMs</span></span>
<span data-ttu-id="43e20-193">Mogelijk moet u tooperform onderhoud op Hallo van virtuele machines waarop uw app, zoals het installeren van updates voor het besturingssysteem wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="43e20-193">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="43e20-194">toodeal met tooyour-app voor verkeer, moet u mogelijk tooadd extra virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="43e20-194">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="43e20-195">Deze sectie leest u hoe tooremove of een virtuele machine van Hallo load balancer toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="43e20-195">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="43e20-196">Een virtuele machine van Hallo load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="43e20-196">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="43e20-197">Hallo-netwerkinterfacekaart met ophalen [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), vervolgens set Hallo *loadbalancerbackendaddresspools gebruikt* eigenschap van Hallo virtuele NIC te*$null*.</span><span class="sxs-lookup"><span data-stu-id="43e20-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC too*$null*.</span></span> <span data-ttu-id="43e20-198">Tot slot werkt Hallo virtuele NIC:</span><span class="sxs-lookup"><span data-stu-id="43e20-198">Finally, update hello virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="43e20-199">toosee hello load balancer verkeer verdelen over Hallo overige twee virtuele machines met uw app u kunt force vernieuwen van uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="43e20-199">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="43e20-200">U kunt nu onderhoud uitvoeren op Hallo VM, zoals het installeren van updates voor het besturingssysteem of het uitvoeren van een VM opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="43e20-200">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="43e20-201">Een VM toohello load balancer toevoegen</span><span class="sxs-lookup"><span data-stu-id="43e20-201">Add a VM toohello load balancer</span></span>
<span data-ttu-id="43e20-202">Na onderhoud aan de virtuele machine uitvoeren of als u tooexpand capaciteit nodig hebt, stelt u Hallo *loadbalancerbackendaddresspools gebruikt* eigenschap van de virtuele NIC toohello hello *BackendAddressPool* van [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="43e20-202">After performing VM maintenance, or if you need tooexpand capacity, set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC toohello *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="43e20-203">Hallo load balancer ophalen:</span><span class="sxs-lookup"><span data-stu-id="43e20-203">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="43e20-204">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="43e20-204">Next steps</span></span>

<span data-ttu-id="43e20-205">In deze zelfstudie hebt gemaakt van een load balancer en virtuele machines tooit gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="43e20-205">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="43e20-206">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="43e20-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="43e20-207">Een Azure load balancer maken</span><span class="sxs-lookup"><span data-stu-id="43e20-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="43e20-208">Een load balancer health test maken</span><span class="sxs-lookup"><span data-stu-id="43e20-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="43e20-209">Regels voor netwerkverkeer voor de load balancer maken</span><span class="sxs-lookup"><span data-stu-id="43e20-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="43e20-210">Hallo aangepaste Scriptextensie toocreate een normale IIS-website gebruiken</span><span class="sxs-lookup"><span data-stu-id="43e20-210">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="43e20-211">Virtuele machines maken en koppelen tooa load balancer</span><span class="sxs-lookup"><span data-stu-id="43e20-211">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="43e20-212">Een load balancer in actie weergeven</span><span class="sxs-lookup"><span data-stu-id="43e20-212">View a load balancer in action</span></span>
> * <span data-ttu-id="43e20-213">Toevoegen of virtuele machines van een load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="43e20-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="43e20-214">Hoe gaan van de volgende zelfstudie toolearn toohello toomanage VM-netwerken.</span><span class="sxs-lookup"><span data-stu-id="43e20-214">Advance toohello next tutorial toolearn how toomanage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="43e20-215">Virtuele machines en virtuele netwerken beheren</span><span class="sxs-lookup"><span data-stu-id="43e20-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
