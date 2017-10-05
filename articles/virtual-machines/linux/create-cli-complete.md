---
title: Een Linux-omgeving maken met de Azure CLI 2.0 | Microsoft Docs
description: Maken van opslag, een Linux-VM, een virtueel netwerk en subnet, een load balancer, een NIC, een openbare IP-adres en een netwerkbeveiligingsgroep via een compleet nieuwe met behulp van de Azure CLI 2.0.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: e5c4785428b2150e951923e98079e00808a82d87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="1368e-103">Een volledige virtuele Linux-machine maken met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1368e-103">Create a complete Linux virtual machine with the Azure CLI</span></span>
<span data-ttu-id="1368e-104">U maakt snel een virtuele machine (VM) in Azure, kunt u één Azure CLI opdracht dat standaardwaarden gebruikt voor het maken van alle vereiste ondersteunende resources.</span><span class="sxs-lookup"><span data-stu-id="1368e-104">To quickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values to create any required supporting resources.</span></span> <span data-ttu-id="1368e-105">Resources, zoals een virtueel netwerk, openbare IP-adres en netwerkbeveiligingsgroepen worden automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1368e-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="1368e-106">Voor meer controle over uw omgeving in de productieomgeving gebruikt, u kunt deze resources tevoren maken en vervolgens uw VM's toe te voegen aan deze.</span><span class="sxs-lookup"><span data-stu-id="1368e-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs to them.</span></span> <span data-ttu-id="1368e-107">In dit artikel begeleidt u bij het maken van een virtuele machine en elk van de ondersteunende resources één voor één.</span><span class="sxs-lookup"><span data-stu-id="1368e-107">This article guides you through how to create a VM and each of the supporting resources one by one.</span></span>

