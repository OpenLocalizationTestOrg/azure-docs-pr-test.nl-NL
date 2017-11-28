---
title: aaaNetworking voor virtuele Azure-machine-schaalsets | Microsoft Docs
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
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="a0671-103">Netwerken voor virtuele-machineschaalsets in Azure</span><span class="sxs-lookup"><span data-stu-id="a0671-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="a0671-104">Wanneer u de schaal van een virtuele machine van Azure instelt via de portal Hallo implementeert, zijn bepaalde netwerkeigenschappen standaardinstellingen, bijvoorbeeld een Azure Load Balancer met binnenkomende NAT-regels.</span><span class="sxs-lookup"><span data-stu-id="a0671-104">When you deploy an Azure virtual machine scale set through hello portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="a0671-105">Dit artikel wordt beschreven hoe toouse aantal Hallo geavanceerdere netwerkfuncties die u met de schaal configureren kunt wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a0671-105">This article describes how toouse some of hello more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="a0671-106">U kunt alle Hallo-functies die in dit artikel met behulp van Azure Resource Manager-sjablonen kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="a0671-106">You can configure all of hello features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="a0671-107">Er zijn ook Azure CLI- en PowerShell-voorbeelden toegevoegd voor bepaalde functies.</span><span class="sxs-lookup"><span data-stu-id="a0671-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="a0671-108">Gebruik CLI 2.10 en PowerShell 4.2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a0671-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="a0671-109">Versneld netwerken</span><span class="sxs-lookup"><span data-stu-id="a0671-109">Accelerated Networking</span></span>
<span data-ttu-id="a0671-110">Azure [versnelde netwerken](../virtual-network/virtual-network-create-vm-accelerated-networking.md) verbetert de prestaties van het netwerk met één hoofdmap i/o-virtualisatie (SR-IOV) tooa virtuele machine inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a0671-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) tooa virtual machine.</span></span> <span data-ttu-id="a0671-111">toouse versnelde netwerken met schaalsets, stelt u enableAcceleratedNetworking te**true** in de schaalset networkInterfaceConfigurations instellingen.</span><span class="sxs-lookup"><span data-stu-id="a0671-111">toouse accelerated networking with scale sets, set enableAcceleratedNetworking too**true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="a0671-112">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a0671-112">For example:</span></span>
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

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="a0671-113">Een schaalset maken die verwijst naar een bestaande Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="a0671-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="a0671-114">Wanneer een schaalset is gemaakt met behulp van hello Azure-portal, wordt een nieuwe load balancer gemaakt voor de meeste configuratieopties.</span><span class="sxs-lookup"><span data-stu-id="a0671-114">When a scale set is created using hello Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="a0671-115">Als u een schaalset die tooreference moet een bestaande load balancer maakt, kunt u dit doen met CLI.</span><span class="sxs-lookup"><span data-stu-id="a0671-115">If you create a scale set, which needs tooreference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="a0671-116">Hallo volgende voorbeeldscript wordt gemaakt van een load balancer en maakt vervolgens een schaalset die verwijst naar het:</span><span class="sxs-lookup"><span data-stu-id="a0671-116">hello following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="a0671-117">Configureerbare DNS-instellingen</span><span class="sxs-lookup"><span data-stu-id="a0671-117">Configurable DNS Settings</span></span>
<span data-ttu-id="a0671-118">Standaard nemen-schaalsets op Hallo specifieke DNS-instellingen van Hallo VNET en het subnet die ze zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a0671-118">By default, scale sets take on hello specific DNS settings of hello VNET and subnet they were created in.</span></span> <span data-ttu-id="a0671-119">U kunt wel Hallo DNS-instellingen configureren voor een schaal rechtstreeks worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a0671-119">You can however, configure hello DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="a0671-120">Een schaal met configureerbare DNS-servers maken</span><span class="sxs-lookup"><span data-stu-id="a0671-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="a0671-121">een schaal ingesteld met een aangepaste DNS-configuratie met CLI 2.0, toocreate toevoegen Hallo **--dns-servers** argument toohello **vmss maken** opdracht, gevolgd door een spatie gescheiden IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="a0671-121">toocreate a scale set with a custom DNS configuration using CLI 2.0, add hello **--dns-servers** argument toohello **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="a0671-122">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a0671-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="a0671-123">tooconfigure aangepaste DNS-servers in een Azure-sjabloon toevoegen aan een dnsSettings eigenschap toohello schaalset networkInterfaceConfigurations-sectie.</span><span class="sxs-lookup"><span data-stu-id="a0671-123">tooconfigure custom DNS servers in an Azure template, add a dnsSettings property toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="a0671-124">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a0671-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="a0671-125">Een schaalset maken met de configureerbare domeinnamen van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="a0671-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="a0671-126">een schaalset met een aangepaste DNS-naam voor virtuele machines met CLI 2.0, toocreate toevoegen Hallo **--vm domeinnaam** argument toohello **vmss maken** opdracht, gevolgd door een tekenreeks voor Hallo domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="a0671-126">toocreate a scale set with a custom DNS name for virtual machines using CLI 2.0, add hello **--vm-domain-name** argument toohello **vmss create** command, followed by a string representing hello domain name.</span></span>

