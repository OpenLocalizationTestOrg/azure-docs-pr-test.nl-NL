---
title: een Linux-omgeving Hello Azure CLI 2.0 aaaCreate | Microsoft Docs
description: Opslag, een Linux-VM, een virtueel netwerk en subnet, een load balancer, een NIC, een openbare IP-adres en een netwerkbeveiligingsgroep maken via Hallo gemalen met behulp van hello Azure CLI 2.0.
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
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="83d33-103">Een volledige virtuele Linux-machine maken met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="83d33-103">Create a complete Linux virtual machine with hello Azure CLI</span></span>
<span data-ttu-id="83d33-104">tooquickly maken van een virtuele machine (VM) in Azure, kunt u één opdracht Azure CLI die gebruikmaakt van standaard waarden toocreate welke verplicht ondersteunende resources gebruiken.</span><span class="sxs-lookup"><span data-stu-id="83d33-104">tooquickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values toocreate any required supporting resources.</span></span> <span data-ttu-id="83d33-105">Resources, zoals een virtueel netwerk, openbare IP-adres en netwerkbeveiligingsgroepen worden automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="83d33-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="83d33-106">Voor meer controle over uw omgeving in de productieomgeving gebruikt, u kunt deze resources tevoren maken en voeg vervolgens uw toothem virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="83d33-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs toothem.</span></span> <span data-ttu-id="83d33-107">In dit artikel begeleidt u bij hoe toocreate een virtuele machine en alle ondersteunende resources één voor één Hallo.</span><span class="sxs-lookup"><span data-stu-id="83d33-107">This article guides you through how toocreate a VM and each of hello supporting resources one by one.</span></span>

