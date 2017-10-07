---
title: aaaAzure voorbeeldscript CLI - twee virtuele machines maken met een interne en externe NSG | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: twee virtuele machines maken met de interne en externe NSG'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a>Beveiligen van netwerkverkeer tussen virtuele machines

Dit script maakt twee virtuele machines en binnenkomende verkeer tooboth beveiligt. Een virtuele machine is toegankelijk op Hallo van internet en is een netwerkbeveiligingsgroep (NSG) tooallow verkeer geconfigureerd op poort 22 en 80. Hallo tweede virtuele machine is niet toegankelijk op Hallo van internet en is een NSG geconfigureerd tooonly verkeer van de eerste virtuele machine Hallo toestaan. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ network vnet maken](https://docs.microsoft.com/cli/azure/network/vnet#create) | Maakt een virtueel Azure-netwerk en subnet. |
| [AZ network vnet subnet maken](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | Maakt een subnet. |
| [AZ vm maken](https://docs.microsoft.com/cli/azure/vm#create) | Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden. Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.  |
| [lijst van de regel met het nsg van netwerken AZ](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | Retourneert informatie over een groep voor de netwerkbeveiligingsregel. In dit voorbeeld wordt Hallo regelnaam opgeslagen in een variabele voor gebruik verderop in het Hallo-script. |
| [AZ netwerk nsg regel update](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | Een regel voor het NSG-updates. In dit voorbeeld is Hallo back-end regel bijgewerkte toopass verkeer alleen via Hallo front-end-subnet. |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
