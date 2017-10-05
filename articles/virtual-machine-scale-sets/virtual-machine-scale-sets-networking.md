---
title: Netwerken voor virtuele-machineschaalsets in Azure | Microsoft Docs
description: Eigenschappen van configuratienetwerken virtuele-machineschaalsets van Azure.
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: a8520c6d8962cc362fc935f6b515a299c0ce75b3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="0b11e-103">Netwerken voor virtuele-machineschaalsets in Azure</span><span class="sxs-lookup"><span data-stu-id="0b11e-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="0b11e-104">Wanneer u een virtuele-machineschaalset van Azure instelt via de portal, zijn bepaalde netwerkeigenschappen standaard ingesteld, bijvoorbeeld een Azure Load Balancer met binnenkomende NAT-regels.</span><span class="sxs-lookup"><span data-stu-id="0b11e-104">When you deploy an Azure virtual machine scale set through the portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="0b11e-105">In dit artikel wordt beschreven hoe u een aantal van de meer geavanceerde netwerkfuncties gebruikt die u kunt configureren met schaalsets.</span><span class="sxs-lookup"><span data-stu-id="0b11e-105">This article describes how to use some of the more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="0b11e-106">U kunt alle functies die in dit artikel configureren met behulp van Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="0b11e-106">You can configure all of the features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="0b11e-107">Er zijn ook Azure CLI- en PowerShell-voorbeelden toegevoegd voor bepaalde functies.</span><span class="sxs-lookup"><span data-stu-id="0b11e-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="0b11e-108">Gebruik CLI 2.10 en PowerShell 4.2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="0b11e-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="0b11e-109">Versneld netwerken</span><span class="sxs-lookup"><span data-stu-id="0b11e-109">Accelerated Networking</span></span>
<span data-ttu-id="0b11e-110">[Versnelde netwerken](../virtual-network/virtual-network-create-vm-accelerated-networking.md) in Azure verbetert de prestaties van het netwerk door het inschakelen van I/O-virtualisatie met één hoofdmap (SR-IOV) bij een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0b11e-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) to a virtual machine.</span></span> <span data-ttu-id="0b11e-111">Als u versneld netwerken wilt gebruiken met schaalsets, stelt u enableAcceleratedNetworking in op **true** in de instelling networkInterfaceConfigurations van uw schaalset.</span><span class="sxs-lookup"><span data-stu-id="0b11e-111">To use accelerated networking with scale sets, set enableAcceleratedNetworking to **true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="0b11e-112">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0b11e-112">For example:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="0b11e-113">Een schaalset maken die verwijst naar een bestaande Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="0b11e-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="0b11e-114">Wanneer een schaalset is gemaakt met Azure Portal, wordt er voor de meeste configuratieopties een nieuwe load balancer gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0b11e-114">When a scale set is created using the Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="0b11e-115">Als u een schaalset maakt die moet verwijzen naar een bestaande load balancer, kunt u dit doen met de CLI.</span><span class="sxs-lookup"><span data-stu-id="0b11e-115">If you create a scale set, which needs to reference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="0b11e-116">Het volgende voorbeeldscript maakt een load balancer en maakt vervolgens een schaalset die ernaar verwijst:</span><span class="sxs-lookup"><span data-stu-id="0b11e-116">The following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="0b11e-117">Configureerbare DNS-instellingen</span><span class="sxs-lookup"><span data-stu-id="0b11e-117">Configurable DNS Settings</span></span>
<span data-ttu-id="0b11e-118">Standaard nemen schaalsets de specifieke DNS-instellingen van het VNET en het subnet waarin ze zijn gemaakt over.</span><span class="sxs-lookup"><span data-stu-id="0b11e-118">By default, scale sets take on the specific DNS settings of the VNET and subnet they were created in.</span></span> <span data-ttu-id="0b11e-119">U kunt de DNS-instellingen voor een schaalset echter rechtstreeks configureren.</span><span class="sxs-lookup"><span data-stu-id="0b11e-119">You can however, configure the DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="0b11e-120">Een schaal met configureerbare DNS-servers maken</span><span class="sxs-lookup"><span data-stu-id="0b11e-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="0b11e-121">Als u een schaalset met een aangepaste DNS-configuratie met CLI 2.0 wilt maken, voegt u het argument **--dns-servers** toe aan de opdracht **vmss create** gevolgd door met spaties gescheiden IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="0b11e-121">To create a scale set with a custom DNS configuration using CLI 2.0, add the **--dns-servers** argument to the **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="0b11e-122">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0b11e-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="0b11e-123">Als u aangepaste DNS-servers wilt configureren in een Azure-sjabloon, voegt u de eigenschap dnsSettings toe aan het gedeelte networkInterfaceConfigurations van de schaalset.</span><span class="sxs-lookup"><span data-stu-id="0b11e-123">To configure custom DNS servers in an Azure template, add a dnsSettings property to the scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="0b11e-124">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0b11e-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="0b11e-125">Een schaalset maken met de configureerbare domeinnamen van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="0b11e-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="0b11e-126">Als u een schaalset wilt maken met een aangepaste DNS-naam voor virtuele machines met CLI 2.0, voegt u het argument **--vm-domain-name** toe aan de opdracht **vmss create**, gevolgd door een tekenreeks met de domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="0b11e-126">To create a scale set with a custom DNS name for virtual machines using CLI 2.0, add the **--vm-domain-name** argument to the **vmss create** command, followed by a string representing the domain name.</span></span>

