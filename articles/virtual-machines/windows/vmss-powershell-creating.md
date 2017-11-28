---
title: Maken van virtuele-machineschaalsets met PowerShell-cmdlets | Microsoft Docs
description: Aan de slag maken en beheren van uw eerste Azure virtuele-Machineschaalsets met Azure PowerShell-cmdlets
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: a3a36028a75d6cb7eb36277f3e2b5ab833c96a96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="894ab-103">Maken van virtuele-Machineschaalsets met PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="894ab-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="894ab-104">Dit artikel begeleidt bij een voorbeeld van het maken van een virtuele-machineschaalset (VMSS).</span><span class="sxs-lookup"><span data-stu-id="894ab-104">This article walks through an example of how to create a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="894ab-105">Een set scale drie knooppunten wordt gemaakt met de gekoppelde netwerken en opslag.</span><span class="sxs-lookup"><span data-stu-id="894ab-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="894ab-106">Eerste stappen</span><span class="sxs-lookup"><span data-stu-id="894ab-106">First Steps</span></span>
<span data-ttu-id="894ab-107">Zorg ervoor dat u hebt de nieuwste Azure PowerShell-module geïnstalleerd om te controleren of u hebt de PowerShell-commandlets die nodig zijn voor het onderhouden en schaalsets maken.</span><span class="sxs-lookup"><span data-stu-id="894ab-107">Ensure you have the latest Azure PowerShell module installed, to make sure you have the PowerShell commandlets needed to maintain, and create scale sets.</span></span>
<span data-ttu-id="894ab-108">Ga naar de opdrachtregel-hulpprogramma's [hier](http://aka.ms/webpi-azps) voor de meest recente beschikbare Azure Modules.</span><span class="sxs-lookup"><span data-stu-id="894ab-108">Go to the command line tools [here](http://aka.ms/webpi-azps) for the latest available Azure Modules.</span></span>

<span data-ttu-id="894ab-109">Gerelateerde VMSS vinden commandlets, gebruikt u de zoekreeks \*VMSS\*.</span><span class="sxs-lookup"><span data-stu-id="894ab-109">To find VMSS related commandlets, use the search string \*VMSS\*.</span></span> <span data-ttu-id="894ab-110">Bijvoorbeeld: _gcm *vmss*_</span><span class="sxs-lookup"><span data-stu-id="894ab-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="894ab-111">Maken van een VMSS</span><span class="sxs-lookup"><span data-stu-id="894ab-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="894ab-112">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="894ab-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="894ab-113">Maken van netwerken (VNET / Subnet)</span><span class="sxs-lookup"><span data-stu-id="894ab-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="894ab-114">Specificatie van het subnet</span><span class="sxs-lookup"><span data-stu-id="894ab-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="894ab-115">VNET-specificatie</span><span class="sxs-lookup"><span data-stu-id="894ab-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume the new subnet is the only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-to-allow-external-access"></a><span data-ttu-id="894ab-116">Openbare IP-Resource voor externe toegang maken</span><span class="sxs-lookup"><span data-stu-id="894ab-116">Create Public IP Resource to Allow External Access</span></span>
<span data-ttu-id="894ab-117">Dit wordt gebonden aan de Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="894ab-117">This will be bound to the Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="894ab-118">Load Balancer maken</span><span class="sxs-lookup"><span data-stu-id="894ab-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP to Load Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="894ab-119">Load Balancer configureren</span><span class="sxs-lookup"><span data-stu-id="894ab-119">Configure Load Balancer</span></span>
<span data-ttu-id="894ab-120">Maken van back-end adresgroep Config, dit wordt gedeeld door de NIC's van de virtuele machines in de schaalset.</span><span class="sxs-lookup"><span data-stu-id="894ab-120">Create Backend Address Pool Config, this will be shared by the NICs of the VMs in the scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="894ab-121">Stel Load Balanced Testpoort, wijzig de instellingen die geschikt is voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="894ab-121">Set Load Balanced Probe Port, change the settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="894ab-122">Maak een binnenkomende NAT-adresgroep voor directe routering verbinding (geen taakverdeling) met de virtuele machines in de schaal instelt via de Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="894ab-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) to the VMs in the scale set via the Load Balancer.</span></span> <span data-ttu-id="894ab-123">Dit is om aan te tonen met RDP en kan niet in uw toepassing nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="894ab-123">This is to demonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="894ab-124">De Load Balanced regel maken, in dit voorbeeld toont laden taakverdeling poort 80 aanvragen, met behulp van de instellingen van de vorige stappen.</span><span class="sxs-lookup"><span data-stu-id="894ab-124">Create the Load Balanced Rule, this example shows load balancing port 80 requests, using the settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="894ab-125">Load Balancer maken met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="894ab-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="894ab-126">Controleer de instellingen van de Load Balancer, controleert u taakverdeling poort configs, opmerking, ziet u inkomende NAT-regels totdat de virtuele machines in de schaalset zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="894ab-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until the VMs in the scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-the-scale-set"></a><span data-ttu-id="894ab-127">Configureer en maak de schaalset</span><span class="sxs-lookup"><span data-stu-id="894ab-127">Configure and Create the scale set</span></span>
<span data-ttu-id="894ab-128">Houd er rekening mee deze infrastructuur voorbeeld ziet u hoe om in te stellen, distribueren en scale-webverkeer in de schaalset, maar de installatiekopieën van virtuele machines die u hier opgeeft hoeft niet elke webservice geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="894ab-128">Note, this infrastructure example shows how to set up distribute and scale web traffic across the scale set, but the VMs Images specified here do not have any web services installed.</span></span>

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

<span data-ttu-id="894ab-129">NIC verbinden met Load Balancer en het Subnet</span><span class="sxs-lookup"><span data-stu-id="894ab-129">Bind NIC to Load Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="894ab-130">Maken van scale set Config</span><span class="sxs-lookup"><span data-stu-id="894ab-130">Create scale set Config</span></span>

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

<span data-ttu-id="894ab-131">Configuratie van scale set bouwen</span><span class="sxs-lookup"><span data-stu-id="894ab-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="894ab-132">U hebt nu de schaalset gemaakt.</span><span class="sxs-lookup"><span data-stu-id="894ab-132">Now you have created the scale set.</span></span> <span data-ttu-id="894ab-133">U kunt testen om verbinding te maken met de afzonderlijke virtuele machine met RDP in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="894ab-133">You can test connecting to the individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
