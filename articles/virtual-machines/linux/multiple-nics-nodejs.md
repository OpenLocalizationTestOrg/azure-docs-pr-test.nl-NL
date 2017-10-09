---
title: een Linux-VM in Azure met meerdere NIC's aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een Linux-VM met meerdere NIC's gekoppeld tooit hello Azure CLI of Resource Manager-sjablonen.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a>Een virtuele Linux-machine maken met meerdere NIC's met behulp van hello Azure CLI 1.0
U kunt een virtuele machine (VM) maken in Azure die meerdere virtuele netwerkinterfaces (NIC's) die zijn gekoppeld tooit heeft. Een veelvoorkomend scenario toohave verschillende subnetten voor front-end en back-end-connectiviteit is of een netwerk toegewezen tooa bewaking of back-upoplossing. Dit artikel vindt u een virtuele machine met meerdere NIC's gekoppeld tooit toocreate snelle opdrachten. Voor gedetailleerde informatie, met inbegrip van hoe toocreate meerdere NIC's in uw eigen Bash-scripts, lees meer over [implementeren meerdere NIC's VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Andere [VM-grootten](sizes.md) ondersteunen een verschillend aantal NIC's, dus het formaat van uw virtuele machine dienovereenkomstig.

> [!WARNING]
> Wanneer u een virtuele machine maken: u kunt geen NIC's tooan bestaande VM Hello Azure CLI 1.0 toevoegen, moet u meerdere NIC's koppelen. U kunt [toegevoegd netwerkkaarten tooan bestaande VM Hello Azure CLI 2.0](multiple-nics.md). U kunt ook [maken van een virtuele machine op basis van de oorspronkelijke virtuele schijven Hallo](copy-vm.md) en meerdere NIC's maken als u Hallo VM implementeren.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#create-supporting-resources) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](multiple-nics.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel


## <a name="create-supporting-resources"></a>Ondersteunende resources maken
Zorg ervoor dat u Hallo hebt [Azure CLI](../../cli-install-nodejs.md) aangemeld en het gebruik van Resource Manager-modus:

```azurecli
azure config mode arm
```

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. Voorbeeld parameternamen opgenomen *myResourceGroup*, *mystorageaccount*, en *myVM*.

Maak eerst een resourcegroep. Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:

```azurecli
azure group create myResourceGroup --location eastus
```

Maak een account opslag toohold uw virtuele machines. Hallo volgende voorbeeld wordt een opslagaccount met de naam *mystorageaccount*:

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

Een virtueel netwerk tooconnect uw virtuele machines te maken. Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* met een adresvoorvoegsel van *192.168.0.0/16*:

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

Maken van twee virtuele netwerksubnetten: één voor verkeer van de front-end- en één voor verkeer van de back-end. Hallo volgende voorbeeld maakt u twee subnetten, met de naam *mySubnetFrontEnd* en *mySubnetBackEnd*:

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a>Maak en configureer meerdere NIC 's
Vindt u meer informatie over [implementeren meerdere NIC's met behulp van Azure CLI Hallo](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), inclusief scripts Hallo proces toocreate doorlopen van alle Hallo NIC's.

Hallo volgende voorbeeld maakt u twee NIC's met de naam *myNic1* en *myNic2*, met één NIC tooeach subnet verbinding te maken:

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

Maakt u gewoonlijk ook een [Netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md) of [netwerktaakverdeler](../../load-balancer/load-balancer-overview.md) toohelp beheren en distribueren van verkeer tussen uw virtuele machines. Hallo volgende voorbeeld wordt een Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

BIND uw NIC's toohello Netwerkbeveiligingsgroep met `azure network nic set`. Hallo volgende voorbeeld wordt gebonden *myNic1* en *myNic2* met *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Een virtuele machine maken en koppelen van Hallo NIC 's
Bij het maken van VM Hallo opgeven u nu meerdere NIC's. In plaats daarvan met `--nic-name` tooprovide één NIC, gebruik in plaats daarvan u `--nic-names` en een door komma's gescheiden lijst met NIC's bieden. U moet ook tootake voorzichtig wanneer u Hallo VM-grootte selecteert. Er gelden beperkingen voor Hallo kunt u het totale aantal NIC's die u tooa VM kunt toevoegen. Lees meer over [Linux VM-grootten](sizes.md). Hallo volgende voorbeeld laat zien hoe toospecify meerdere NIC's en klik vervolgens op een virtuele machine het formaat dat ondersteunt het gebruik van meerdere NIC's (*Standard_DS2_v2*):

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a>Meerdere NIC's met behulp van Resource Manager-sjablonen maken
Azure Resource Manager-sjablonen gebruiken declaratieve JSON-bestanden toodefine uw omgeving. U vindt een [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Resource Manager-sjablonen bieden een manier toocreate meerdere exemplaren van een bron tijdens implementatie, zoals meerdere NIC's maken. U gebruikt *kopie* toospecify Hallo aantal exemplaren toocreate:

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

Lees meer over [maken van meerdere exemplaren die gebruikmaken van *kopie*](../../resource-group-create-multiple.md). 

U kunt ook een `copyIndex()` toothen toevoeg-een nummer tooa resourcenaam, zodat u toocreate `myNic1`, `myNic2`, enzovoort Hallo hieronder vindt u een voorbeeld van de indexwaarde Hallo:

```json
"name": "[concat('myNic', copyIndex())]", 
```

U kunt een compleet voorbeeld van lezen [meerdere NIC's met behulp van Resource Manager-sjablonen maken](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Volgende stappen
Zorg ervoor dat tooreview [Linux VM-grootten](sizes.md) bij het toocreating met meerdere NIC's een virtuele machine. Betalen aandacht toohello maximum aantal NIC's die ondersteuning biedt voor elke VM-grootte. 

Houd er rekening mee dat u aanvullende NIC's tooan bestaande VM niet toevoegen, moet u alle Hallo NIC's maken bij het implementeren van Hallo VM. Wees voorzichtig bij het plannen van uw implementaties toomake ervoor dat u alle Hallo vereist netwerkverbinding vanaf Hallo begin hebt.