<span data-ttu-id="a0671-127">tooset Hallo-domeinnaam in een Azure-sjabloon toevoegen een **dnsSettings** eigenschap toohello schaalset **networkInterfaceConfigurations** sectie.</span><span class="sxs-lookup"><span data-stu-id="a0671-127">tooset hello domain name in an Azure template, add a **dnsSettings** property toohello scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="a0671-128">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a0671-128">For example:</span></span>

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

<span data-ttu-id="a0671-129">Hallo-uitvoer voor de DNS-naam van een afzonderlijke virtuele machine in de volgende formulier Hallo zou worden:</span><span class="sxs-lookup"><span data-stu-id="a0671-129">hello output, for an individual virtual machine dns name would be in hello following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="a0671-130">Openbare IPv4 per virtuele machine</span><span class="sxs-lookup"><span data-stu-id="a0671-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="a0671-131">Virtuele machines in Azure-schaalsets hebben meestal geen eigen openbaar IP-adres nodig.</span><span class="sxs-lookup"><span data-stu-id="a0671-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="a0671-132">Voor de meeste scenario is beter voordelige en veilige tooassociate een openbare IP-adres tooa load balancer of tooan afzonderlijke virtuele machine (ook wel een jumpbox) die vervolgens binnenkomende verbindingen tooscale set virtuele machines stuurt die u nodig (bijvoorbeeld: binnenkomende NAT-regels).</span><span class="sxs-lookup"><span data-stu-id="a0671-132">For most scenarios, it is more economical and secure tooassociate a public IP address tooa load balancer or tooan individual virtual machine (aka a jumpbox), which then routes incoming connections tooscale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="a0671-133">Echter een aantal scenario's hoeven virtuele machines toohave-schaalset hun eigen openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="a0671-133">However, some scenarios do require scale set virtual machines toohave their own public IP addresses.</span></span> <span data-ttu-id="a0671-134">Een voorbeeld games, waarin een console moet toomake een rechtstreekse verbinding tooa cloud virtuele machine, die game fysische verwerking doet.</span><span class="sxs-lookup"><span data-stu-id="a0671-134">An example is gaming, where a console needs toomake a direct connection tooa cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="a0671-135">Een ander voorbeeld is waarbij virtuele machines toomake externe verbindingen tooone moet een andere tussen regio's in een gedistribueerde database.</span><span class="sxs-lookup"><span data-stu-id="a0671-135">Another example is where virtual machines need toomake external connections tooone another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="a0671-136">Een schaalset met een openbaar IP-adres per virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="a0671-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="a0671-137">een schaalset waarmee een openbare IP-adres tooeach virtuele machine met CLI 2.0, toegewezen toocreate toevoegen Hallo **--openbare ip per vm** parameter toohello **vmss maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="a0671-137">toocreate a scale set that assigns a public IP address tooeach virtual machine with CLI 2.0, add hello **--public-ip-per-vm** parameter toohello **vmss create** command.</span></span> 

