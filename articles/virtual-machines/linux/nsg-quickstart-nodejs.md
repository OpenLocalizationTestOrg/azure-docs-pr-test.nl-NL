---
title: aaaOpen poorten tooa Linux-VM met Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over hoe een poort tooopen / maken van een eindpunt tooyour Linux-VM met hello Azure resource manager deployment model en Azure CLI 1.0 Hallo
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a>Openen poorten en eindpunten tooa Linux VM aan Azure met Azure CLI 1.0 Hallo
U een poort openen of maken van een eindpunt tooa virtuele machine (VM) in Azure door het maken van een netwerk-filter op een subnet of een VM-netwerkinterface. U plaatsen deze filters die binnenkomend en uitgaand verkeer worden beheerd, van een Netwerkbeveiligingsgroep gekoppeld toohello resource die Hallo verkeer ontvangt. We gebruiken een voorbeeld van webverkeer op poort 80. Dit artikel laat zien hoe een poort tooa VM met tooopen hello Azure CLI 1.0.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](nsg-quickstart.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel


## <a name="quick-commands"></a>Snelle opdrachten
een Netwerkbeveiligingsgroep toocreate en regels moet u [hello Azure CLI 1.0](../../cli-install-nodejs.md) geïnstalleerd en met Resource Manager-modus:

```azurecli
azure config mode arm
```

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. Voorbeeld parameternamen opgenomen *myResourceGroup*, *myNetworkSecurityGroup*, en *myVnet*.

Maak de beveiligingsgroep van uw netwerk, invoeren van uw eigen namen en de locatie op de juiste wijze. Hallo volgende voorbeeld wordt een Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup* in Hallo *eastus* locatie:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Een regel tooallow HTTP-verkeer tooyour webserver toevoegen (of aanpassen voor uw eigen scenario, zoals SSH-toegang of database connectivity). Hallo volgende voorbeeld maakt u een regel met naam *myNetworkSecurityGroupRule* tooallow TCP-verkeer op poort 80:

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

Hallo Netwerkbeveiligingsgroep koppelen aan uw VM-netwerkinterface (NIC). Hallo volgende voorbeeld wordt gekoppeld aan een bestaande NIC met de naam *myNic* Hello Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

U kunt ook uw Netwerkbeveiligingsgroep koppelen aan een virtueel netwerksubnet in plaats van alleen toohello netwerkinterface op een enkele virtuele machine. Hallo volgende voorbeeld wordt een bestaand subnet met de naam *mySubnet* in Hallo *myVnet* virtueel netwerk met Hallo Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a>Meer informatie over Netwerkbeveiligingsgroepen
Hallo-hier snelle opdrachten kunt u tooget up en wordt uitgevoerd met verkeer stromende tooyour VM. Netwerkbeveiligingsgroepen bieden veel handige functies en verfijning voor het beheren van toegang tot tooyour bronnen. U kunt meer lezen over [hier maken van een Netwerkbeveiligingsgroep en ACL regels](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).

U kunt Netwerkbeveiligingsgroepen en ACL-regels definiëren als onderdeel van Azure Resource Manager-sjablonen. Lees meer over [Netwerkbeveiligingsgroepen maken met behulp van sjablonen](../../virtual-network/virtual-networks-create-nsg-arm-template.md).

Als u toouse poort doorsturen toomap een unieke externe poort tooan interne poort op de virtuele machine moet, gebruikt u een load balancer en Network Address Translation (NAT)-regels. U kunt bijvoorbeeld tooexpose TCP-poort 8080 extern wilt en verkeer wordt gestuurd tooTCP poort 80 op een virtuele machine hebben. U kunt meer informatie over [maken van een Internet gerichte load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).

## <a name="next-steps"></a>Volgende stappen
In dit voorbeeld moet u een eenvoudige regel tooallow HTTP-verkeer gemaakt. Hier vindt u informatie over het maken van meer gedetailleerde omgevingen in Hallo artikelen te volgen:

* [Overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Wat is een netwerkbeveiligingsgroep (NSG)?](../../virtual-network/virtual-networks-nsg.md)
* [Overzicht van Azure Resource Manager voor Load Balancers](../../load-balancer/load-balancer-arm.md)

