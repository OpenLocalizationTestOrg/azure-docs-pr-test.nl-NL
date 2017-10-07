---
title: een virtuele Machine Scale Sets voor Windows in Azure aaaCreate | Microsoft Docs
description: Maken en implementeren van een maximaal beschikbare toepassing op Windows-VM's met behulp van een virtuele-machineschaalset
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="9370d-103">Een virtuele-Machineschaalset maken en implementeren van een maximaal beschikbare app in Windows</span><span class="sxs-lookup"><span data-stu-id="9370d-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="9370d-104">Een virtuele-machineschaalset kunt u toodeploy en beheren van een reeks identiek zijn, automatisch schalen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="9370d-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="9370d-105">U kunt Hallo aantal virtuele machines in de schaalset Hallo handmatig schalen of regels tooautoscale op basis van CPU-gebruik, geheugen-aanvraag of netwerkverkeer definiëren.</span><span class="sxs-lookup"><span data-stu-id="9370d-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="9370d-106">In deze zelfstudie maakt implementeren u een virtuele-machineschaalset instellen in Azure.</span><span class="sxs-lookup"><span data-stu-id="9370d-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="9370d-107">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="9370d-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9370d-108">Hallo aangepaste Scriptextensie toodefine een site IIS tooscale gebruiken</span><span class="sxs-lookup"><span data-stu-id="9370d-108">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="9370d-109">Een load balancer voor uw scale set maken</span><span class="sxs-lookup"><span data-stu-id="9370d-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="9370d-110">Maken van een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="9370d-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="9370d-111">Vergroten of verkleinen Hallo aantal exemplaren in een schaalset</span><span class="sxs-lookup"><span data-stu-id="9370d-111">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="9370d-112">Maken van regels voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="9370d-112">Create autoscale rules</span></span>