<span data-ttu-id="a0671-138">toocreate een schaal ingesteld met een Azure-sjabloon, zorg ervoor dat Hallo API-versie van Hallo Microsoft.Compute/virtualMachineScaleSets resource is ten minste **2017-03-30**, en voeg een **publicIpAddressConfiguration**JSON eigenschap toohello schaalset ipConfigurations-sectie.</span><span class="sxs-lookup"><span data-stu-id="a0671-138">toocreate a scale set using an Azure template, make sure hello API version of hello Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="a0671-139">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a0671-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="a0671-140">Voorbeeldsjabloon: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="a0671-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a><span data-ttu-id="a0671-141">Hallo openbare IP-adres opvragen adressen van Hallo virtuele machines in een schaal instellen</span><span class="sxs-lookup"><span data-stu-id="a0671-141">Querying hello public IP addresses of hello virtual machines in a scale set</span></span>
<span data-ttu-id="a0671-142">toolist hello openbare IP-adressen toegewezen tooscale set virtuele machines met CLI 2.0, gebruikt u Hallo **az vmss lijst-exemplaar-openbare-IP-adressen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="a0671-142">toolist hello public IP addresses assigned tooscale set virtual machines using CLI 2.0, use hello **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="a0671-143">toolist schaalset openbare IP-adressen met behulp van PowerShell, gebruikt u Hallo _Get-AzureRmPublicIpAddress_ opdracht.</span><span class="sxs-lookup"><span data-stu-id="a0671-143">toolist scale set public IP addresses using PowerShell, use hello _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="a0671-144">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a0671-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="a0671-145">U kunt ook query Hallo openbare IP-adressen door te verwijzen rechtstreeks naar de bron-id Hallo van Hallo openbare IP-adresconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="a0671-145">You can also query hello public IP addresses by referencing hello resource id of hello public IP address configuration directly.</span></span> <span data-ttu-id="a0671-146">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a0671-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="a0671-147">tooquery hello openbare IP-adressen toegewezen tooscale set virtuele machines met behulp van Hallo [Azure Resource Explorer](https://resources.azure.com), of REST API van Azure met versie Hallo **2017-03-30** of hoger.</span><span class="sxs-lookup"><span data-stu-id="a0671-147">tooquery hello public IP addresses assigned tooscale set virtual machines using hello [Azure Resource Explorer](https://resources.azure.com), or hello Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="a0671-148">tooview openbare IP-adressen voor een scale-Hallo Resource Explorer, met een set bekijkt hello **publicipaddresses** sectie onder uw schaalset.</span><span class="sxs-lookup"><span data-stu-id="a0671-148">tooview public IP addresses for a scale set using hello Resource Explorer, look at hello **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="a0671-149">Bijvoorbeeld: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="a0671-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="a0671-150">Voorbeelduitvoer:</span><span class="sxs-lookup"><span data-stu-id="a0671-150">Example output:</span></span>
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

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="a0671-151">Meerdere IP-adressen per NIC</span><span class="sxs-lookup"><span data-stu-id="a0671-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="a0671-152">Elke NIC gekoppeld tooa die virtuele machine in een scale-set kan een of meer IP-configuraties die zijn gekoppeld aan deze hebben.</span><span class="sxs-lookup"><span data-stu-id="a0671-152">Every NIC attached tooa VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="a0671-153">Aan elke configuratie is één privé-IP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a0671-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="a0671-154">Aan elke configuratie kan ook één resource met een openbaar IP-adres zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a0671-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="a0671-155">hoeveel IP-adressen kunnen toounderstand tooa NIC, worden toegewezen en hoeveel openbare IP-adressen kunt u in een Azure-abonnement te verwijzen[Azure limieten](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="a0671-155">toounderstand how many IP addresses can be assigned tooa NIC, and how many public IP addresses you can use in an Azure subscription, refer too[Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="a0671-156">Meerdere NIC's per virtuele machine</span><span class="sxs-lookup"><span data-stu-id="a0671-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="a0671-157">U kunt hebben up too8 NIC's per virtuele machine, afhankelijk van de grootte van de machine.</span><span class="sxs-lookup"><span data-stu-id="a0671-157">You can have up too8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="a0671-158">Hallo maximum aantal NIC's per machine is beschikbaar in Hallo [VM-grootte artikel](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="a0671-158">hello maximum number of NICs per machine is available in hello [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="a0671-159">Hallo volgende voorbeeld is dat een schaalset netwerkprofiel met meerdere NIC-vermeldingen en meerdere openbare IP-adressen per virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="a0671-159">hello following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
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

## <a name="nsg-per-scale-set"></a><span data-ttu-id="a0671-160">NSG per schaalset</span><span class="sxs-lookup"><span data-stu-id="a0671-160">NSG per scale set</span></span>
<span data-ttu-id="a0671-161">Netwerkbeveiligingsgroepen kunnen direct tooa scale set, ingesteld door een verwijzing toohello network interface-configuratiesectie van Hallo schaal toe te voegen eigenschappen van virtuele machine worden aangebracht.</span><span class="sxs-lookup"><span data-stu-id="a0671-161">Network Security Groups can be applied directly tooa scale set, by adding a reference toohello network interface configuration section of hello scale set virtual machine properties.</span></span>

<span data-ttu-id="a0671-162">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a0671-162">For example:</span></span> 
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

## <a name="next-steps"></a><span data-ttu-id="a0671-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0671-163">Next steps</span></span>
<span data-ttu-id="a0671-164">Voor meer informatie over virtuele netwerken van Azure te verwijzen[deze documentatie](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0671-164">For more information about Azure virtual networks, refer too[this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
