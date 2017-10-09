---
title: een volledige Linux-omgeving Hello Azure CLI 1.0 aaaCreate | Microsoft Docs
description: Opslag, een Linux-VM, een virtueel netwerk en subnet, een load balancer, een NIC, een openbare IP-adres en een netwerkbeveiligingsgroep maken via Hallo gemalen met behulp van hello Azure CLI 1.0.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a>Een volledige Linux-omgeving maken met Azure CLI 1.0 Hallo
In dit artikel verder gaan we met een eenvoudig netwerk met een combinatie van virtuele machines die gebruikt voor ontwikkeling en eenvoudige computing worden en een load balancer. We doorlopen Hallo proces door de opdracht, totdat u twee hebt, beveiligde virtuele Linux-machines toowhich die u verbinding van een willekeurige plaats op Hallo Internet maken kunt. Vervolgens kunt u op toomore complexe netwerken en omgevingen.

Langs Hallo manier u meer informatie over Hallo afhankelijkheidshiërarchie dat Hallo Resource Manager-implementatiemodel u biedt, en over hoeveel power biedt. Nadat u hoe Hallo systeem is gemaakt ziet, kunt u opnieuw bouwen het veel sneller met behulp van [Azure Resource Manager-sjablonen](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ook, nadat u leert hoe onderdelen van uw omgeving Hallo bij elkaar passen, sjablonen tooautomate maken ze eenvoudiger.

Hallo-omgeving bevat:

* Twee virtuele machines in een beschikbaarheidsset.
* Een load balancer met een regel voor load balancing op poort 80.
* Netwerkbeveiligingsgroep (NSG) regels tooprotect tegen ongewenste verkeer van de VM.

toocreate deze aangepaste omgeving, moet u Hallo nieuwste [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in de modus Resource Manager (`azure config mode arm`). U moet ook een JSON hulpprogramma parseren. In dit voorbeeld wordt [jq](https://stedolan.github.io/jq/).


## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel


## <a name="quick-commands"></a>Snelle opdrachten
Als u moet tooquickly Hallo taak, na de sectie details Hallo Hallo baseren opdrachten tooupload een tooAzure VM. Meer gedetailleerde informatie en context voor elke stap vindt u in de rest Hallo van Hallo document, te beginnen [hier](#detailed-walkthrough).

Zorg ervoor dat u hebt [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) aangemeld en het gebruik van Resource Manager-modus:

```azurecli
azure config mode arm
```

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.

Hallo resourcegroep maken. Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westeurope` locatie:

```azurecli
azure group create -n myResourceGroup -l westeurope
```

Hallo resourcegroep controleren met behulp van Hallo JSON-parser:

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Hallo-opslagaccount maken. Hallo volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount`. (Hallo opslagaccountnaam moet uniek zijn, zodat uw eigen unieke naam opgeven.)

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

Hallo storage-account met behulp van de JSON-parser Hallo controleren:

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

Hallo virtueel netwerk maken. Hallo volgende voorbeeld wordt een virtueel netwerk met de naam `myVnet`:

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

Een subnet maken. Hallo volgende voorbeeld wordt een subnet met de naam `mySubnet`:

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

Hallo virtueel netwerk en subnet controleren met behulp van Hallo JSON-parser:

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Maak een openbare IP-adres. Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam `myPublicIP` met Hallo DNS-naam van `mypublicdns`. (Hallo DNS-naam moet uniek zijn, zodat uw eigen unieke naam opgeven.)

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

Hallo load balancer maken. Hallo volgende voorbeeld maakt u een load balancer met de naam `myLoadBalancer`:

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

Maak een front-end-IP-adresgroep voor Hallo load balancer, en koppel Hallo openbare IP-adres. Hallo volgende voorbeeld wordt een front-end-IP-adresgroep met de naam `mySubnetPool`:

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

Hallo backend-IP-adresgroep voor Hallo load balancer maken. Hallo volgende voorbeeld wordt een back-end-IP-adresgroep met de naam `myBackEndPool`:

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

SSH inkomende netwerk address translation (NAT) regels voor Hallo load balancer maken. Hallo volgende voorbeeld maakt u twee regels van load balancer, `myLoadBalancerRuleSSH1` en `myLoadBalancerRuleSSH2`:

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

Maken van webinhoud Hallo inkomende NAT-regels voor Hallo de load balancer. Hallo volgende voorbeeld maakt u een regel voor load balancer met de naam `myLoadBalancerRuleWeb`:

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

Hallo health load balancer-test maken. Hallo volgende voorbeeld wordt een TCP-test met de naam `myHealthProbe`:

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

Hallo load balancer, IP-adresgroepen en NAT-regels controleren met behulp van Hallo JSON-parser:

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

Hallo eerste netwerkinterfacekaart (NIC) maken. Vervang Hallo `#####-###-###` secties met uw eigen Azure-abonnement-ID. Uw abonnement ID wordt vermeld in de uitvoer van Hallo **jq** wanneer u bekijkt hello resources die u maakt. U kunt ook uw abonnements-ID met weergeven `azure account list`.

Hallo volgende voorbeeld wordt een NIC met de naam `myNic1`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

De tweede NIC Hallo maken Hallo volgende voorbeeld wordt een NIC met de naam `myNic2`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

Controleer of u Hallo twee NIC's met behulp van de JSON-parser Hallo:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

Hallo netwerkbeveiligingsgroep maken. Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam `myNetworkSecurityGroup`:

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

Twee regels voor binnenkomende verbindingen voor Hallo netwerkbeveiligingsgroep toevoegen. Hallo volgende voorbeeld maakt u twee regels `myNetworkSecurityGroupRuleSSH` en `myNetworkSecurityGroupRuleHTTP`:

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

Controleer of u Hallo netwerkbeveiligingsgroep en regels voor binnenkomende verbindingen met behulp van de JSON-parser Hallo:

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

Hallo netwerkbeveiliging binden groep toohello twee NIC's:

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

Hallo beschikbaarheidsset maken. Hallo volgende voorbeeld maakt u een beschikbaarheidsset benoemde `myAvailabilitySet`:

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

Maak Hallo eerste Linux VM. Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM1`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Hallo maken tweede Linux VM. Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM2`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Hallo JSON-parser tooverify gebruiken die alles die is gemaakt:

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

Uw nieuwe omgeving tooa sjabloon tooquickly opnieuw maken nieuwe exemplaren exporteren:

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht
Hallo gedetailleerde stappen volgen wordt uitgelegd wat elke opdracht doet tijdens het samenstellen van buiten uw omgeving. Deze begrippen zijn handig als u uw eigen aangepaste omgevingen voor ontwikkeling of productie bouwen.

Zorg ervoor dat u hebt [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) aangemeld en het gebruik van Resource Manager-modus:

```azurecli
azure config mode arm
```

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.

## <a name="create-resource-groups-and-choose-deployment-locations"></a>Maken van resourcegroepen en locaties implementatie kiezen
Azure-resourcegroepen zijn logische implementatie entiteiten met gegevens en metagegevens tooenable Hallo logische beheer van de configuratie van de resource-implementaties. Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westeurope` locatie:

```azurecli
azure group create --name myResourceGroup --location westeurope
```

Uitvoer:

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a>Een opslagaccount maken
U moet de storage-accounts voor de VM-schijven en eventuele extra gegevensschijven die u tooadd wilt. U kunt storage-accounts maken bijna onmiddellijk na het maken van resourcegroepen.

Hier gebruiken we Hallo `azure storage account create` opdracht, en Hallo type opslagondersteuning gewenste Hallo-locatie van de resourcegroep Hallo Hallo account die wordt doorgegeven bepaalt. Hallo volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount`:

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

Uitvoer:

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

onze resourcegroep via Hallo tooexamine `azure group show` opdracht, gebruiken we Hallo [jq](https://stedolan.github.io/jq/) hulpprogramma samen met de Hallo `--json` Azure CLI-optie. (U kunt **jsawk** of enkele taal bibliotheek u liever tooparse Hallo JSON.)

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Uitvoer:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

tooinvestigate hello storage-account met behulp van Hallo CLI, moet u eerst tooset Hallo accountnamen en sleutels. Hallo-naam van de storage-account in het volgende voorbeeld met een naam die u kiest Hallo Hallo vervangen:

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

U kunt vervolgens uw storage-gegevens eenvoudig bekijken:

```azurecli
azure storage container list
```

Uitvoer:

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a>Een virtueel netwerk en subnet maken
Vervolgens gaat u tooneed toocreate een virtueel netwerk in Azure en een subnet van uw virtuele machines maken worden uitgevoerd. Hallo volgende voorbeeld wordt een virtueel netwerk met de naam `myVnet` Hello `192.168.0.0/16` adresvoorvoegsel:

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

Uitvoer:

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

We gebruiken opnieuw Hallo--json-optie van `azure group show` en `jq` toosee hoe we onze bronnen bouwen. Nu een `storageAccounts` resource en een `virtualNetworks` resource.  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Uitvoer:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

Nu gaan we een subnet maken in Hallo `myVnet` virtueel netwerk in welke Hallo virtuele machines zijn geïmplementeerd. We gebruiken Hallo `azure network vnet subnet create` opdracht samen met de Hallo resources we al hebt gemaakt: Hallo `myResourceGroup` resourcegroep en Hallo `myVnet` virtueel netwerk. In de Hallo voorbeeld te volgen, we Hallo subnet met de naam toevoegen `mySubnet` met Hallo subnet adresvoorvoegsel van `192.168.1.0/24`:

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

Uitvoer:

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

Omdat Hallo subnet logisch in het virtuele netwerk hello, zoekt we Hallo subnet met een iets andere opdracht. Hallo-opdracht we gebruiken is `azure network vnet show`, maar we verder tooexamine Hallo JSON-uitvoer met behulp van `jq`.

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Uitvoer:

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a>Een openbaar IP-adres maken
Nu gaan we maken Hallo openbaar IP-adres (PIP) dat we tooyour load balancer toewijzen. Hiermee kunt u tooconnect tooyour VM's van Hallo Internet met behulp van Hallo `azure network public-ip create` opdracht. Omdat Hallo standaardadres dynamisch is, maken we een benoemde DNS-vermelding in Hallo **cloudapp.azure.com** domein met behulp van Hallo `--domain-name-label` optie. Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam `myPublicIP` met Hallo DNS-naam van `mypublicdns`. Aangezien Hallo DNS-naam uniek zijn moet, kunt u uw eigen unieke DNS-naam opgeven:

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

Uitvoer:

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

Hallo openbaar IP-adres is ook een bron op het hoogste niveau, zodat u deze met ziet `azure group show`.

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Uitvoer:

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

U kunt meer informatie over resource, zoals Hallo volledig gekwalificeerde domeinnaam (FQDN) van subdomein hello, met behulp van de volledige Hallo onderzoeken `azure network public-ip show` opdracht. Hallo openbare IP-adres resource logisch is toegewezen, maar een specifiek adres nog niet is toegewezen. een IP-adres tooobtain, gaat u tooneed een load balancer die we nog geen hebt gemaakt.

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

Uitvoer:

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a>Een load balancer en IP-adresgroepen maken
Wanneer u een load balancer maakt, kunt u toodistribute verkeer over meerdere virtuele machines. Het bevat ook redundantie tooyour toepassing door het uitvoeren van meerdere virtuele machines die toouser aanvragen in Hallo-gebeurtenis van onderhoud of zware belasting reageren. Hallo volgende voorbeeld maakt u een load balancer met de naam `myLoadBalancer`:

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

Uitvoer:

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

De load balancer is redelijk leeg, dus gaan we een aantal IP-adresgroepen maken. We willen toocreate twee IP-adresgroepen voor de load balancer, één voor Hallo-front-end en één voor de back-end Hallo. de front-end-IP-adresgroep Hallo is openbaar zichtbaar. Het is ook Hallo locatie toowhich die we toewijzen Hallo PIP die we eerder hebben gemaakt. Vervolgens gebruiken we Hallo back-end-pool als locatie voor onze tooconnect VM's aan. Op die manier Hallo-verkeer door Hallo load balancer toohello VMs kan stromen.

Eerst laten we onze front-end-IP-adresgroep maken. Hallo volgende voorbeeld wordt een front-groep met de naam `myFrontEndPool`:

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

Uitvoer:

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

Houd er rekening mee hoe we Hallo gebruikt `--public-ip-name` toopass in Hallo switch `myPublicIP` die we eerder hebben gemaakt. Toewijzen van Hallo openbare IP-adres toohello load balancer kunt u tooreach uw virtuele machines via Hallo Internet.

Vervolgens maken we onze tweede IP-adresgroep voor de back-end-verkeer. Hallo volgende voorbeeld wordt een back-end-pool met de naam `myBackEndPool`:

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

Uitvoer:

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

We zien hoe u onze load balancer doet door te zoeken met `azure network lb show` en onderzoeken Hallo JSON-uitvoer:

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

Uitvoer:

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a>NAT-regels van load balancer maken
tooget verkeer via de load balancer moeten we toocreate netwerk address translation (NAT) regels die binnenkomend of uitgaand acties specificeren. U kunt opgeven Hallo protocol toouse vervolgens externe poorten toointernal poorten naar wens worden toegewezen. Voor onze omgeving gaan we een aantal regels maken die SSH toestaan via onze load balancer tooour virtuele machines. We instellen TCP-poorten 4222 en 4223 toodirect tooTCP poort 22 op de virtuele machines (die we later maken). Hallo volgende voorbeeld maakt u een regel met naam `myLoadBalancerRuleSSH1` 4222 tooport 22 toomap TCP-poort:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

Uitvoer:

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

Herhaal Hallo procedure voor de tweede NAT-regel voor SSH. Hallo volgende voorbeeld maakt u een regel met naam `myLoadBalancerRuleSSH2` 4223 tooport 22 toomap TCP-poort:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

We gaan ook opwekken en maak een NAT-regel voor TCP-poort 80 voor internetverkeer, Hallo regel aansluiting up tooour IP-adresgroepen. Als we IP-adresgroep, in plaats van een afzonderlijk, up Hallo regel tooour VMs aansluiting aansluiten Hallo regel tooan kunnen we toevoegen of verwijderen van virtuele machines van Hallo IP-adresgroep. Hallo load balancer automatisch aangepast Hallo verkeersstroom. Hallo volgende voorbeeld maakt u een regel met naam `myLoadBalancerRuleWeb` toomap TCP-poort 80 tooport 80:

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

Uitvoer:

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a>Een load balancer health test maken
Een health test regelmatig controles op Hallo van virtuele machines die zich achter onze load balancer-toomake ervoor dat ze zijn het functioneren en toorequests reageert, zoals is gedefinieerd. Als u niet, ze verwijderd uit omgeleid bewerking tooensure dat gebruikers worden niet wordt toothem. U kunt aangepaste controles voor de Hallo health test, samen met intervallen en time-outwaarden definiëren. Zie voor meer informatie over statuscontroles [Load Balancer-tests](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Hallo volgende voorbeeld wordt een TCP health aangeduid met de naam `myHealthProbe`:

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

Uitvoer:

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

Hier wordt een interval van 15 seconden voor onze statuscontroles opgegeven. We kunnen maximaal vier tests (één minuut) voordat Hallo load balancer overweegt dat die host Hallo werkt niet meer over het hoofd ziet.

## <a name="verify-hello-load-balancer"></a>Controleer of Hallo load balancer
Nu wordt Hallo load balancer-configuratie uitgevoerd. Hier volgen Hallo manier te werk:

1. U hebt gemaakt voor een load balancer.
2. U een front-end-IP-adresgroep gemaakt en een openbare IP-tooit toegewezen.
3. U een back-end-IP-adresgroep die virtuele machines verbinding met maken kunnen gemaakt.
4. U NAT-regels waarmee SSH toohello VM's voor beheer, samen met een regel waarmee u TCP-poort 80 voor de web-app hebt gemaakt.
5. U hebt een health test tooperiodically selectievakje Hallo VM's toegevoegd. Deze test health zorgt ervoor dat gebruikers een virtuele machine die niet meer werkt of inhoud tooaccess niet proberen.

We bekijken wat de load balancer er nu uit:

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

Uitvoer:

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a>Maken van een NIC toouse Hello Linux VM
NIC's zijn programmatisch beschikbaar, omdat u regels tootheir gebruik kunt toepassen. U kunt ook meer dan één hebben. In de volgende Hallo `azure network nic create` opdracht u aansluiten Hallo NIC toohello load back-end-IP-adresgroep en deze koppelen aan Hallo NAT-regel toopermit SSH-verkeer.

Vervang Hallo `#####-###-###` secties met uw eigen Azure-abonnement-ID. Uw abonnement ID wordt vermeld in de uitvoer van Hallo `jq` wanneer u bekijkt hello resources die u maakt. U kunt ook uw abonnements-ID met weergeven `azure account list`.

Hallo volgende voorbeeld wordt een NIC met de naam `myNic1`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

Uitvoer:

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

Hallo details kunt u zien door Hallo resource rechtstreeks in. U Hallo resource bestuderen met behulp van Hallo `azure network nic show` opdracht:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

Uitvoer:

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

Nu we maken Hallo tweede NIC, opnieuw koppelen in tooour backend-IP-adresgroep. Deze tijd Hallo tweede NAT-regel toestaat SSH verkeer. Hallo volgende voorbeeld wordt een NIC met de naam `myNic2`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a>Een netwerkbeveiligingsgroep en regels maken
Nu een netwerkbeveiligingsgroep maken en regels voor binnenkomende verbindingen die van toepassing hello toegang krijgen tot toohello NIC. Een netwerkbeveiligingsgroep kan worden toegepast tooa NIC of subnet. U definiëren regels toocontrol Hallo verkeersstroom in uw virtuele machines. Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam `myNetworkSecurityGroup`:

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

We voegen inkomende hello-regel voor Hallo NSG tooallow binnenkomende verbindingen op poort 22 (toosupport SSH). Hallo volgende voorbeeld maakt u een regel met naam `myNetworkSecurityGroupRuleSSH` tooallow TCP op poort 22:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

Nu gaan we voegen inkomende hello-regel voor Hallo NSG tooallow binnenkomende verbindingen op poort 80 (webverkeer toosupport). Hallo volgende voorbeeld maakt u een regel met naam `myNetworkSecurityGroupRuleHTTP` tooallow TCP op poort 80:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> inkomende Hello-regel is een filter naar binnenkomende netwerkverbindingen. In dit voorbeeld binden we Hallo NSG toohello VMs virtuele NIC, wat betekent dat elke aanvraag tooport 22 wordt doorgegeven via toohello NIC op de virtuele machine. Deze regel binnenkomende over een netwerkverbinding is en niet over een eindpunt met dit is wat het normaal zou zijn over in klassieke implementaties. tooopen een poort, moet u Hallo laten `--source-port-range` instellen te '\*' (standaardwaarde Hallo) tooaccept inkomende aanvragen van **eventuele** poort aanvraagt. Poorten zijn meestal dynamisch zijn.
>
>

## <a name="bind-toohello-nic"></a>BIND toohello NIC
Hallo NSG toohello NIC's worden gebonden. We moeten tooconnect onze NIC's met onze netwerkbeveiligingsgroep. Voer beide opdrachten, toohook van beide onze NIC's:

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a>Een beschikbaarheidsset maken
Beschikbaarheidssets help verspreiding uw virtuele machines in domeinen met fouten en upgradedomeinen. Laten we de beschikbaarheidsset voor uw virtuele machines maken. Hallo volgende voorbeeld maakt u een beschikbaarheidsset benoemde `myAvailabilitySet`:

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

Domeinen met fouten definiëren een groepering van virtuele machines die een gemeenschappelijk power-bron- en switch delen. Standaard zijn Hallo virtuele machines die zijn geconfigureerd in de beschikbaarheidsset gescheiden in up toothree domeinen met fouten. Hallo idee is een hardwareprobleem in een van deze domeinen met fouten heeft geen invloed op elke virtuele machine die uw app wordt uitgevoerd. Virtuele machines verdeelt Azure automatisch over Hallo foutdomeinen wanneer ze worden geplaatst in een beschikbaarheidsset.

Upgradedomeinen groepen van virtuele machines en de onderliggende fysieke hardware die kan worden opgestart op Hallo duiden op hetzelfde moment. Hallo volgorde waarin upgradedomeinen worden opgestart mogelijk geen opeenvolgende tijdens gepland onderhoud, maar slechts één upgrade opnieuw wordt opgestart tegelijk. Opnieuw verdeelt Azure automatisch uw virtuele machines over upgradedomeinen wanneer ze worden geplaatst in een site beschikbaarheid.

Lees meer over [Hallo beschikbaarheid van virtuele machines beheren](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="create-hello-linux-vms"></a>Hallo Linux virtuele machines maken
U hebt Hallo-opslag- en netwerkbronnen toosupport Internet toegankelijke VM's gemaakt. Nu gaan we die virtuele machines maken en ze zijn beveiligd met een SSH-sleutel die geen wachtwoord. In dit geval gaan we een Ubuntu VM op basis van Hallo toocreate meest recente TNS. We vinden die informatie van de installatiekopie met behulp van `azure vm image list`, zoals beschreven in [Azure VM-installatiekopieën vinden](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

We een installatiekopie van een geselecteerd met de opdracht Hallo `azure vm image list westeurope canonical | grep LTS`. In dit geval gebruiken we `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`. Voor het laatste veld hello, geven we `latest` zodat in de toekomst Hallo we altijd de meest recente build Hallo gaan. (we gebruiken Hallo-tekenreeks is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).

Deze stap is bekend tooanyone die al is gemaakt door een ssh rsa openbare en persoonlijke sleutel koppelen op Linux- of Mac via **ssh-keygen - t rsa -b 2048**. Als u nog geen sleutelparen die een certificaat uw `~/.ssh` directory, kunt u deze maken:

* Automatisch via Hallo `azure vm create --generate-ssh-keys` optie.
* Handmatig met behulp van [Hallo instructies toocreate ze zelf](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

U kunt ook hello gebruiken `--admin-password` methode tooauthenticate uw SSH-verbindingen na Hallo VM wordt gemaakt. Deze methode is meestal minder goed beveiligd.

We Hallo VM maken door onze bronnen en informatie samen met de Hallo brengen `azure vm create` opdracht:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Uitvoer:

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

U kunt tooyour VM direct verbinding maken met behulp van uw standaard SSH-sleutels. Zorg ervoor dat u de juiste poort Hallo opgeeft omdat we via Hallo load balancer geven. (Voor onze eerste VM we ingesteld Hallo NAT regel tooforward poort 4222 tooour VM.)

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

Uitvoer:

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

Maak uw tweede VM in Hallo dezelfde manier:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

En u kunt nu Hallo `azure vm show myResourceGroup myVM1` opdracht tooexamine wat u hebt gemaakt. U uitvoert op dit moment uw Ubuntu VM's achter een load balancer in Azure die u aanmelden kunt bij alleen met uw SSH-sleutelpaar (omdat wachtwoorden zijn uitgeschakeld). U kunt installeren nginx of httpd, een web-app implementeren en Zie Hallo verkeer verloopt via Hallo load balancer tooboth Hallo VM's.

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

Uitvoer:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a>Hallo-omgeving exporteren als een sjabloon
Nu dat u hebt gemaakt om een extra development environment Hello uit deze omgeving, wat gebeurt er als u wilt dat toocreate dezelfde parameters of een productie-omgeving die overeenkomt met het? Resource Manager JSON-sjablonen die alle Hallo parameters voor uw omgeving definiëren gebruikt. U maken uit de volledige omgeving door te verwijzen naar deze JSON-sjabloon. U kunt [handmatig JSON-sjablonen samenstellen](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of een bestaande omgeving toocreate Hallo JSON-sjabloon voor u te exporteren:

```azurecli
azure group export --name myResourceGroup
```

Deze opdracht maakt u Hallo `myResourceGroup.json` bestand in de huidige werkmap. Wanneer u een omgeving met deze sjabloon maakt, wordt u gevraagd alle Hallo resourcenamen, inclusief Hallo namen voor Hallo load balancer, netwerkinterfaces of virtuele machines op te geven. U kunt deze namen in uw sjabloonbestand vullen door toe te voegen Hallo `-p` of `--includeParameterDefaultValue` parameter toohello `azure group export` opdracht die eerder is aangegeven. Uw JSON-sjabloon toospecify Hallo resourcenamen, bewerken of [maken van een bestand parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) die Hallo resourcenamen aangeeft.

een omgeving met de sjabloon toocreate:

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

U kunt tooread [meer over hoe u toodeploy van sjablonen](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Meer informatie over hoe tooincrementally update omgevingen, parameterbestand hello gebruiken en sjablonen gebruiken vanaf een enkele opslaglocatie.

## <a name="next-steps"></a>Volgende stappen
U bent nu klaar toobegin werken met meerdere netwerkonderdelen en virtuele machines. Kunt u dit voorbeeld omgeving toobuild out van uw toepassing met behulp van Hallo kernonderdelen geïntroduceerd hier.
