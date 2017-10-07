---
title: een Linux-VM in Azure met meerdere NIC's aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een Linux-VM met meerdere NIC's gekoppeld tooit hello Azure CLI 2.0 of Resource Manager-sjablonen.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a>Hoe toocreate virtuele Linux-machine in Azure met meerdere netwerk netwerkinterfacekaarten
U kunt een virtuele machine (VM) maken in Azure die meerdere virtuele netwerkinterfaces (NIC's) die zijn gekoppeld tooit heeft. Een veelvoorkomend scenario toohave verschillende subnetten voor front-end en back-end-connectiviteit is of een netwerk toegewezen tooa bewaking of back-upoplossing. Dit artikel wordt uitgelegd hoe toocreate met meerdere NIC's een virtuele machine gekoppeld tooit en hoe tooadd of verwijder NIC's van een bestaande virtuele machine. Voor gedetailleerde informatie, met inbegrip van hoe toocreate meerdere NIC's in uw eigen Bash-scripts, lees meer over [implementeren meerdere NIC's VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Andere [VM-grootten](sizes.md) ondersteunen een verschillend aantal NIC's, dus het formaat van uw virtuele machine dienovereenkomstig.

Dit artikel wordt uitgelegd hoe toocreate een virtuele machine met meerdere NIC's met Azure CLI 2.0 Hallo. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](multiple-nics-nodejs.md).


## <a name="create-supporting-resources"></a>Ondersteunende resources maken
Meest recente installatie Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. Voorbeeld parameternamen opgenomen *myResourceGroup*, *mystorageaccount*, en *myVM*.

Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:

```azurecli
az group create --name myResourceGroup --location eastus
```

Virtueel netwerk met Hallo maken [az network vnet maken](/cli/azure/network/vnet#create). Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* en subnet met de naam *mySubnetFrontEnd*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

Maak een subnet voor back-end-verkeer Hallo met [az network vnet subnet maken](/cli/azure/network/vnet/subnet#create). Hallo volgende voorbeeld wordt een subnet met de naam *mySubnetBackEnd*:

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

Maken van een netwerkbeveiligingsgroep met [az netwerk nsg maken](/cli/azure/network/nsg#create). Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a>Maak en configureer meerdere NIC 's
Maak twee NIC's met [az netwerk nic maken](/cli/azure/network/nic#create). Hallo volgende voorbeeld maakt u twee NIC's met de naam *myNic1* en *myNic2*, met elkaar verbonden Hallo netwerkbeveiligingsgroep, met één NIC tooeach subnet verbinding te maken:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Een virtuele machine maken en koppelen van Hallo NIC 's
Wanneer u Hallo VM maakt, geef Hallo NIC's u hebt gemaakt met `--nics`. U moet ook tootake voorzichtig wanneer u Hallo VM-grootte selecteert. Er gelden beperkingen voor Hallo kunt u het totale aantal NIC's die u tooa VM kunt toevoegen. Lees meer over [Linux VM-grootten](sizes.md). 

Maak een VM met [az vm create](/cli/azure/vm#create). Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a>Toevoegen van een NIC tooa VM
de vorige stappen Hallo gemaakt van een virtuele machine met meerdere NIC's. U kunt ook NIC's tooan bestaande VM Hello Azure CLI 2.0 toevoegen. 

Maken van een ander NIC met [az netwerk nic maken](/cli/azure/network/nic#create). Hallo volgende voorbeeld wordt een NIC met de naam *myNic3* toohello back-end-subnet en netwerkbeveiligingsgroep gemaakt in de vorige stappen Hallo verbonden:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

een NIC tooan tooadd bestaande VM eerst ongedaan Hallo VM met [az vm ongedaan](/cli/azure/vm#deallocate). Hallo volgende voorbeeld deallocates Hallo VM met de naam *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Voeg Hallo NIC met [az vm nic toevoegen](/cli/azure/vm/nic#add). Hallo volgende voorbeeld wordt *myNic3* te*myVM*:

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

Start met virtuele machine Hallo [az vm start](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a>Een NIC van een virtuele machine verwijderen
een NIC van een bestaande VM tooremove eerst Hallo VM ongedaan gemaakt met [az vm ongedaan](/cli/azure/vm#deallocate). Hallo volgende voorbeeld deallocates Hallo VM met de naam *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Verwijder Hallo NIC met [az vm nic verwijderen](/cli/azure/vm/nic#remove). Hallo volgende voorbeeld wordt verwijderd *myNic3* van *myVM*:

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

Start met virtuele machine Hallo [az vm start](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
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
Bekijk [Linux VM-grootten](sizes.md) bij het toocreating met meerdere NIC's een virtuele machine. Betalen aandacht toohello maximum aantal NIC's die ondersteuning biedt voor elke VM-grootte. 