<span data-ttu-id="83d33-108">Zorg ervoor dat u Hallo laatste hebt geïnstalleerd [Azure CLI 2.0](/cli/azure/install-az-cli2) en geregistreerde tooan Azure-account met [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="83d33-108">Make sure that you have installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged tooan Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="83d33-109">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="83d33-109">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="83d33-110">De namen van de voorbeeld-parameter *myResourceGroup*, *myVnet*, en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="83d33-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="83d33-111">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="83d33-111">Create resource group</span></span>
<span data-ttu-id="83d33-112">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="83d33-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="83d33-113">Een resourcegroep moet worden gemaakt voordat een virtuele machine en de ondersteunende bronnen van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="83d33-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="83d33-114">Maak Hallo resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="83d33-114">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="83d33-115">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="83d33-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="83d33-116">Hallo-uitvoer van de Azure CLI-opdrachten is standaard in JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="83d33-116">By default, hello output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="83d33-117">toochange hello uitvoer tooa standaardlijst of tabel, bijvoorbeeld gebruiken [az configureren--uitvoer](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="83d33-117">toochange hello default output tooa list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="83d33-118">U kunt ook toevoegen `--output` tooany opdracht voor een eenmalige wijzigen in de indeling van uitvoer.</span><span class="sxs-lookup"><span data-stu-id="83d33-118">You can also add `--output` tooany command for a one time change in output format.</span></span> <span data-ttu-id="83d33-119">Hallo volgende voorbeeld ziet u JSON-uitvoer van Hallo Hallo `az group create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="83d33-119">hello following example shows hello JSON output from hello `az group create` command:</span></span>

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

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="83d33-120">Een virtueel netwerk en subnet maken</span><span class="sxs-lookup"><span data-stu-id="83d33-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="83d33-121">Vervolgens maken van een virtueel netwerk in Azure en een subnet in toowhich kunt u uw virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="83d33-121">Next you create a virtual network in Azure and a subnet in toowhich you can create your VMs.</span></span> <span data-ttu-id="83d33-122">Gebruik [az network vnet maken](/cli/azure/network/vnet#create) toocreate een virtueel netwerk met de naam *myVnet* Hello *192.168.0.0/16* adresvoorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="83d33-122">Use [az network vnet create](/cli/azure/network/vnet#create) toocreate a virtual network named *myVnet* with hello *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="83d33-123">U ook een subnet met de naam toevoegen *mySubnet* met het Hallo-adresvoorvoegsel van *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="83d33-123">You also add a subnet named *mySubnet* with hello address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="83d33-124">Hallo uitvoer toont logisch gemaakt in het virtuele netwerk Hallo Hallo-subnet:</span><span class="sxs-lookup"><span data-stu-id="83d33-124">hello output shows hello subnet as logically created inside hello virtual network:</span></span>

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


## <a name="create-a-public-ip-address"></a><span data-ttu-id="83d33-125">Een openbaar IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="83d33-125">Create a public IP address</span></span>
<span data-ttu-id="83d33-126">Nu gaan we maken een openbaar IP-adres met [az netwerk openbare ip-maken](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="83d33-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="83d33-127">Dit openbare IP-adres, kunt u tooconnect tooyour VM's van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="83d33-127">This public IP address enables you tooconnect tooyour VMs from hello Internet.</span></span> <span data-ttu-id="83d33-128">Omdat Hallo standaardadres dynamisch is, we ook een benoemde DNS-vermelding maken met de Hallo `--domain-name-label` optie.</span><span class="sxs-lookup"><span data-stu-id="83d33-128">Because hello default address is dynamic, we also create a named DNS entry with hello `--domain-name-label` option.</span></span> <span data-ttu-id="83d33-129">Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam *myPublicIP* met Hallo DNS-naam van *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="83d33-129">hello following example creates a public IP named *myPublicIP* with hello DNS name of *mypublicdns*.</span></span> <span data-ttu-id="83d33-130">Aangezien Hallo DNS-naam uniek zijn moet, Geef uw eigen unieke DNS-naam:</span><span class="sxs-lookup"><span data-stu-id="83d33-130">Because hello DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="83d33-131">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="83d33-131">Output:</span></span>

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


## <a name="create-a-network-security-group"></a><span data-ttu-id="83d33-132">Een netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="83d33-132">Create a network security group</span></span>
<span data-ttu-id="83d33-133">toocontrol hello stroom van verkeer van en naar uw virtuele machines, maak een netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="83d33-133">toocontrol hello flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="83d33-134">Een netwerkbeveiligingsgroep kan worden toegepast tooa NIC of subnet.</span><span class="sxs-lookup"><span data-stu-id="83d33-134">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="83d33-135">Hallo volgende voorbeeld wordt [az netwerk nsg maken](/cli/azure/network/nsg#create) toocreate een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="83d33-135">hello following example uses [az network nsg create](/cli/azure/network/nsg#create) toocreate a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="83d33-136">U definieert de regels die bepaalde Hallo-verkeer toestaan of weigeren.</span><span class="sxs-lookup"><span data-stu-id="83d33-136">You define rules that allow or deny hello specific traffic.</span></span> <span data-ttu-id="83d33-137">tooallow binnenkomende verbindingen op poort 22 (toosupport SSH) maken een inkomende regel voor de netwerkbeveiligingsgroep Hallo met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="83d33-137">tooallow inbound connections on port 22 (toosupport SSH), create an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="83d33-138">Hallo volgende voorbeeld maakt u een regel met naam *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="83d33-138">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

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

<span data-ttu-id="83d33-139">tooallow binnenkomende verbindingen op poort 80 (toosupport internetverkeer), een ander netwerk groep beveiligingsregel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="83d33-139">tooallow inbound connections on port 80 (toosupport web traffic), add another network security group rule.</span></span> <span data-ttu-id="83d33-140">Hallo volgende voorbeeld maakt u een regel met naam *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="83d33-140">hello following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

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

<span data-ttu-id="83d33-141">Raadpleeg Hallo netwerkbeveiligingsgroep en regels met [az netwerk nsg weergeven](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="83d33-141">Examine hello network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="83d33-142">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="83d33-142">Output:</span></span>

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
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
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
      "description": "Allow outbound traffic from all VMs tooInternet",
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

## <a name="create-a-virtual-nic"></a><span data-ttu-id="83d33-143">Maken van een virtuele NIC</span><span class="sxs-lookup"><span data-stu-id="83d33-143">Create a virtual NIC</span></span>
<span data-ttu-id="83d33-144">Virtuele netwerkinterfacekaarten (NIC's) zijn programmatisch beschikbaar, omdat u regels tootheir gebruik kunt toepassen.</span><span class="sxs-lookup"><span data-stu-id="83d33-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="83d33-145">U kunt ook meer dan één hebben.</span><span class="sxs-lookup"><span data-stu-id="83d33-145">You can also have more than one.</span></span> <span data-ttu-id="83d33-146">In de volgende Hallo [az netwerk nic maken](/cli/azure/network/nic#create) opdracht maken van een NIC met de naam *myNic* en deze koppelen aan de netwerkbeveiligingsgroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="83d33-146">In hello following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with hello network security group.</span></span> <span data-ttu-id="83d33-147">openbaar IP-adres Hallo *myPublicIP* is ook gekoppeld aan Hallo virtuele NIC.</span><span class="sxs-lookup"><span data-stu-id="83d33-147">hello public IP address *myPublicIP* is also associated with hello virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="83d33-148">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="83d33-148">Output:</span></span>

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


## <a name="create-an-availability-set"></a><span data-ttu-id="83d33-149">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="83d33-149">Create an availability set</span></span>
<span data-ttu-id="83d33-150">Beschikbaarheidssets help verspreiding uw virtuele machines in domeinen met fouten en domeinen van de update.</span><span class="sxs-lookup"><span data-stu-id="83d33-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="83d33-151">Hoewel u slechts één virtuele machine nu maken, is de best practice toouse beschikbaarheid sets toomake deze eenvoudiger tooexpand in toekomstige Hallo.</span><span class="sxs-lookup"><span data-stu-id="83d33-151">Even though you only create one VM right now, it's best practice toouse availability sets toomake it easier tooexpand in hello future.</span></span> 

<span data-ttu-id="83d33-152">Domeinen met fouten definiëren een groepering van virtuele machines die een gemeenschappelijk power-bron- en switch delen.</span><span class="sxs-lookup"><span data-stu-id="83d33-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="83d33-153">Standaard zijn Hallo virtuele machines die zijn geconfigureerd in de beschikbaarheidsset gescheiden in up toothree domeinen met fouten.</span><span class="sxs-lookup"><span data-stu-id="83d33-153">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="83d33-154">Een hardwareprobleem in een van deze domeinen met fouten heeft geen invloed op elke virtuele machine die uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="83d33-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="83d33-155">Update domeinen groepen van virtuele machines en de onderliggende fysieke hardware die kan worden opgestart op Hallo duiden op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="83d33-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="83d33-156">Hallo volgorde in welke update domeinen worden opgestart mogelijk geen opeenvolgende tijdens gepland onderhoud, maar slechts één updatedomein tegelijk wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="83d33-156">During planned maintenance, hello order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="83d33-157">Virtuele machines distribueert Azure automatisch in Hallo probleem- en domeinen wanneer ze worden geplaatst in een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="83d33-157">Azure automatically distributes VMs across hello fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="83d33-158">Zie voor meer informatie [Hallo beschikbaarheid van virtuele machines beheren](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="83d33-158">For more information, see [managing hello availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="83d33-159">Maken van een beschikbaarheidsset voor uw virtuele machine met [az vm beschikbaarheidsset maken](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="83d33-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="83d33-160">Hallo volgende voorbeeld maakt u een beschikbaarheidsset benoemde *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="83d33-160">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="83d33-161">Hallo uitvoer opmerkingen bij de domeinen met fouten en domeinen bijwerken:</span><span class="sxs-lookup"><span data-stu-id="83d33-161">hello output notes fault domains and update domains:</span></span>

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


## <a name="create-hello-linux-vms"></a><span data-ttu-id="83d33-162">Hallo Linux virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="83d33-162">Create hello Linux VMs</span></span>
<span data-ttu-id="83d33-163">U hebt Hallo netwerk resources toosupport Internet toegankelijke VM's gemaakt.</span><span class="sxs-lookup"><span data-stu-id="83d33-163">You've created hello network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="83d33-164">Nu een virtuele machine maken en beveilig deze met een SSH-sleutel.</span><span class="sxs-lookup"><span data-stu-id="83d33-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="83d33-165">In dit geval gaan we een Ubuntu VM op basis van Hallo toocreate meest recente TNS.</span><span class="sxs-lookup"><span data-stu-id="83d33-165">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="83d33-166">U vindt aanvullende afbeeldingen met [az vm afbeeldingenlijst](/cli/azure/vm/image#list), zoals beschreven in [Azure VM-installatiekopieën vinden](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="83d33-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="83d33-167">We ook opgeven een SSH-sleutel toouse voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="83d33-167">We also specify an SSH key toouse for authentication.</span></span> <span data-ttu-id="83d33-168">Als u een openbare SSH-sleutelpaar niet hebt, kunt u [maken ze](mac-create-ssh-keys.md) of gebruik Hallo `--generate-ssh-keys` parameter toocreate ze voor u.</span><span class="sxs-lookup"><span data-stu-id="83d33-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use hello `--generate-ssh-keys` parameter toocreate them for you.</span></span> <span data-ttu-id="83d33-169">Als u al een sleutelpaar, als deze parameter gebruikt bestaande sleutels in `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="83d33-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="83d33-170">Hallo VM maken door onze bronnen en informatie samen met de Hallo brengen [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="83d33-170">Create hello VM by bringing all our resources and information together with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="83d33-171">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="83d33-171">hello following example creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="83d33-172">SSH tooyour VM Hello DNS-vermelding die u hebt opgegeven tijdens het maken van Hallo openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="83d33-172">SSH tooyour VM with hello DNS entry you provided when you created hello public IP address.</span></span> <span data-ttu-id="83d33-173">Dit `fqdn` in Hallo uitvoer wordt weergegeven als u uw virtuele machine maken:</span><span class="sxs-lookup"><span data-stu-id="83d33-173">This `fqdn` is shown in hello output as you create your VM:</span></span>

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

<span data-ttu-id="83d33-174">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="83d33-174">Output:</span></span>

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="83d33-175">U kunt installeren NGINX en Zie Hallo verkeer stroom toohello VM.</span><span class="sxs-lookup"><span data-stu-id="83d33-175">You can install NGINX and see hello traffic flow toohello VM.</span></span> <span data-ttu-id="83d33-176">NGINX als volgt installeren:</span><span class="sxs-lookup"><span data-stu-id="83d33-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="83d33-177">toosee hello NGINX standaardsite in actie, open uw webbrowser en voer de FQDN-naam:</span><span class="sxs-lookup"><span data-stu-id="83d33-177">toosee hello default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Standaard NGINX-site op de virtuele machine](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="83d33-179">Als een sjabloon exporteren</span><span class="sxs-lookup"><span data-stu-id="83d33-179">Export as a template</span></span>
<span data-ttu-id="83d33-180">Wat gebeurt er als u nu wilt toocreate een extra development environment Hello dezelfde parameters of een productie-omgeving die overeenkomt met het?</span><span class="sxs-lookup"><span data-stu-id="83d33-180">What if you now want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="83d33-181">Resource Manager JSON-sjablonen die alle Hallo parameters voor uw omgeving definiëren gebruikt.</span><span class="sxs-lookup"><span data-stu-id="83d33-181">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="83d33-182">U maken uit de volledige omgeving door te verwijzen naar deze JSON-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="83d33-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="83d33-183">U kunt [handmatig JSON-sjablonen samenstellen](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of een bestaande omgeving toocreate Hallo JSON-sjabloon exporteren voor u.</span><span class="sxs-lookup"><span data-stu-id="83d33-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you.</span></span> <span data-ttu-id="83d33-184">Gebruik [exporteren az](/cli/azure/group#export) tooexport uw resourcegroep als volgt:</span><span class="sxs-lookup"><span data-stu-id="83d33-184">Use [az group export](/cli/azure/group#export) tooexport your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="83d33-185">Deze opdracht maakt u Hallo `myResourceGroup.json` bestand in de huidige werkmap.</span><span class="sxs-lookup"><span data-stu-id="83d33-185">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="83d33-186">Wanneer u een omgeving met deze sjabloon maakt, wordt u gevraagd alle Hallo resourcenamen op te geven.</span><span class="sxs-lookup"><span data-stu-id="83d33-186">When you create an environment from this template, you are prompted for all hello resource names.</span></span> <span data-ttu-id="83d33-187">U kunt deze namen in uw sjabloonbestand vullen door toe te voegen Hallo `--include-parameter-default-value` parameter toohello `az group export` opdracht.</span><span class="sxs-lookup"><span data-stu-id="83d33-187">You can populate these names in your template file by adding hello `--include-parameter-default-value` parameter toohello `az group export` command.</span></span> <span data-ttu-id="83d33-188">Uw JSON-sjabloon toospecify Hallo resourcenamen, bewerken of [maken van een bestand parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) die Hallo resourcenamen aangeeft.</span><span class="sxs-lookup"><span data-stu-id="83d33-188">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="83d33-189">een omgeving met de sjabloon, gebruik toocreate [az implementatie maken](/cli/azure/group/deployment#create) als volgt:</span><span class="sxs-lookup"><span data-stu-id="83d33-189">toocreate an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="83d33-190">U kunt tooread [meer over hoe u toodeploy van sjablonen](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="83d33-190">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="83d33-191">Meer informatie over hoe tooincrementally update omgevingen, parameterbestand hello gebruiken en sjablonen gebruiken vanaf een enkele opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="83d33-191">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83d33-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="83d33-192">Next steps</span></span>
<span data-ttu-id="83d33-193">U bent nu klaar toobegin werken met meerdere netwerkonderdelen en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="83d33-193">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="83d33-194">Kunt u dit voorbeeld omgeving toobuild out van uw toepassing met behulp van Hallo kernonderdelen geïntroduceerd hier.</span><span class="sxs-lookup"><span data-stu-id="83d33-194">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
