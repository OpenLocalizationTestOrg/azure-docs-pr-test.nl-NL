---
title: aaaAzure voorbeeldscript CLI - Peer twee virtuele netwerken | Microsoft Docs
description: Azure CLI-voorbeeldscript - Peer twee virtuele netwerken
services: virtual-network
documentationcenter: virtual-network
author: KumudD
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
ms.author: kumud
ms.openlocfilehash: 54dabb2b9e05951d10f1b6b4f61ca592ce11d364
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a>Peer twee virtuele netwerken

Dit script wordt gemaakt en verbinding maakt twee virtuele netwerken in Hallo dezelfde regio trhough hello Azure-netwerk. Na het uitvoeren van script hello, maakt u een peering tussen twee virtuele netwerken.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ network vnet maken](https://docs.microsoft.com/cli/azure/network/vnet#create) | Maakt een virtueel Azure-netwerk en subnet. |
| [AZ network vnet-peering maken](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | Maakt een peering tussen twee virtuele netwerken.  |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende netwerken CLI scriptvoorbeelden kunnen u vinden in Hallo [overzicht van Azure-netwerken documentatie](../cli-samples.md).
