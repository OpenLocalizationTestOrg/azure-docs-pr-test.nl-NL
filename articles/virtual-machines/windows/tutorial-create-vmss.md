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
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a>Een virtuele-Machineschaalset maken en implementeren van een maximaal beschikbare app in Windows
Een virtuele-machineschaalset kunt u toodeploy en beheren van een reeks identiek zijn, automatisch schalen virtuele machines. U kunt Hallo aantal virtuele machines in de schaalset Hallo handmatig schalen of regels tooautoscale op basis van CPU-gebruik, geheugen-aanvraag of netwerkverkeer definiëren. In deze zelfstudie maakt implementeren u een virtuele-machineschaalset instellen in Azure. Procedures voor:

> [!div class="checklist"]
> * Hallo aangepaste Scriptextensie toodefine een site IIS tooscale gebruiken
> * Een load balancer voor uw scale set maken
> * Maken van een virtuele-machineschaalset
> * Vergroten of verkleinen Hallo aantal exemplaren in een schaalset
> * Maken van regels voor automatisch schalen

Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger. Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).


## <a name="scale-set-overview"></a>Overzicht van Scale Set
Schaalsets vergelijkbare concepten gebruiken als u in de vorige zelfstudie hello te kennisgemaakt[maximaal beschikbare virtuele machines maken](tutorial-availability-sets.md). Virtuele machines in een schaalset worden gedistribueerd voor probleem- en update domeinen net als bij virtuele machines in een beschikbaarheidsset.

Virtuele machines worden gemaakt als nodig in een schaalset. U automatisch schalen regels toocontrol definiëren hoe en wanneer virtuele machines worden toegevoegd of verwijderd uit het Hallo-schaalset. Deze regels kunnen activeren op basis van metrische gegevens zoals CPU-belasting, geheugengebruik of netwerkverkeer.

Schaal wordt ingesteld voor ondersteuning van too1, 000 VM's wanneer u een installatiekopie van een Azure-platform. Voor werkbelastingen met aanzienlijke installatie of VM aanpassingsvereisten, kunt u desgewenst te[maken van een aangepaste VM-installatiekopie](tutorial-custom-images.md). U kunt maken van too100 virtuele machines in een schaal instelt met behulp van een aangepaste installatiekopie.


## <a name="create-an-app-tooscale"></a>Maken van een app-tooscale
Voordat u een schaalset maken kunt, maakt u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupAutomate* in Hallo *EastUS* locatie:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

In een eerdere zelfstudie hebt u geleerd hoe te[automatiseren VM-configuratie](tutorial-automate-vm-deployment.md) met behulp van aangepaste Scriptextensie Hallo. Maken van een scale set-configuratie en vervolgens een aangepaste Scriptextensie tooinstall toepassen en IIS te configureren:

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

## <a name="create-scale-load-balancer"></a>Schaal load balancer maken
Een Azure load balancer is een Layer-4 (TCP, UDP) load balancer die zorgt voor hoge beschikbaarheid door het distribueren van inkomend verkeer tussen orde virtuele machines. Een load balancer health test een bepaalde poort op elke virtuele machine bewaakt en distribueert u alleen verkeer tooan operationele VM. Zie voor meer informatie de volgende zelfstudie Hallo op [hoe tooload balans vinden tussen virtuele machines van Windows](tutorial-load-balancer.md).

Maak een load balancer die een openbaar IP-adres en webverkeer op poort 80 distribueert:

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

## <a name="create-a-scale-set"></a>Maken van een schaalset
Maak nu de schaal van een virtuele machine in te stellen [nieuw AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm). Hallo volgende voorbeeld wordt een set met de naam scale *myScaleSet*:

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

Het duurt enkele minuten toocreate en configureer alle Hallo scale set resources en virtuele machines.


## <a name="test-your-app"></a>Uw app testen
toosee uw IIS-website in actie verkrijgen Hallo openbare IP-adres van de load balancer met [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myPublicIP* gemaakt als onderdeel van het Hallo-schaalset:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

Voer Hallo openbaar IP-adres in de webbrowser tooa. Hallo-app wordt weergegeven, inclusief Hallo hostnaam Hallo VM die Hallo load balancer gedistribueerde verkeer naar:

![Actieve IIS-website](./media/tutorial-create-vmss/running-iis-site.png)

toosee hello schaal instellen in actie, u kunt force vernieuwen uw web browser toosee Hallo load balancer verkeer verdelen over alle Hallo virtuele machines waarop uw app wordt uitgevoerd.


## <a name="management-tasks"></a>Beheertaken
Gedurende de levenscyclus van de Hallo van Hallo scale is ingesteld, moet u mogelijk toorun een of meer beheertaken. U kunt bovendien toocreate scripts die verschillende lifecycle-taken automatiseren. Azure PowerShell biedt een snelle manier toodo deze taken. Hier volgen enkele algemene taken.

### <a name="view-vms-in-a-scale-set"></a>Weergave virtuele machines in een schaalset
tooview een lijst met virtuele machines die worden uitgevoerd in uw scale ingesteld, gebruikt u [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) als volgt:

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


### <a name="increase-or-decrease-vm-instances"></a>Vergroten of verkleinen van VM-exemplaren
toosee hello aantal exemplaren van u momenteel hebt in een schaal ingesteld, gebruikt u [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) en query's uitvoeren op *sku.capacity*:

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

U kunt vervolgens handmatig vergroten of verkleinen Hallo aantal virtuele machines in Hallo schaal in te stellen [Update AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss). Hallo volgende voorbeeld wordt Hallo aantal virtuele machines in te stellen schaal*5*:

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

Als duurt een paar minuten tooupdate Hallo opgegeven aantal exemplaren in de schaalset.


### <a name="configure-autoscale-rules"></a>Regels voor automatisch schalen configureren
In plaats van handmatig schalen Hallo aantal exemplaren in uw scale is ingesteld, kunt u regels voor automatisch schalen definiëren. Deze regels controleren Hallo-exemplaren in uw scale ingesteld en reageren dienovereenkomstig op basis van metrische gegevens en drempels die u definieert. Hallo voorbeeld te volgen uitgeschaald Hallo aantal exemplaren van door een wanneer het gemiddelde CPU-belasting Hallo is groter dan 60% gedurende een periode van 5 minuten. Als Hallo gemiddelde CPU-belasting vervolgens onder 30% gedurende een periode van 5 minuten, worden Hallo instanties geschaald door één exemplaar:

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


## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie maakt u een virtuele-machineschaalset gemaakt. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Hallo aangepaste Scriptextensie toodefine een site IIS tooscale gebruiken
> * Een load balancer voor uw scale set maken
> * Maken van een virtuele-machineschaalset
> * Vergroten of verkleinen Hallo aantal exemplaren in een schaalset
> * Maken van regels voor automatisch schalen

De volgende zelfstudie toolearn toohello voor vooraf informatie over taakverdeling concepten voor virtuele machines.

> [!div class="nextstepaction"]
> [Load balance virtuele machines](tutorial-load-balancer.md)
