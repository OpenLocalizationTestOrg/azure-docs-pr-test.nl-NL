---
title: aaaAzure CLI voorbeeldscript - routeverkeer via een virtueel netwerkapparaat | Microsoft Docs
description: 'Azure CLI - voorbeeldscript: de Route-verkeer via een firewall netwerk virtueel apparaat.'
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>-Routeverkeer via een virtueel netwerkapparaat

Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten. Een virtuele machine wordt gemaakt met ingeschakelde tooroute verkeer tussen de twee subnetten Hallo doorsturen via IP. U kunt na het uitvoeren van script Hallo netwerksoftware, zoals een firewalltoepassing toohello VM implementeren.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Voorbeeld van een script


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate na een resourcegroep, het virtuele netwerk en netwerkbeveiligingsgroepen. Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ network vnet maken](/cli/azure/network/vnet#create) | Maakt een virtueel Azure-netwerk en de front-end-subnet. |
| [AZ netwerksubnet maken](/cli/azure/network/vnet/subnet#create) | Maakt back-end en DMZ subnetten. |
| [AZ netwerk openbare ip-maken](/cli/azure/network/public-ip#create) | Maakt een openbare IP-adres tooaccess-Hallo VM van Hallo Internet. |
| [AZ netwerk nic maken](/cli/azure/network/nic#create) | Maakt een virtuele netwerkinterface en doorsturen via IP inschakelen voor deze. |
| [nsg voor AZ netwerk maken](/cli/azure/network/nsg#create) | Maakt een netwerkbeveiligingsgroep (NSG). |
| [AZ netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) | NSG-regels waarmee HTTP en HTTPS-poorten inkomend toohello VM maakt. |
| [AZ network vnet subnet bijwerken](/cli/azure/network/vnet/subnet#update)| Gekoppeld Hallo nsg's en route toosubnets tabellen. |
| [AZ netwerk routetabel maken](/cli/azure/network/route-table#create)| Een routetabel voor alle routes maken. |
| [netwerkroute AZ-routetabel maken](/cli/azure/network/route-table/route#create)| Routes maakt tooroute verkeer tussen subnetten en Hallo Internet via VM Hallo. |
| [AZ vm maken](/cli/azure/vm#create) | Een virtuele machine maakt en koppelt Hallo NIC tooit. Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toouse en beheerdersreferenties. |
| [AZ groep verwijderen](/cli/azure/group#delete) | Hiermee verwijdert u een resourcegroep en alle resources die deze bevat. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](/cli/azure/overview).

Aanvullende netwerken CLI scriptvoorbeelden kunnen u vinden in Hallo [overzicht netwerken van Azure-documentatie](../cli-samples.md)
