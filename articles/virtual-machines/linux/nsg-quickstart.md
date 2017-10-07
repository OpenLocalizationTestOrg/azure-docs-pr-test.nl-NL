---
title: aaaOpen poorten tooa Linux-VM met Azure CLI 2.0 | Microsoft Docs
description: Meer informatie over hoe een poort tooopen / maken van een eindpunt tooyour Linux-VM met hello Azure resource manager deployment model en hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a>Openen van poorten en eindpunten tooa Linux VM Hello Azure CLI
U een poort openen of maken van een eindpunt tooa virtuele machine (VM) in Azure door het maken van een netwerk-filter op een subnet of een VM-netwerkinterface. U plaatsen deze filters die binnenkomend en uitgaand verkeer worden beheerd, van een Netwerkbeveiligingsgroep gekoppeld toohello resource die Hallo verkeer ontvangt. We gebruiken een voorbeeld van webverkeer op poort 80. Dit artikel ziet u hoe tooopen een poort tooa VM Hello Azure CLI 2.0. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).


## <a name="quick-commands"></a>Snelle opdrachten
toocreate een netwerkbeveiliging en regels u moet recente Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter *myResourceGroup*, *myNetworkSecurityGroup*, en *myVnet*.

Maken van de netwerkbeveiligingsgroep met Hallo [az netwerk nsg maken](/cli/azure/network/nsg#create). Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup* in Hallo *eastus* locatie:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Toevoegen van een regel met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) tooallow HTTP verkeer tooyour webserver (of aanpassen voor uw eigen scenario, zoals SSH-toegang of database connectivity). Hallo volgende voorbeeld maakt u een regel met naam *myNetworkSecurityGroupRule* tooallow TCP-verkeer op poort 80:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

Hallo Netwerkbeveiligingsgroep koppelen aan uw VM-netwerkinterface (NIC) met [az netwerk nic update](/cli/azure/network/nic#update). Hallo volgende voorbeeld wordt gekoppeld aan een bestaande NIC met de naam *myNic* Hello Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

U kunt ook uw Netwerkbeveiligingsgroep koppelen aan een virtueel netwerksubnet met [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) in plaats van alleen toohello netwerkinterface op een enkele virtuele machine. Hallo volgende voorbeeld wordt een bestaand subnet met de naam *mySubnet* in Hallo *myVnet* virtueel netwerk met Hallo Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a>Meer informatie over Netwerkbeveiligingsgroepen
Hallo-hier snelle opdrachten kunt u tooget up en wordt uitgevoerd met verkeer stromende tooyour VM. Netwerkbeveiligingsgroepen bieden veel handige functies en verfijning voor het beheren van toegang tot tooyour bronnen. U kunt meer lezen over [hier maken van een Netwerkbeveiligingsgroep en ACL regels](tutorial-virtual-network.md#secure-network-traffic).

Voor maximaal beschikbare webtoepassingen, moet u uw virtuele machines achter een Load Balancer van Azure plaatsen. Hallo-taakverdeling verkeer tooVMs, met een Netwerkbeveiligingsgroep waarmee wordt verkeer gefilterd. Zie voor meer informatie [hoe tooload saldo Linux virtuele machines in Azure toocreate een maximaal beschikbare toepassing](tutorial-load-balancer.md).

## <a name="next-steps"></a>Volgende stappen
In dit voorbeeld moet u een eenvoudige regel tooallow HTTP-verkeer gemaakt. Hier vindt u informatie over het maken van meer gedetailleerde omgevingen in Hallo artikelen te volgen:

* [Overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Wat is een netwerkbeveiligingsgroep (NSG)?](../../virtual-network/virtual-networks-nsg.md)