<span data-ttu-id="0b11e-127">Als u de domeinnaam wilt instellen in een Azure-sjabloon, voegt u de eigenschap **dnsSettings** toe aan het gedeelte **networkInterfaceConfigurations** van de schaalset.</span><span class="sxs-lookup"><span data-stu-id="0b11e-127">To set the domain name in an Azure template, add a **dnsSettings** property to the scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="0b11e-128">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0b11e-128">For example:</span></span>

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

<span data-ttu-id="0b11e-129">De uitvoer voor de DNS-naam van een afzonderlijke virtuele machine heeft de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="0b11e-129">The output, for an individual virtual machine dns name would be in the following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="0b11e-130">Openbare IPv4 per virtuele machine</span><span class="sxs-lookup"><span data-stu-id="0b11e-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="0b11e-131">Virtuele machines in Azure-schaalsets hebben meestal geen eigen openbaar IP-adres nodig.</span><span class="sxs-lookup"><span data-stu-id="0b11e-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="0b11e-132">Het is in de meeste gevallen voordeliger en veiliger om een openbaar IP-adres aan een load balancer of een afzonderlijke virtuele machine (ook wel een jumpbox) te koppelen. Deze stuurt vervolgens binnenkomende verbindingen indien nodig door naar virtuele machines van de schaalset (bijvoorbeeld via de binnenkomende NAT-regels).</span><span class="sxs-lookup"><span data-stu-id="0b11e-132">For most scenarios, it is more economical and secure to associate a public IP address to a load balancer or to an individual virtual machine (aka a jumpbox), which then routes incoming connections to scale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="0b11e-133">In sommige gevallen hebben virtuele machines van een schaalset echter hun eigen openbare IP-adressen nodig.</span><span class="sxs-lookup"><span data-stu-id="0b11e-133">However, some scenarios do require scale set virtual machines to have their own public IP addresses.</span></span> <span data-ttu-id="0b11e-134">Dit is bijvoorbeeld het geval bij games, waarbij een console rechtstreeks verbinding moet maken met een virtuele cloudmachine, die de physics van de game verwerkt.</span><span class="sxs-lookup"><span data-stu-id="0b11e-134">An example is gaming, where a console needs to make a direct connection to a cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="0b11e-135">Een ander voorbeeld is de situatie waarbij virtuele machines externe verbindingen met elkaar moeten maken via regio's in een gedistribueerde database.</span><span class="sxs-lookup"><span data-stu-id="0b11e-135">Another example is where virtual machines need to make external connections to one another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="0b11e-136">Een schaalset met een openbaar IP-adres per virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="0b11e-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="0b11e-137">Als u een schaalset wilt maken waarmee een openbaar IP-adres wordt toegewezen aan elke virtuele machine met CLI 2.0, voegt u de parameter **--public-ip-per-vm** toe aan de opdracht **vmss create**.</span><span class="sxs-lookup"><span data-stu-id="0b11e-137">To create a scale set that assigns a public IP address to each virtual machine with CLI 2.0, add the **--public-ip-per-vm** parameter to the **vmss create** command.</span></span> 