<span data-ttu-id="1368e-108">Zorg ervoor dat de meest recente geïnstalleerd [Azure CLI 2.0](/cli/azure/install-az-cli2) en geregistreerd in een Azure-account met [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1368e-108">Make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged to an Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1368e-109">In de volgende voorbeelden kunt u de parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="1368e-109">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1368e-110">De namen van de voorbeeld-parameter *myResourceGroup*, *myVnet*, en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1368e-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="1368e-111">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="1368e-111">Create resource group</span></span>
<span data-ttu-id="1368e-112">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="1368e-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="1368e-113">Een resourcegroep moet worden gemaakt voordat een virtuele machine en de ondersteunende bronnen van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="1368e-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="1368e-114">Maken van de resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="1368e-114">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1368e-115">Het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* in de *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="1368e-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="1368e-116">Standaard is de uitvoer van de Azure CLI-opdrachten in JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="1368e-116">By default, the output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="1368e-117">Als u de uitvoer naar een lijst of tabel standaard, bijvoorbeeld gebruiken [az configureren--uitvoer](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="1368e-117">To change the default output to a list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="1368e-118">U kunt ook toevoegen `--output` elke opdracht voor een eenmalige wijzigen in de indeling van uitvoer.</span><span class="sxs-lookup"><span data-stu-id="1368e-118">You can also add `--output` to any command for a one time change in output format.</span></span> <span data-ttu-id="1368e-119">Het volgende voorbeeld ziet u de JSON-uitvoer van de `az group create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="1368e-119">The following example shows the JSON output from the `az group create` command:</span></span>

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="1368e-120">Een virtueel netwerk en subnet maken</span><span class="sxs-lookup"><span data-stu-id="1368e-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="1368e-121">Volgende die u een virtueel netwerk maken in Azure en een subnet in waarop u uw virtuele machines kunt maken.</span><span class="sxs-lookup"><span data-stu-id="1368e-121">Next you create a virtual network in Azure and a subnet in to which you can create your VMs.</span></span> <span data-ttu-id="1368e-122">Gebruik [az network vnet maken](/cli/azure/network/vnet#create) voor het maken van een virtueel netwerk met de naam *myVnet* met de *192.168.0.0/16* adresvoorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="1368e-122">Use [az network vnet create](/cli/azure/network/vnet#create) to create a virtual network named *myVnet* with the *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="1368e-123">U ook een subnet met de naam toevoegen *mySubnet* met het adresvoorvoegsel van *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="1368e-123">You also add a subnet named *mySubnet* with the address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="1368e-124">De uitvoer ziet u het subnet logisch gemaakt binnen het virtuele netwerk:</span><span class="sxs-lookup"><span data-stu-id="1368e-124">The output shows the subnet as logically created inside the virtual network:</span></span>

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a><span data-ttu-id="1368e-125">Een openbaar IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="1368e-125">Create a public IP address</span></span>
<span data-ttu-id="1368e-126">Nu gaan we maken een openbaar IP-adres met [az netwerk openbare ip-maken](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="1368e-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="1368e-127">Dit openbare IP-adres kunt u vanaf Internet verbinding maken met uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1368e-127">This public IP address enables you to connect to your VMs from the Internet.</span></span> <span data-ttu-id="1368e-128">Omdat het standaardadres dynamisch is, maken we ook een benoemde DNS-vermelding met de `--domain-name-label` optie.</span><span class="sxs-lookup"><span data-stu-id="1368e-128">Because the default address is dynamic, we also create a named DNS entry with the `--domain-name-label` option.</span></span> <span data-ttu-id="1368e-129">Het volgende voorbeeld wordt een openbaar IP-adres met de naam *myPublicIP* met de DNS-naam van *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="1368e-129">The following example creates a public IP named *myPublicIP* with the DNS name of *mypublicdns*.</span></span> <span data-ttu-id="1368e-130">Omdat de DNS-naam moet uniek zijn, Geef uw eigen unieke DNS-naam:</span><span class="sxs-lookup"><span data-stu-id="1368e-130">Because the DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="1368e-131">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="1368e-131">Output:</span></span>

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a><span data-ttu-id="1368e-132">Een netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="1368e-132">Create a network security group</span></span>
<span data-ttu-id="1368e-133">Maak een netwerkbeveiligingsgroep voor het beheren van de stroom van verkeer van en naar uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1368e-133">To control the flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="1368e-134">Een netwerkbeveiligingsgroep kan worden toegepast op een NIC of een subnet.</span><span class="sxs-lookup"><span data-stu-id="1368e-134">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="1368e-135">Het volgende voorbeeld wordt [az netwerk nsg maken](/cli/azure/network/nsg#create) een netwerkbeveiligingsgroep maken met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="1368e-135">The following example uses [az network nsg create](/cli/azure/network/nsg#create) to create a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="1368e-136">U definieert de regels die de specifieke verkeer toestaan of weigeren.</span><span class="sxs-lookup"><span data-stu-id="1368e-136">You define rules that allow or deny the specific traffic.</span></span> <span data-ttu-id="1368e-137">Binnenkomende verbindingen op poort 22 (voor ondersteuning van SSH) wilt toestaan, maakt u een inkomende regel voor de netwerkbeveiligingsgroep met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="1368e-137">To allow inbound connections on port 22 (to support SSH), create an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="1368e-138">Het volgende voorbeeld wordt een regel met naam *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="1368e-138">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

<span data-ttu-id="1368e-139">Als u wilt toestaan voor binnenkomende verbindingen op poort 80 (voor ondersteuning webverkeer), een ander netwerk groep beveiligingsregel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1368e-139">To allow inbound connections on port 80 (to support web traffic), add another network security group rule.</span></span> <span data-ttu-id="1368e-140">Het volgende voorbeeld wordt een regel met naam *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="1368e-140">The following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="1368e-141">Controleer de netwerkbeveiligingsgroep en de regels met [az netwerk nsg weergeven](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="1368e-141">Examine the network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="1368e-142">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="1368e-142">Output:</span></span>

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to Internet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a><span data-ttu-id="1368e-143">Maken van een virtuele NIC</span><span class="sxs-lookup"><span data-stu-id="1368e-143">Create a virtual NIC</span></span>
<span data-ttu-id="1368e-144">Virtuele netwerkinterfacekaarten (NIC's) zijn programmatisch beschikbaar omdat u regels toepassen op het gebruik ervan kunt.</span><span class="sxs-lookup"><span data-stu-id="1368e-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="1368e-145">U kunt ook meer dan één hebben.</span><span class="sxs-lookup"><span data-stu-id="1368e-145">You can also have more than one.</span></span> <span data-ttu-id="1368e-146">In de volgende [az netwerk nic maken](/cli/azure/network/nic#create) opdracht maken van een NIC met de naam *myNic* en deze koppelen aan de netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="1368e-146">In the following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with the network security group.</span></span> <span data-ttu-id="1368e-147">Het openbare IP-adres *myPublicIP* is ook gekoppeld aan de virtuele netwerkadapter.</span><span class="sxs-lookup"><span data-stu-id="1368e-147">The public IP address *myPublicIP* is also associated with the virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="1368e-148">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="1368e-148">Output:</span></span>

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a><span data-ttu-id="1368e-149">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="1368e-149">Create an availability set</span></span>
<span data-ttu-id="1368e-150">Beschikbaarheidssets help verspreiding uw virtuele machines in domeinen met fouten en domeinen van de update.</span><span class="sxs-lookup"><span data-stu-id="1368e-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="1368e-151">Hoewel u slechts één virtuele machine nu maken, is het beste beschikbaarheidssets gebruiken om het gemakkelijker om uit te breiden in de toekomst.</span><span class="sxs-lookup"><span data-stu-id="1368e-151">Even though you only create one VM right now, it's best practice to use availability sets to make it easier to expand in the future.</span></span> 

<span data-ttu-id="1368e-152">Domeinen met fouten definiëren een groepering van virtuele machines die een gemeenschappelijk power-bron- en switch delen.</span><span class="sxs-lookup"><span data-stu-id="1368e-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="1368e-153">Standaard worden de virtuele machines die worden geconfigureerd in de beschikbaarheidsset gescheiden over maximaal drie domeinen met fouten.</span><span class="sxs-lookup"><span data-stu-id="1368e-153">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="1368e-154">Een hardwareprobleem in een van deze domeinen met fouten heeft geen invloed op elke virtuele machine die uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1368e-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="1368e-155">Update domeinen duiden op groepen van virtuele machines en de onderliggende fysieke hardware die op hetzelfde moment kan worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="1368e-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="1368e-156">De volgorde in welke update domeinen worden opgestart mogelijk geen opeenvolgende tijdens gepland onderhoud, maar slechts één updatedomein tegelijk wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="1368e-156">During planned maintenance, the order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="1368e-157">Virtuele machines distribueert Azure automatisch in domeinen met fouten en update domeinen wanneer ze worden geplaatst in een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="1368e-157">Azure automatically distributes VMs across the fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="1368e-158">Zie voor meer informatie [het beheren van de beschikbaarheid van virtuele machines](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="1368e-158">For more information, see [managing the availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="1368e-159">Maken van een beschikbaarheidsset voor uw virtuele machine met [az vm beschikbaarheidsset maken](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="1368e-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="1368e-160">Het volgende voorbeeld wordt een benoemde beschikbaarheidsset *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="1368e-160">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="1368e-161">De uitvoer opmerkingen bij de domeinen met fouten en domeinen van de update:</span><span class="sxs-lookup"><span data-stu-id="1368e-161">The output notes fault domains and update domains:</span></span>

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-the-linux-vms"></a><span data-ttu-id="1368e-162">De virtuele Linux-machines maken</span><span class="sxs-lookup"><span data-stu-id="1368e-162">Create the Linux VMs</span></span>
<span data-ttu-id="1368e-163">U kunt de netwerkbronnen ter ondersteuning van Internet toegankelijke VM's hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1368e-163">You've created the network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="1368e-164">Nu een virtuele machine maken en beveilig deze met een SSH-sleutel.</span><span class="sxs-lookup"><span data-stu-id="1368e-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="1368e-165">In dit geval gaan we een Ubuntu VM op basis van de meest recente TNS maken.</span><span class="sxs-lookup"><span data-stu-id="1368e-165">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="1368e-166">U vindt aanvullende afbeeldingen met [az vm afbeeldingenlijst](/cli/azure/vm/image#list), zoals beschreven in [Azure VM-installatiekopieën vinden](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="1368e-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="1368e-167">We ook opgeven een SSH-sleutel moet worden gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="1368e-167">We also specify an SSH key to use for authentication.</span></span> <span data-ttu-id="1368e-168">Als u een openbare SSH-sleutelpaar niet hebt, kunt u [maken ze](mac-create-ssh-keys.md) of gebruik de `--generate-ssh-keys` -parameter voor deze voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1368e-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use the `--generate-ssh-keys` parameter to create them for you.</span></span> <span data-ttu-id="1368e-169">Als u al een sleutelpaar, als deze parameter gebruikt bestaande sleutels in `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="1368e-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="1368e-170">De virtuele machine maken door brengen onze bronnen en informatie samen met de [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1368e-170">Create the VM by bringing all our resources and information together with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="1368e-171">Het volgende voorbeeld wordt een virtuele machine met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="1368e-171">The following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="1368e-172">SSH met uw virtuele machine met de DNS-vermelding die u hebt opgegeven tijdens het maken van het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="1368e-172">SSH to your VM with the DNS entry you provided when you created the public IP address.</span></span> <span data-ttu-id="1368e-173">Dit `fqdn` in de uitvoer wordt weergegeven als u uw virtuele machine maken:</span><span class="sxs-lookup"><span data-stu-id="1368e-173">This `fqdn` is shown in the output as you create your VM:</span></span>

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="1368e-174">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="1368e-174">Output:</span></span>

```bash
The authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="1368e-175">U kunt installeren NGINX en het verkeer stroom aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1368e-175">You can install NGINX and see the traffic flow to the VM.</span></span> <span data-ttu-id="1368e-176">NGINX als volgt installeren:</span><span class="sxs-lookup"><span data-stu-id="1368e-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="1368e-177">Open uw webbrowser als u wilt de NGINX standaardsite in actie zien, en voert u de FQDN-naam:</span><span class="sxs-lookup"><span data-stu-id="1368e-177">To see the default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Standaard NGINX-site op de virtuele machine](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="1368e-179">Als een sjabloon exporteren</span><span class="sxs-lookup"><span data-stu-id="1368e-179">Export as a template</span></span>
<span data-ttu-id="1368e-180">Wat gebeurt er als u nu wilt maken van een extra development environment met dezelfde parameters of een productie-omgeving die overeenkomt met het?</span><span class="sxs-lookup"><span data-stu-id="1368e-180">What if you now want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="1368e-181">Resource Manager gebruikt de JSON-sjablonen op dat de parameters voor uw omgeving definiëren.</span><span class="sxs-lookup"><span data-stu-id="1368e-181">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="1368e-182">U maken uit de volledige omgeving door te verwijzen naar deze JSON-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="1368e-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="1368e-183">U kunt [handmatig JSON-sjablonen samenstellen](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of exporteren van een bestaande omgeving voor het maken van het JSON-sjabloon voor u.</span><span class="sxs-lookup"><span data-stu-id="1368e-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you.</span></span> <span data-ttu-id="1368e-184">Gebruik [exporteren az](/cli/azure/group#export) exporteren van uw resourcegroep als volgt:</span><span class="sxs-lookup"><span data-stu-id="1368e-184">Use [az group export](/cli/azure/group#export) to export your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="1368e-185">Deze opdracht maakt u de `myResourceGroup.json` bestand in de huidige werkmap.</span><span class="sxs-lookup"><span data-stu-id="1368e-185">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="1368e-186">Wanneer u een omgeving met deze sjabloon maakt, wordt u gevraagd de resourcenamen.</span><span class="sxs-lookup"><span data-stu-id="1368e-186">When you create an environment from this template, you are prompted for all the resource names.</span></span> <span data-ttu-id="1368e-187">U kunt deze namen in uw sjabloonbestand vullen door toe te voegen de `--include-parameter-default-value` -parameter voor de `az group export` opdracht.</span><span class="sxs-lookup"><span data-stu-id="1368e-187">You can populate these names in your template file by adding the `--include-parameter-default-value` parameter to the `az group export` command.</span></span> <span data-ttu-id="1368e-188">Bewerk uw JSON-sjabloon om op te geven van de resourcenamen van de of [maken van een bestand parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) die Hiermee worden de resourcenamen.</span><span class="sxs-lookup"><span data-stu-id="1368e-188">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="1368e-189">Gebruik voor het maken van een omgeving met de sjabloon [az implementatie maken](/cli/azure/group/deployment#create) als volgt:</span><span class="sxs-lookup"><span data-stu-id="1368e-189">To create an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="1368e-190">U wilt lezen [meer over het implementeren van sjablonen](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1368e-190">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1368e-191">Meer informatie over hoe u stapsgewijs omgevingen bijwerken, gebruikt u het parameterbestand en toegang tot sjablonen vanaf één locatie.</span><span class="sxs-lookup"><span data-stu-id="1368e-191">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1368e-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1368e-192">Next steps</span></span>
<span data-ttu-id="1368e-193">U nu kunt aan de slag met meerdere netwerkonderdelen en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1368e-193">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="1368e-194">Voor het bouwen van uw toepassing met behulp van de belangrijkste onderdelen die zijn geïntroduceerd hier kunt u deze Voorbeeldomgeving.</span><span class="sxs-lookup"><span data-stu-id="1368e-194">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
