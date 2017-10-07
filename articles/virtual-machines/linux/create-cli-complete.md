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
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a>Een volledige virtuele Linux-machine maken met hello Azure CLI
tooquickly maken van een virtuele machine (VM) in Azure, kunt u één opdracht Azure CLI die gebruikmaakt van standaard waarden toocreate welke verplicht ondersteunende resources gebruiken. Resources, zoals een virtueel netwerk, openbare IP-adres en netwerkbeveiligingsgroepen worden automatisch gemaakt. Voor meer controle over uw omgeving in de productieomgeving gebruikt, u kunt deze resources tevoren maken en voeg vervolgens uw toothem virtuele machines. In dit artikel begeleidt u bij hoe toocreate een virtuele machine en alle ondersteunende resources één voor één Hallo.

Zorg ervoor dat u Hallo laatste hebt geïnstalleerd [Azure CLI 2.0](/cli/azure/install-az-cli2) en geregistreerde tooan Azure-account met [az aanmelding](/cli/azure/#login).

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter *myResourceGroup*, *myVnet*, en *myVM*.

## <a name="create-resource-group"></a>Een resourcegroep maken
Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. Een resourcegroep moet worden gemaakt voordat een virtuele machine en de ondersteunende bronnen van het virtuele netwerk. Maak Hallo resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:

```azurecli
az group create --name myResourceGroup --location eastus
```

Hallo-uitvoer van de Azure CLI-opdrachten is standaard in JSON (JavaScript Object Notation). toochange hello uitvoer tooa standaardlijst of tabel, bijvoorbeeld gebruiken [az configureren--uitvoer](/cli/azure/#configure). U kunt ook toevoegen `--output` tooany opdracht voor een eenmalige wijzigen in de indeling van uitvoer. Hallo volgende voorbeeld ziet u JSON-uitvoer van Hallo Hallo `az group create` opdracht:

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

## <a name="create-a-virtual-network-and-subnet"></a>Een virtueel netwerk en subnet maken
Vervolgens maken van een virtueel netwerk in Azure en een subnet in toowhich kunt u uw virtuele machines maken. Gebruik [az network vnet maken](/cli/azure/network/vnet#create) toocreate een virtueel netwerk met de naam *myVnet* Hello *192.168.0.0/16* adresvoorvoegsel. U ook een subnet met de naam toevoegen *mySubnet* met het Hallo-adresvoorvoegsel van *192.168.1.0/24*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

Hallo uitvoer toont logisch gemaakt in het virtuele netwerk Hallo Hallo-subnet:

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


## <a name="create-a-public-ip-address"></a>Een openbaar IP-adres maken
Nu gaan we maken een openbaar IP-adres met [az netwerk openbare ip-maken](/cli/azure/network/public-ip#create). Dit openbare IP-adres, kunt u tooconnect tooyour VM's van Hallo Internet. Omdat Hallo standaardadres dynamisch is, we ook een benoemde DNS-vermelding maken met de Hallo `--domain-name-label` optie. Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam *myPublicIP* met Hallo DNS-naam van *mypublicdns*. Aangezien Hallo DNS-naam uniek zijn moet, Geef uw eigen unieke DNS-naam:

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

Uitvoer:

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


## <a name="create-a-network-security-group"></a>Een netwerkbeveiligingsgroep maken
toocontrol hello stroom van verkeer van en naar uw virtuele machines, maak een netwerkbeveiligingsgroep. Een netwerkbeveiligingsgroep kan worden toegepast tooa NIC of subnet. Hallo volgende voorbeeld wordt [az netwerk nsg maken](/cli/azure/network/nsg#create) toocreate een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

U definieert de regels die bepaalde Hallo-verkeer toestaan of weigeren. tooallow binnenkomende verbindingen op poort 22 (toosupport SSH) maken een inkomende regel voor de netwerkbeveiligingsgroep Hallo met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create). Hallo volgende voorbeeld maakt u een regel met naam *myNetworkSecurityGroupRuleSSH*:

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

tooallow binnenkomende verbindingen op poort 80 (toosupport internetverkeer), een ander netwerk groep beveiligingsregel toevoegen. Hallo volgende voorbeeld maakt u een regel met naam *myNetworkSecurityGroupRuleHTTP*:

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

Raadpleeg Hallo netwerkbeveiligingsgroep en regels met [az netwerk nsg weergeven](/cli/azure/network/nsg#show):

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

Uitvoer:

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

## <a name="create-a-virtual-nic"></a>Maken van een virtuele NIC
Virtuele netwerkinterfacekaarten (NIC's) zijn programmatisch beschikbaar, omdat u regels tootheir gebruik kunt toepassen. U kunt ook meer dan één hebben. In de volgende Hallo [az netwerk nic maken](/cli/azure/network/nic#create) opdracht maken van een NIC met de naam *myNic* en deze koppelen aan de netwerkbeveiligingsgroep Hallo. openbaar IP-adres Hallo *myPublicIP* is ook gekoppeld aan Hallo virtuele NIC.

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

Uitvoer:

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


## <a name="create-an-availability-set"></a>Een beschikbaarheidsset maken
Beschikbaarheidssets help verspreiding uw virtuele machines in domeinen met fouten en domeinen van de update. Hoewel u slechts één virtuele machine nu maken, is de best practice toouse beschikbaarheid sets toomake deze eenvoudiger tooexpand in toekomstige Hallo. 

Domeinen met fouten definiëren een groepering van virtuele machines die een gemeenschappelijk power-bron- en switch delen. Standaard zijn Hallo virtuele machines die zijn geconfigureerd in de beschikbaarheidsset gescheiden in up toothree domeinen met fouten. Een hardwareprobleem in een van deze domeinen met fouten heeft geen invloed op elke virtuele machine die uw app wordt uitgevoerd.

Update domeinen groepen van virtuele machines en de onderliggende fysieke hardware die kan worden opgestart op Hallo duiden op hetzelfde moment. Hallo volgorde in welke update domeinen worden opgestart mogelijk geen opeenvolgende tijdens gepland onderhoud, maar slechts één updatedomein tegelijk wordt opgestart.

Virtuele machines distribueert Azure automatisch in Hallo probleem- en domeinen wanneer ze worden geplaatst in een beschikbaarheidsset. Zie voor meer informatie [Hallo beschikbaarheid van virtuele machines beheren](manage-availability.md).

Maken van een beschikbaarheidsset voor uw virtuele machine met [az vm beschikbaarheidsset maken](/cli/azure/vm/availability-set#create). Hallo volgende voorbeeld maakt u een beschikbaarheidsset benoemde *myAvailabilitySet*:

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

Hallo uitvoer opmerkingen bij de domeinen met fouten en domeinen bijwerken:

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


## <a name="create-hello-linux-vms"></a>Hallo Linux virtuele machines maken
U hebt Hallo netwerk resources toosupport Internet toegankelijke VM's gemaakt. Nu een virtuele machine maken en beveilig deze met een SSH-sleutel. In dit geval gaan we een Ubuntu VM op basis van Hallo toocreate meest recente TNS. U vindt aanvullende afbeeldingen met [az vm afbeeldingenlijst](/cli/azure/vm/image#list), zoals beschreven in [Azure VM-installatiekopieën vinden](cli-ps-findimage.md).

We ook opgeven een SSH-sleutel toouse voor verificatie. Als u een openbare SSH-sleutelpaar niet hebt, kunt u [maken ze](mac-create-ssh-keys.md) of gebruik Hallo `--generate-ssh-keys` parameter toocreate ze voor u. Als u al een sleutelpaar, als deze parameter gebruikt bestaande sleutels in `~/.ssh`.

Hallo VM maken door onze bronnen en informatie samen met de Hallo brengen [az vm maken](/cli/azure/vm#create) opdracht. Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM*:

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

SSH tooyour VM Hello DNS-vermelding die u hebt opgegeven tijdens het maken van Hallo openbaar IP-adres. Dit `fqdn` in Hallo uitvoer wordt weergegeven als u uw virtuele machine maken:

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

Uitvoer:

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

U kunt installeren NGINX en Zie Hallo verkeer stroom toohello VM. NGINX als volgt installeren:

```bash
sudo apt-get install -y nginx
```

toosee hello NGINX standaardsite in actie, open uw webbrowser en voer de FQDN-naam:

![Standaard NGINX-site op de virtuele machine](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a>Als een sjabloon exporteren
Wat gebeurt er als u nu wilt toocreate een extra development environment Hello dezelfde parameters of een productie-omgeving die overeenkomt met het? Resource Manager JSON-sjablonen die alle Hallo parameters voor uw omgeving definiëren gebruikt. U maken uit de volledige omgeving door te verwijzen naar deze JSON-sjabloon. U kunt [handmatig JSON-sjablonen samenstellen](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of een bestaande omgeving toocreate Hallo JSON-sjabloon exporteren voor u. Gebruik [exporteren az](/cli/azure/group#export) tooexport uw resourcegroep als volgt:

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

Deze opdracht maakt u Hallo `myResourceGroup.json` bestand in de huidige werkmap. Wanneer u een omgeving met deze sjabloon maakt, wordt u gevraagd alle Hallo resourcenamen op te geven. U kunt deze namen in uw sjabloonbestand vullen door toe te voegen Hallo `--include-parameter-default-value` parameter toohello `az group export` opdracht. Uw JSON-sjabloon toospecify Hallo resourcenamen, bewerken of [maken van een bestand parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) die Hallo resourcenamen aangeeft.

een omgeving met de sjabloon, gebruik toocreate [az implementatie maken](/cli/azure/group/deployment#create) als volgt:

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

U kunt tooread [meer over hoe u toodeploy van sjablonen](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Meer informatie over hoe tooincrementally update omgevingen, parameterbestand hello gebruiken en sjablonen gebruiken vanaf een enkele opslaglocatie.

## <a name="next-steps"></a>Volgende stappen
U bent nu klaar toobegin werken met meerdere netwerkonderdelen en virtuele machines. Kunt u dit voorbeeld omgeving toobuild out van uw toepassing met behulp van Hallo kernonderdelen geïntroduceerd hier.
