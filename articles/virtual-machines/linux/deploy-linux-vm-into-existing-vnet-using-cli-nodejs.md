---
title: aaaDeploy virtuele Linux-machines in bestaande netwerk met Azure CLI 1.0 | Microsoft Docs
description: Hoe een Linux-VM naar een bestaand virtueel netwerk met behulp van toodeploy hello Azure CLI 1.0
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a>Hoe een virtuele Linux-machine in Azure een bestaand virtueel netwerk met Azure CLI 1.0 Hallo toodeploy

Dit artikel ziet u hoe toouse Azure CLI 1.0 toodeploy een virtuele machine (VM) in een bestaand virtueel netwerk (VNet). Hallo-vereisten zijn:

- [een Azure-account.](https://azure.microsoft.com/pricing/free-trial/)
- [bestanden voor openbare en persoonlijke SSH-sleutels](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel


## <a name="quick-commands"></a>Snelle opdrachten

Als u moet tooquickly Hallo taak, Hallo sectie volgen details Hallo opdrachten die nodig zijn. Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).

Randvoorwaarden voor: Resourcegroep, VNet, NSG met SSH inkomende Subnet. Geen voorbeelden vervangen door uw eigen instellingen.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Hallo VM in Hallo virtuele netwerkinfrastructuur implementeren

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht

Azure activa zoals Hallo VNets en netwerkbeveiligingsgroepen moeten statisch zijn en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven. Zodra een VNet is geïmplementeerd, kan opnieuw door nieuwe implementaties zonder een nadelige invloed toohello infrastructuur worden gebruikt. Denk na over een VNet dat een netwerkswitch traditionele hardware. U hoeft dan niet een geheel nieuwe hardware overschakelen met elke implementatie tooconfigure. Met een juist geconfigureerde VNet, kunt u blijven toodeploy nieuwe servers in dit VNet steeds met enkele eventuele wijzigingen gedurende de levensduur Hallo Hallo VNet vereist.

## <a name="create-hello-resource-group"></a>Hallo resourcegroep maken

Maak eerst een groep resource tooorganize alles wat die u in dit scenario maakt. Zie voor meer informatie over resourcegroepen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a>Hallo VNet maken

de eerste stap Hallo is toobuild een VNet-toolaunch Hallo VM's in. Hallo VNet bevat één subnet voor dit scenario. Zie voor meer informatie over Azure VNets [een virtueel netwerk maken met behulp van hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a>Hallo netwerkbeveiligingsgroep maken

Hallo-subnet is gebouwd achter een bestaande netwerkbeveiligingsgroep dus bouwen Hallo netwerkbeveiligingsgroep voordat Hallo subnet. Beveiligingsgroepen voor Azure-netwerk zijn equivalent tooa firewall op Hallo netwerklaag. Zie voor meer informatie over Azure netwerkbeveiligingsgroepen [hoe toocreate netwerk beveiligingsgroepen in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Regel voor geven van een binnenkomende SSH toevoegen

Hallo VM moet toegang vanaf Hallo internet zodat een regel voor het toestaan van binnenkomende poort 22 verkeer toobe Hallo netwerk tooport 22 op Hallo VM doorgegeven nodig is.

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Voeg een subnet toohello VNet

Virtuele machines binnen Hallo VNet moeten zich bevinden in een subnet. Elke VNet kan meerdere subnetten hebben. Hallo subnet maken en koppelen aan de netwerkbeveiligingsgroep Hallo.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

Hallo Subnet is nu toegevoegd in Hallo VNet en die zijn gekoppeld aan netwerkbeveiligingsgroep hello en regel.


## <a name="add-a-vnic-toohello-subnet"></a>Een VNic toohello subnet toevoegen

Virtueel-netwerkkaarten (VNics) zijn belangrijk omdat u ze hergebruiken kunt door deze toodifferent virtuele machines te verbinden. Deze aanpak houdt Hallo VNic als statische resource Hallo VMs tijdelijke kan zijn. Een VNic maken en deze koppelen aan Hallo subnet in de vorige stap Hallo gemaakt.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Hallo VM in Hallo VNet en NSG implementeren

U hebt nu een VNet en het subnet in dit VNet en een netwerkbeveiligingsgroep tooprotect Hallo subnet blokkeert al het binnenkomende verkeer behalve poort 22 voor SSH fungeert. Hallo VM kan nu worden geïmplementeerd in deze bestaande netwerkinfrastructuur.

Met behulp van Azure CLI Hallo en Hallo `azure vm create` opdracht Hallo Linux VM geïmplementeerde toohello bestaande Azure-resourcegroep, VNet Subnet en VNic is. Zie voor meer informatie over het gebruik van Hallo CLI toodeploy een volledige virtuele machine [een volledige Linux-omgeving maken met behulp van hello Azure CLI](create-cli-complete.md)

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

Met behulp van Hallo vlaggen CLI toocall uit bestaande resources instrueren van Azure toodeploy Hallo VM binnen de bestaande netwerk Hallo. Zodra een VNet en een subnet is geïmplementeerd, kunnen ze als statisch of permanente resources binnen uw Azure-regio worden gelaten.  

## <a name="next-steps"></a>Volgende stappen

* [Een Azure Resource Manager-sjabloon toocreate een specifieke implementatie gebruiken](../windows/cli-deploy-templates.md)
* [Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten](create-cli-complete.md)
* [Linux-VM in Azure met behulp van sjablonen maken](create-ssh-secured-vm-from-template.md)
