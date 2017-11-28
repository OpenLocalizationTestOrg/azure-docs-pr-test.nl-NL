---
title: een Azure internetgerichte aaaCreate load balancer met IPv6 - PowerShell | Microsoft Docs
description: Meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler met IPv6 met behulp van PowerShell voor Resource Manager
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: IPv6-, azure load balancer, dual-stack, openbare IP-adres, systeemeigen ipv6, mobiele, iot
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="08795-104">Maken van een Internetgericht load balancer met IPv6 met behulp van PowerShell voor Resource Manager aan de slag</span><span class="sxs-lookup"><span data-stu-id="08795-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="08795-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08795-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="08795-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="08795-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="08795-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="08795-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="08795-108">Azure Load Balancer is een Layer-4 (TCP, UDP) load balancer.</span><span class="sxs-lookup"><span data-stu-id="08795-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="08795-109">Hallo load balancer biedt hoge beschikbaarheid door het distribueren van inkomend verkeer tussen orde service-exemplaren in cloudservices of virtuele machines in een load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="08795-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="08795-110">Azure Load Balancer kan deze services ook toepassen op meerdere poorten, meerdere IP-adressen of allebei.</span><span class="sxs-lookup"><span data-stu-id="08795-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="08795-111">Voorbeeldscenario voor implementatie</span><span class="sxs-lookup"><span data-stu-id="08795-111">Example deployment scenario</span></span>

<span data-ttu-id="08795-112">Hallo illustreert volgende diagram Hallo load balancing-oplossing wordt geïmplementeerd in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="08795-112">hello following diagram illustrates hello load balancing solution being deployed in this article.</span></span>