<span data-ttu-id="9370d-113">Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="9370d-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="9370d-114">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="9370d-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="9370d-115">Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="9370d-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="9370d-116">Overzicht van Scale Set</span><span class="sxs-lookup"><span data-stu-id="9370d-116">Scale Set overview</span></span>
<span data-ttu-id="9370d-117">Schaalsets vergelijkbare concepten gebruiken als u in de vorige zelfstudie hello te kennisgemaakt[maximaal beschikbare virtuele machines maken](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="9370d-117">Scale sets use similar concepts as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="9370d-118">Virtuele machines in een schaalset worden gedistribueerd voor probleem- en update domeinen net als bij virtuele machines in een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="9370d-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="9370d-119">Virtuele machines worden gemaakt als nodig in een schaalset.</span><span class="sxs-lookup"><span data-stu-id="9370d-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="9370d-120">U automatisch schalen regels toocontrol definiëren hoe en wanneer virtuele machines worden toegevoegd of verwijderd uit het Hallo-schaalset.</span><span class="sxs-lookup"><span data-stu-id="9370d-120">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="9370d-121">Deze regels kunnen activeren op basis van metrische gegevens zoals CPU-belasting, geheugengebruik of netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="9370d-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="9370d-122">Schaal wordt ingesteld voor ondersteuning van too1, 000 VM's wanneer u een installatiekopie van een Azure-platform.</span><span class="sxs-lookup"><span data-stu-id="9370d-122">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="9370d-123">Voor werkbelastingen met aanzienlijke installatie of VM aanpassingsvereisten, kunt u desgewenst te[maken van een aangepaste VM-installatiekopie](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="9370d-123">For workloads with significant installation or VM customization requirements, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="9370d-124">U kunt maken van too100 virtuele machines in een schaal instelt met behulp van een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="9370d-124">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="9370d-125">Maken van een app-tooscale</span><span class="sxs-lookup"><span data-stu-id="9370d-125">Create an app tooscale</span></span>
<span data-ttu-id="9370d-126">Voordat u een schaalset maken kunt, maakt u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="9370d-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="9370d-127">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupAutomate* in Hallo *EastUS* locatie:</span><span class="sxs-lookup"><span data-stu-id="9370d-127">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="9370d-128">In een eerdere zelfstudie hebt u geleerd hoe te[automatiseren VM-configuratie](tutorial-automate-vm-deployment.md) met behulp van aangepaste Scriptextensie Hallo.</span><span class="sxs-lookup"><span data-stu-id="9370d-128">In an earlier tutorial, you learned how too[Automate VM configuration](tutorial-automate-vm-deployment.md) using hello Custom Script Extension.</span></span> <span data-ttu-id="9370d-129">Maken van een scale set-configuratie en vervolgens een aangepaste Scriptextensie tooinstall toepassen en IIS te configureren:</span><span class="sxs-lookup"><span data-stu-id="9370d-129">Create a scale set configuration then apply a Custom Script Extension tooinstall and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="9370d-130">Schaal load balancer maken</span><span class="sxs-lookup"><span data-stu-id="9370d-130">Create scale load balancer</span></span>
<span data-ttu-id="9370d-131">Een Azure load balancer is een Layer-4 (TCP, UDP) load balancer die zorgt voor hoge beschikbaarheid door het distribueren van inkomend verkeer tussen orde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="9370d-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="9370d-132">Een load balancer health test een bepaalde poort op elke virtuele machine bewaakt en distribueert u alleen verkeer tooan operationele VM.</span><span class="sxs-lookup"><span data-stu-id="9370d-132">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span> <span data-ttu-id="9370d-133">Zie voor meer informatie de volgende zelfstudie Hallo op [hoe tooload balans vinden tussen virtuele machines van Windows](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="9370d-133">For more information, see hello next tutorial on [How tooload balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="9370d-134">Maak een load balancer die een openbaar IP-adres en webverkeer op poort 80 distribueert:</span><span class="sxs-lookup"><span data-stu-id="9370d-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="9370d-135">Maken van een schaalset</span><span class="sxs-lookup"><span data-stu-id="9370d-135">Create a scale set</span></span>
<span data-ttu-id="9370d-136">Maak nu de schaal van een virtuele machine in te stellen [nieuw AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="9370d-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="9370d-137">Hallo volgende voorbeeld wordt een set met de naam scale *myScaleSet*:</span><span class="sxs-lookup"><span data-stu-id="9370d-137">hello following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="9370d-138">Het duurt enkele minuten toocreate en configureer alle Hallo scale set resources en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="9370d-138">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="9370d-139">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="9370d-139">Test your app</span></span>
<span data-ttu-id="9370d-140">toosee uw IIS-website in actie verkrijgen Hallo openbare IP-adres van de load balancer met [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="9370d-140">toosee your IIS website in action, obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="9370d-141">Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myPublicIP* gemaakt als onderdeel van het Hallo-schaalset:</span><span class="sxs-lookup"><span data-stu-id="9370d-141">hello following example obtains hello IP address for *myPublicIP* created as part of hello scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="9370d-142">Voer Hallo openbaar IP-adres in de webbrowser tooa.</span><span class="sxs-lookup"><span data-stu-id="9370d-142">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="9370d-143">Hallo-app wordt weergegeven, inclusief Hallo hostnaam Hallo VM die Hallo load balancer gedistribueerde verkeer naar:</span><span class="sxs-lookup"><span data-stu-id="9370d-143">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Actieve IIS-website](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="9370d-145">toosee hello schaal instellen in actie, u kunt force vernieuwen uw web browser toosee Hallo load balancer verkeer verdelen over alle Hallo virtuele machines waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9370d-145">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="9370d-146">Beheertaken</span><span class="sxs-lookup"><span data-stu-id="9370d-146">Management tasks</span></span>
<span data-ttu-id="9370d-147">Gedurende de levenscyclus van de Hallo van Hallo scale is ingesteld, moet u mogelijk toorun een of meer beheertaken.</span><span class="sxs-lookup"><span data-stu-id="9370d-147">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="9370d-148">U kunt bovendien toocreate scripts die verschillende lifecycle-taken automatiseren.</span><span class="sxs-lookup"><span data-stu-id="9370d-148">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="9370d-149">Azure PowerShell biedt een snelle manier toodo deze taken.</span><span class="sxs-lookup"><span data-stu-id="9370d-149">Azure PowerShell provides a quick way toodo those tasks.</span></span> <span data-ttu-id="9370d-150">Hier volgen enkele algemene taken.</span><span class="sxs-lookup"><span data-stu-id="9370d-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="9370d-151">Weergave virtuele machines in een schaalset</span><span class="sxs-lookup"><span data-stu-id="9370d-151">View VMs in a scale set</span></span>
<span data-ttu-id="9370d-152">tooview een lijst met virtuele machines die worden uitgevoerd in uw scale ingesteld, gebruikt u [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) als volgt:</span><span class="sxs-lookup"><span data-stu-id="9370d-152">tooview a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="9370d-153">Vergroten of verkleinen van VM-exemplaren</span><span class="sxs-lookup"><span data-stu-id="9370d-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="9370d-154">toosee hello aantal exemplaren van u momenteel hebt in een schaal ingesteld, gebruikt u [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) en query's uitvoeren op *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="9370d-154">toosee hello number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="9370d-155">U kunt vervolgens handmatig vergroten of verkleinen Hallo aantal virtuele machines in Hallo schaal in te stellen [Update AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="9370d-155">You can then manually increase or decrease hello number of virtual machines in hello scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="9370d-156">Hallo volgende voorbeeld wordt Hallo aantal virtuele machines in te stellen schaal*5*:</span><span class="sxs-lookup"><span data-stu-id="9370d-156">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="9370d-157">Als duurt een paar minuten tooupdate Hallo opgegeven aantal exemplaren in de schaalset.</span><span class="sxs-lookup"><span data-stu-id="9370d-157">If takes a few minutes tooupdate hello specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="9370d-158">Regels voor automatisch schalen configureren</span><span class="sxs-lookup"><span data-stu-id="9370d-158">Configure autoscale rules</span></span>
<span data-ttu-id="9370d-159">In plaats van handmatig schalen Hallo aantal exemplaren in uw scale is ingesteld, kunt u regels voor automatisch schalen definiëren.</span><span class="sxs-lookup"><span data-stu-id="9370d-159">Rather than manually scaling hello number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="9370d-160">Deze regels controleren Hallo-exemplaren in uw scale ingesteld en reageren dienovereenkomstig op basis van metrische gegevens en drempels die u definieert.</span><span class="sxs-lookup"><span data-stu-id="9370d-160">These rules monitor hello instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="9370d-161">Hallo voorbeeld te volgen uitgeschaald Hallo aantal exemplaren van door een wanneer het gemiddelde CPU-belasting Hallo is groter dan 60% gedurende een periode van 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="9370d-161">hello following example scales out hello number of instances by one when hello average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="9370d-162">Als Hallo gemiddelde CPU-belasting vervolgens onder 30% gedurende een periode van 5 minuten, worden Hallo instanties geschaald door één exemplaar:</span><span class="sxs-lookup"><span data-stu-id="9370d-162">If hello average CPU load then drops below 30% over a 5 minute period, hello instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="9370d-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9370d-163">Next steps</span></span>
<span data-ttu-id="9370d-164">In deze zelfstudie maakt u een virtuele-machineschaalset gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9370d-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="9370d-165">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="9370d-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9370d-166">Hallo aangepaste Scriptextensie toodefine een site IIS tooscale gebruiken</span><span class="sxs-lookup"><span data-stu-id="9370d-166">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="9370d-167">Een load balancer voor uw scale set maken</span><span class="sxs-lookup"><span data-stu-id="9370d-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="9370d-168">Maken van een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="9370d-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="9370d-169">Vergroten of verkleinen Hallo aantal exemplaren in een schaalset</span><span class="sxs-lookup"><span data-stu-id="9370d-169">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="9370d-170">Maken van regels voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="9370d-170">Create autoscale rules</span></span>

<span data-ttu-id="9370d-171">De volgende zelfstudie toolearn toohello voor vooraf informatie over taakverdeling concepten voor virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="9370d-171">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9370d-172">Load balance virtuele machines</span><span class="sxs-lookup"><span data-stu-id="9370d-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
