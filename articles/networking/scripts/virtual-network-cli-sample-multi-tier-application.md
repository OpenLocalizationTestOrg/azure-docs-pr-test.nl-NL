---
title: aaaAzure CLI script steekproef - maken van een netwerk voor toepassingen met meerdere lagen | Microsoft Docs
description: 'Azure CLI-script voorbeeld: een virtueel netwerk voor toepassingen met meerdere lagen maken.'
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
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a>Een netwerk voor toepassingen met meerdere lagen maken

Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten. Verkeer toohello front-end-subnet is beperkt tooHTTP en SSH, tijdens het verkeer toohello back-end-subnet is beperkt tooMySQL, poort 3306. Na het Hallo-script wordt uitgevoerd hebt u twee virtuele machines, één in elk subnet dat u kunt webserver en MySQL-software te implementeren.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Voorbeeld van een script


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

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
| [AZ netwerksubnet maken](/cli/azure/network/vnet/subnet#create) | Maakt een back-end-subnet. |
| [AZ netwerk openbare ip-maken](/cli/azure/network/public-ip#create) | Maakt een openbare IP-adres tooaccess-Hallo VM van Hallo Internet. |
| [AZ netwerk nic maken](/cli/azure/network/nic#create) | Virtuele netwerkinterfaces maakt en koppelt deze toohello van het virtuele netwerk front-end en back-end-subnetten. |
| [nsg voor AZ netwerk maken](/cli/azure/network/nsg#create) | Netwerkbeveiligingsgroepen (NSG) die gekoppeld toohello front-end en back-end subnetten zijn maakt. |
| [AZ netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) |NSG-regels toestaan of blokkeren van bepaalde poorten toospecific subnetten maakt. |
| [AZ vm maken](/cli/azure/vm#create) | Virtuele machines maakt en koppelt een NIC tooeach VM. Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toouse en beheerdersreferenties. |
| [AZ groep verwijderen](/cli/azure/group#delete) | Hiermee verwijdert u een resourcegroep en alle resources die deze bevat. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](/cli/azure/overview).

Aanvullende netwerken CLI scriptvoorbeelden kunnen u vinden in Hallo [overzicht netwerken van Azure-documentatie](../cli-samples.md)