<span data-ttu-id="0b11e-138">Als u een schaalset maakt met een Azure-sjabloon, zorg er dan voor dat de API-versie van de resource Microsoft.Compute/virtualMachineScaleSets ten minste **2017-03-30** is en voeg de JSON-eigenschap **publicIpAddressConfiguration** toe aan het gedeelte ipConfigurations van de schaalset.</span><span class="sxs-lookup"><span data-stu-id="0b11e-138">To create a scale set using an Azure template, make sure the API version of the Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property to the scale set ipConfigurations section.</span></span> <span data-ttu-id="0b11e-139">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0b11e-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="0b11e-140">Voorbeeldsjabloon: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="0b11e-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-the-public-ip-addresses-of-the-virtual-machines-in-a-scale-set"></a><span data-ttu-id="0b11e-141">Query’s uitvoeren op de openbare IP-adressen van de virtuele machines in een schaalset</span><span class="sxs-lookup"><span data-stu-id="0b11e-141">Querying the public IP addresses of the virtual machines in a scale set</span></span>
<span data-ttu-id="0b11e-142">U kunt de openbare IP-adressen die zijn toegewezen aan de virtuele machines van de schaalset met CLI 2.0 in een lijst weergeven met de opdracht **az vmss list-instance-public-ips**.</span><span class="sxs-lookup"><span data-stu-id="0b11e-142">To list the public IP addresses assigned to scale set virtual machines using CLI 2.0, use the **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="0b11e-143">Gebruik de opdracht _Get-AzureRmPublicIpAddress_ om openbare IP-adressen voor schaalsets weer te geven met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0b11e-143">To list scale set public IP addresses using PowerShell, use the _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="0b11e-144">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0b11e-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="0b11e-145">U kunt ook query’s uitvoeren op de openbare IP-adressen door rechtstreeks naar de resource-id van de openbare IP-adresconfiguratie te verwijzen.</span><span class="sxs-lookup"><span data-stu-id="0b11e-145">You can also query the public IP addresses by referencing the resource id of the public IP address configuration directly.</span></span> <span data-ttu-id="0b11e-146">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0b11e-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="0b11e-147">Query’s uitvoeren op de openbare IP-adressen die zijn toegewezen aan de virtuele machines in de schaalset met de [Azure Resource Explorer](https://resources.azure.com) of de REST API van Azure met versie **2017-03-30** of hoger.</span><span class="sxs-lookup"><span data-stu-id="0b11e-147">To query the public IP addresses assigned to scale set virtual machines using the [Azure Resource Explorer](https://resources.azure.com), or the Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="0b11e-148">Als u de openbare IP-adressen van een schaalset wilt bekijken met behulp van de Resource Explorer, bekijkt u het gedeelte **publicipaddresses** onder uw schaalset.</span><span class="sxs-lookup"><span data-stu-id="0b11e-148">To view public IP addresses for a scale set using the Resource Explorer, look at the **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="0b11e-149">Bijvoorbeeld: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="0b11e-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="0b11e-150">Voorbeelduitvoer:</span><span class="sxs-lookup"><span data-stu-id="0b11e-150">Example output:</span></span>
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="0b11e-151">Meerdere IP-adressen per NIC</span><span class="sxs-lookup"><span data-stu-id="0b11e-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="0b11e-152">Aan elke NIC die aan een virtuele machine in een schaalset is gekoppeld, zijn een of meer IP-configuraties gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="0b11e-152">Every NIC attached to a VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="0b11e-153">Aan elke configuratie is één privé-IP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="0b11e-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="0b11e-154">Aan elke configuratie kan ook één resource met een openbaar IP-adres zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="0b11e-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="0b11e-155">Om te begrijpen hoeveel IP adressen kunnen worden toegewezen aan een NIC en hoeveel openbare IP-adressen u kunt gebruiken in een Azure-abonnement, bekijkt u de [Azure-limieten](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="0b11e-155">To understand how many IP addresses can be assigned to a NIC, and how many public IP addresses you can use in an Azure subscription, refer to [Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="0b11e-156">Meerdere NIC's per virtuele machine</span><span class="sxs-lookup"><span data-stu-id="0b11e-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="0b11e-157">U kunt maximaal 8 NIC's per virtuele machine hebben, afhankelijk van de grootte van de machine.</span><span class="sxs-lookup"><span data-stu-id="0b11e-157">You can have up to 8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="0b11e-158">Het maximale aantal NIC's per computer is beschikbaar in het artikel [VM-grootte](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="0b11e-158">The maximum number of NICs per machine is available in the [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="0b11e-159">Het volgende voorbeeld is een netwerkprofiel van een schaalset met meerdere NIC-vermeldingen en meerdere openbare IP-adressen per virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="0b11e-159">The following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a><span data-ttu-id="0b11e-160">NSG per schaalset</span><span class="sxs-lookup"><span data-stu-id="0b11e-160">NSG per scale set</span></span>
<span data-ttu-id="0b11e-161">Netwerkbeveiligingsgroepen kunnen rechtstreeks op een schaalset worden toegepast door een verwijzing naar de sectie Configuratie van netwerkinterface van de eigenschappen van de virtuele machine van de schaalset toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="0b11e-161">Network Security Groups can be applied directly to a scale set, by adding a reference to the network interface configuration section of the scale set virtual machine properties.</span></span>

<span data-ttu-id="0b11e-162">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0b11e-162">For example:</span></span> 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="0b11e-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0b11e-163">Next steps</span></span>
<span data-ttu-id="0b11e-164">Raadpleeg [deze documentatie](../virtual-network/virtual-networks-overview.md) voor meer informatie over virtuele netwerken in Azure.</span><span class="sxs-lookup"><span data-stu-id="0b11e-164">For more information about Azure virtual networks, refer to [this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
