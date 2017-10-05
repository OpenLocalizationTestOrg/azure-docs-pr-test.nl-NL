---
title: Implementeren van virtuele Linux-machines in de bestaande netwerk met Azure CLI 1.0 | Microsoft Docs
description: Het implementeren van een Linux-VM naar een bestaand virtueel netwerk met behulp van de Azure CLI 1.0
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
ms.openlocfilehash: 767a3f7cadba6b1e71e5a8f5995a9db090e419dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli-10"></a>Het implementeren van een virtuele Linux-machine in Azure een bestaand virtueel netwerk met de Azure CLI 1.0

In dit artikel laat zien hoe Azure CLI 1.0 gebruiken voor het implementeren van een virtuele machine (VM) in een bestaand virtueel netwerk (VNet). De vereisten zijn:

- [een Azure-account.](https://azure.microsoft.com/pricing/free-trial/)
- [bestanden voor openbare en persoonlijke SSH-sleutels](mac-create-ssh-keys.md)


## <a name="cli-versions-to-complete-the-task"></a>CLI-versies om de taak uit te voeren
U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:

- [Azure CLI 1.0](#quick-commands) – onze CLI voor het klassieke en resource management-implementatiemodel (in dit artikel)
- [Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel


## <a name="quick-commands"></a>Snelle opdrachten

Als u de taak snel uitvoeren moet, wordt de volgende sectie de opdrachten die nodig zijn. Meer gedetailleerde informatie en context voor elke stap u de rest van het document vindt [vanaf hier](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).

Randvoorwaarden voor: Resourcegroep, VNet, NSG met SSH inkomende Subnet. Geen voorbeelden vervangen door uw eigen instellingen.

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a>Implementeer de virtuele machine in de infrastructuur van het virtuele netwerk

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

Azure activa, zoals de VNets en netwerkbeveiligingsgroepen moeten statisch zijn en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven. Zodra een VNet is geïmplementeerd, kan dit opnieuw gebruikt door nieuwe implementaties zonder een ongewenst is van invloed op de infrastructuur. Denk na over een VNet dat een netwerkswitch traditionele hardware. U moet niet een geheel nieuwe hardwareswitch configureren met elke implementatie. U kunt blijven implementeren nieuwe servers in dit VNet steeds met enkele eventuele wijzigingen die zijn vereist tijdens de levensduur van het VNet met een juist geconfigureerde VNet.

## <a name="create-the-resource-group"></a>De resourcegroep maken

Maak eerst een resourcegroep te organiseren alles wat die u in dit scenario maakt. Zie voor meer informatie over resourcegroepen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-the-vnet"></a>Het VNet maken

De eerste stap is het bouwen van een VNet Start de virtuele machines in. Het VNet bevat één subnet voor dit scenario. Zie voor meer informatie over Azure VNets [een virtueel netwerk maken met behulp van de Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-the-network-security-group"></a>De netwerkbeveiligingsgroep maken

Het subnet is gebouwd achter een bestaand netwerk beveiligingsgroep maken zodat de netwerkbeveiligingsgroep voor het subnet. Beveiligingsgroepen voor Azure-netwerk zijn equivalent aan een firewall op de netwerklaag. Zie voor meer informatie over Azure netwerkbeveiligingsgroepen [netwerk beveiligingsgroepen maken in de Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Regel voor geven van een binnenkomende SSH toevoegen

De virtuele machine moet toegang via het internet, zodat een regel binnenkomende poort 22-verkeer op de virtuele machine via het netwerk worden doorgegeven aan poort 22 nodig is.

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

## <a name="add-a-subnet-to-the-vnet"></a>Voeg een subnet toe aan het VNet

Virtuele machines binnen het VNet moeten zich bevinden in een subnet. Elke VNet kan meerdere subnetten hebben. Het subnet te maken en koppelen aan de netwerkbeveiligingsgroep.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

Het Subnet is nu toegevoegd in het VNet en die zijn gekoppeld aan de netwerkbeveiligingsgroep en de regelset.


## <a name="add-a-vnic-to-the-subnet"></a>Een VNic toevoegen aan het subnet

Virtueel-netwerkkaarten (VNics) zijn belangrijk omdat u ze hergebruiken kunt door deze te verbinden met andere virtuele machines. Deze aanpak houdt de VNic als statische resource terwijl de virtuele machines kunnen tijdelijk zijn. Een VNic maken en deze koppelen aan het subnet in de vorige stap hebt gemaakt.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a>Implementeer de virtuele machine in het VNet en het NSG

U hebt nu een VNet en het subnet in dit VNet en een netwerkbeveiligingsgroep ter bescherming van het subnet blokkeert al het binnenkomende verkeer behalve poort 22 voor SSH fungeert. De virtuele machine kan nu worden geïmplementeerd in deze bestaande netwerkinfrastructuur.

Met de Azure CLI, en de `azure vm create` opdracht, de Linux-VM wordt geïmplementeerd op de bestaande Azure-resourcegroep, VNet, Subnet en VNic. Zie voor meer informatie over een volledige virtuele machine implementeren met behulp van de CLI [een volledige Linux-omgeving maken met behulp van de Azure CLI](create-cli-complete.md)

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

Met behulp van de vlaggen CLI aan te roepen bestaande bronnen, vertelt u Azure voor het implementeren van de virtuele machine binnen de bestaande netwerk. Zodra een VNet en een subnet is geïmplementeerd, kunnen ze als statisch of permanente resources binnen uw Azure-regio worden gelaten.  

## <a name="next-steps"></a>Volgende stappen

* [Een Azure Resource Manager-sjabloon gebruiken om een specifieke implementatie te maken](../windows/cli-deploy-templates.md)
* [Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten](create-cli-complete.md)
* [Linux-VM in Azure met behulp van sjablonen maken](create-ssh-secured-vm-from-template.md)