![Load balancer-scenario](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="08795-114">In dit scenario maakt u hello Azure-resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="08795-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="08795-115">een internetgerichte Load Balancer met een IPv4 en IPv6-openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="08795-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="08795-116">twee laden taakverdeling regels toomap Hallo openbare VIP's toohello persoonlijke eindpunten</span><span class="sxs-lookup"><span data-stu-id="08795-116">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>
* <span data-ttu-id="08795-117">een Beschikbaarheidsset toothat bevat Hallo twee virtuele machines</span><span class="sxs-lookup"><span data-stu-id="08795-117">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="08795-118">twee virtuele machines (VM's)</span><span class="sxs-lookup"><span data-stu-id="08795-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="08795-119">de virtuele netwerkinterface voor elke virtuele machine met zowel IPv4 als IPv6-adressen die zijn toegewezen</span><span class="sxs-lookup"><span data-stu-id="08795-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a><span data-ttu-id="08795-120">Hallo-oplossing met behulp van Azure PowerShell Hallo implementeren</span><span class="sxs-lookup"><span data-stu-id="08795-120">Deploying hello solution using hello Azure PowerShell</span></span>

<span data-ttu-id="08795-121">Hallo stappen laten zien hoe toocreate een internetverbinding netwerktaakverdeler met Azure Resource Manager met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08795-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="08795-122">Met Azure Resource Manager elke bron wordt gemaakt en afzonderlijk geconfigureerd, klikt u vervolgens samenstellen toocreate een resource.</span><span class="sxs-lookup"><span data-stu-id="08795-122">With Azure Resource Manager, each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="08795-123">een load balancer toodeploy, u maken en configureren van Hallo objecten te volgen:</span><span class="sxs-lookup"><span data-stu-id="08795-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="08795-124">Front-end-IP-configuratie: bevat openbare IP-adressen voor inkomend netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="08795-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="08795-125">Back-end-adresgroep - bevat netwerkinterfaces (NIC's) voor virtuele machines tooreceive-netwerkverkeer Hallo van Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="08795-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="08795-126">Taakverdeling regels - bevat regels voor toewijzing van een openbare poort op Hallo load balancer tooport in Hallo back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="08795-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="08795-127">Binnenkomende NAT-regels: regels voor toewijzing van een openbare poort op Hallo load balancer tooa poort voor een specifieke virtuele machine in het back-end-adresgroep Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="08795-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="08795-128">Tests - beschikbaarheid van health-tests gebruikt toocheck van exemplaren van virtuele machines in het back-end-adresgroep Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="08795-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="08795-129">Zie [Azure Resource Manager-ondersteuning voor load balancer](load-balancer-arm.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="08795-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="08795-130">PowerShell toouse Resource Manager instellen</span><span class="sxs-lookup"><span data-stu-id="08795-130">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="08795-131">Zorg ervoor dat u hebt Hallo nieuwste productieversie van hello Azure Resource Manager-module voor PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08795-131">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="08795-132">Meld u aan bij Azure</span><span class="sxs-lookup"><span data-stu-id="08795-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="08795-133">Voer uw referenties in wanneer dit wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="08795-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="08795-134">Controleer de abonnementen Hallo voor Hallo-account</span><span class="sxs-lookup"><span data-stu-id="08795-134">Check hello subscriptions for hello account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="08795-135">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="08795-135">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="08795-136">Maak een resourcegroep (kunt deze stap als u een bestaande resourcegroep overslaan)</span><span class="sxs-lookup"><span data-stu-id="08795-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="08795-137">Een virtueel netwerk en een openbare IP-adres voor Hallo front-end-IP-adresgroep maken</span><span class="sxs-lookup"><span data-stu-id="08795-137">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="08795-138">Maak een virtueel netwerk met een subnet.</span><span class="sxs-lookup"><span data-stu-id="08795-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="08795-139">Azure openbaar IP-adres (PIP) resources maken voor Hallo front-end-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="08795-139">Create Azure Public IP address (PIP) resources for hello front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="08795-140">Hallo load balancer gebruikmaakt Hallo domeinlabel van Hallo openbare IP-adres als voorvoegsel voor de FQDN-naam.</span><span class="sxs-lookup"><span data-stu-id="08795-140">hello load balancer uses hello domain label of hello public IP as prefix for its FQDN.</span></span> <span data-ttu-id="08795-141">In dit voorbeeld Hallo FQDN-namen zijn *lbnrpipv4.westus.cloudapp.azure.com* en *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="08795-141">In this example, hello FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="08795-142">Een Front-End-IP-configuraties en een Back-End-adresgroep maken</span><span class="sxs-lookup"><span data-stu-id="08795-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="08795-143">Maak adres voor front-end-configuratie die gebruikmaakt van Hallo openbare IP-adressen die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08795-143">Create front-end address configuration that uses hello Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="08795-144">Maak back-end-adresgroepen.</span><span class="sxs-lookup"><span data-stu-id="08795-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="08795-145">LB regels, NAT-regels, een test- en een load balancer maken</span><span class="sxs-lookup"><span data-stu-id="08795-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="08795-146">In dit voorbeeld maakt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="08795-146">This example creates hello following items:</span></span>

* <span data-ttu-id="08795-147">een NAT-regel tootranslate alle binnenkomend verkeer op poort 443 tooport 4443</span><span class="sxs-lookup"><span data-stu-id="08795-147">a NAT rule tootranslate all incoming traffic on port 443 tooport 4443</span></span>
* <span data-ttu-id="08795-148">een load balancer-regel toobalance alle binnenkomend verkeer op poort 80 tooport 80 op Hallo adressen in Hallo back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="08795-148">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="08795-149">een load balancer regel tooallow RDP verbinding toohello VM's op poort 3389.</span><span class="sxs-lookup"><span data-stu-id="08795-149">a load balancer rule tooallow RDP connection toohello VMs on port 3389.</span></span>
* <span data-ttu-id="08795-150">een test regel toocheck Hallo gezondheidsstatus op een pagina met de naam *HealthProbe.aspx* of een service via poort 8080</span><span class="sxs-lookup"><span data-stu-id="08795-150">a probe rule toocheck hello health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="08795-151">een load balancer die gebruikmaakt van alle deze objecten</span><span class="sxs-lookup"><span data-stu-id="08795-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="08795-152">Hallo NAT-regels maken.</span><span class="sxs-lookup"><span data-stu-id="08795-152">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="08795-153">Maak een statustest.</span><span class="sxs-lookup"><span data-stu-id="08795-153">Create a health probe.</span></span> <span data-ttu-id="08795-154">Er zijn twee manieren tooconfigure een test:</span><span class="sxs-lookup"><span data-stu-id="08795-154">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="08795-155">HTTP-test</span><span class="sxs-lookup"><span data-stu-id="08795-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="08795-156">of de TCP-controle</span><span class="sxs-lookup"><span data-stu-id="08795-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="08795-157">In dit voorbeeld gaan we toouse Hallo die TCP-tests.</span><span class="sxs-lookup"><span data-stu-id="08795-157">For this example, we are going toouse hello TCP probes.</span></span>

3. <span data-ttu-id="08795-158">Maak een load balancer-regel.</span><span class="sxs-lookup"><span data-stu-id="08795-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="08795-159">Hallo load balancer met behulp van Hallo eerder gemaakte objecten maken.</span><span class="sxs-lookup"><span data-stu-id="08795-159">Create hello load balancer using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a><span data-ttu-id="08795-160">NIC's voor Hallo back-end virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="08795-160">Create NICs for hello back-end VMs</span></span>

1. <span data-ttu-id="08795-161">Hallo virtueel netwerk ophalen en virtueel netwerksubnet waar Hallo NIC's moeten toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08795-161">Get hello Virtual Network and Virtual Network Subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="08795-162">IP-configuraties en NIC's voor virtuele machines Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="08795-162">Create IP configurations and NICs for hello VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a><span data-ttu-id="08795-163">Virtuele machines maken en toewijzen van Hallo NIC's van een nieuw gemaakt</span><span class="sxs-lookup"><span data-stu-id="08795-163">Create virtual machines and assign hello newly created NICs</span></span>

<span data-ttu-id="08795-164">Zie voor meer informatie over het maken van een virtuele machine [maken en vooraf configureren van een virtuele Windows-computer met Resource Manager en Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="08795-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="08795-165">Een Beschikbaarheidsset en Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="08795-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="08795-166">Elke virtuele machine maken en toewijzen van Hallo vorige gemaakt NIC 's</span><span class="sxs-lookup"><span data-stu-id="08795-166">Create each VM and assign hello previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a><span data-ttu-id="08795-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08795-167">Next steps</span></span>

[<span data-ttu-id="08795-168">Aan de slag met het configureren van een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="08795-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="08795-169">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="08795-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="08795-170">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="08795-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
