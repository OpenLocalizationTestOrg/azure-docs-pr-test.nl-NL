---
title: Virtuele-machineschaalset aaaCreating wilt instellen met PowerShell-cmdlets | Microsoft Docs
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
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="6cc48-103">Maken van virtuele-Machineschaalsets met PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="6cc48-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="6cc48-104">Dit artikel begeleidt bij een voorbeeld van hoe toocreate een virtuele-machineschaalset (VMSS).</span><span class="sxs-lookup"><span data-stu-id="6cc48-104">This article walks through an example of how toocreate a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="6cc48-105">Een set scale drie knooppunten wordt gemaakt met de gekoppelde netwerken en opslag.</span><span class="sxs-lookup"><span data-stu-id="6cc48-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="6cc48-106">Eerste stappen</span><span class="sxs-lookup"><span data-stu-id="6cc48-106">First Steps</span></span>
<span data-ttu-id="6cc48-107">Zorg ervoor dat u Hallo nieuwste Azure PowerShell-module geïnstalleerd hebt, hebt u Hallo PowerShell commandlets toomake toomaintain nodig en schaalsets maken.</span><span class="sxs-lookup"><span data-stu-id="6cc48-107">Ensure you have hello latest Azure PowerShell module installed, toomake sure you have hello PowerShell commandlets needed toomaintain, and create scale sets.</span></span>
<span data-ttu-id="6cc48-108">Ga toohello opdrachtregelprogramma's [hier](http://aka.ms/webpi-azps) Hallo voor de meest recente beschikbare Azure-Modules.</span><span class="sxs-lookup"><span data-stu-id="6cc48-108">Go toohello command line tools [here](http://aka.ms/webpi-azps) for hello latest available Azure Modules.</span></span>

<span data-ttu-id="6cc48-109">toofind VMSS gerelateerde commandlets, gebruiken de zoekreeks Hallo \*VMSS\*.</span><span class="sxs-lookup"><span data-stu-id="6cc48-109">toofind VMSS related commandlets, use hello search string \*VMSS\*.</span></span> <span data-ttu-id="6cc48-110">Bijvoorbeeld: _gcm *vmss*_</span><span class="sxs-lookup"><span data-stu-id="6cc48-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="6cc48-111">Maken van een VMSS</span><span class="sxs-lookup"><span data-stu-id="6cc48-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="6cc48-112">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="6cc48-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="6cc48-113">Maken van netwerken (VNET / Subnet)</span><span class="sxs-lookup"><span data-stu-id="6cc48-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="6cc48-114">Specificatie van het subnet</span><span class="sxs-lookup"><span data-stu-id="6cc48-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="6cc48-115">VNET-specificatie</span><span class="sxs-lookup"><span data-stu-id="6cc48-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a><span data-ttu-id="6cc48-116">Openbare IP-Resource tooAllow externe toegang maken</span><span class="sxs-lookup"><span data-stu-id="6cc48-116">Create Public IP Resource tooAllow External Access</span></span>
<span data-ttu-id="6cc48-117">Dit is gebonden toohello Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="6cc48-117">This will be bound toohello Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="6cc48-118">Load Balancer maken</span><span class="sxs-lookup"><span data-stu-id="6cc48-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="6cc48-119">Load Balancer configureren</span><span class="sxs-lookup"><span data-stu-id="6cc48-119">Configure Load Balancer</span></span>
<span data-ttu-id="6cc48-120">Maken van back-end adresgroep Config, dit worden gedeeld door Hallo NIC's van Hallo virtuele machines in de schaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="6cc48-120">Create Backend Address Pool Config, this will be shared by hello NICs of hello VMs in hello scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="6cc48-121">Stel Load Balanced Testpoort, Hallo instellingen geschikt is voor uw toepassing wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6cc48-121">Set Load Balanced Probe Port, change hello settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="6cc48-122">Maken van een binnenkomende NAT-adresgroep voor directe routering verbinding (geen taakverdeling) toohello virtuele machines in Hallo scale ingesteld via Hallo Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="6cc48-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) toohello VMs in hello scale set via hello Load Balancer.</span></span> <span data-ttu-id="6cc48-123">Dit is toodemonstrate met RDP en kan niet in uw toepassing nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="6cc48-123">This is toodemonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="6cc48-124">Hallo met gelijke taakverdeling regel laden in het volgende voorbeeld toont load balancing poort 80 aanvragen, met de Hallo-instellingen van de vorige stappen maken.</span><span class="sxs-lookup"><span data-stu-id="6cc48-124">Create hello Load Balanced Rule, this example shows load balancing port 80 requests, using hello settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="6cc48-125">Load Balancer maken met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="6cc48-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="6cc48-126">Controleer de instellingen van de Load Balancer, controleert u load balanced poort configs, houd er rekening mee, ziet u inkomende NAT-regels tot Hallo virtuele machines in de schaalset Hallo worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6cc48-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until hello VMs in hello scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a><span data-ttu-id="6cc48-127">Configureren en maken Hallo schaalset</span><span class="sxs-lookup"><span data-stu-id="6cc48-127">Configure and Create hello scale set</span></span>
<span data-ttu-id="6cc48-128">Houd er rekening mee deze infrastructuur-voorbeeld laat zien hoe tooset up distribueren en scale-webverkeer over Hallo scale set echter Hallo installatiekopieën van virtuele machines die u hier opgeeft hoeft niet elke webservice geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6cc48-128">Note, this infrastructure example shows how tooset up distribute and scale web traffic across hello scale set, but hello VMs Images specified here do not have any web services installed.</span></span>

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

<span data-ttu-id="6cc48-129">BIND NIC tooLoad Balancer en het Subnet</span><span class="sxs-lookup"><span data-stu-id="6cc48-129">Bind NIC tooLoad Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="6cc48-130">Maken van scale set Config</span><span class="sxs-lookup"><span data-stu-id="6cc48-130">Create scale set Config</span></span>

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

<span data-ttu-id="6cc48-131">Configuratie van scale set bouwen</span><span class="sxs-lookup"><span data-stu-id="6cc48-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="6cc48-132">U hebt nu Hallo schaalset gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6cc48-132">Now you have created hello scale set.</span></span> <span data-ttu-id="6cc48-133">U kunt testen verbindende toohello afzonderlijke virtuele machine met RDP in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6cc48-133">You can test connecting toohello individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
