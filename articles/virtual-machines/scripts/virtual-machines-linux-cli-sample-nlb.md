---
title: aaaAzure voorbeeldscript CLI - Maak een Linux-VM met NLB | Microsoft Docs
description: Azure CLI Script voorbeeld - een virtuele Linux-machine maken met NLB
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
ms.openlocfilehash: 79b245c1268734fead313b34c120f74ab2330d4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-highly-available-vm"></a>Een maximaal beschikbare virtuele machine maken

Dit voorbeeldscript wordt gemaakt van alles wat u nodig toorun verschillende Ubuntu virtuele machines geconfigureerd in een maximaal beschikbare en load balanced configuratie. Nadat het Hallo-script wordt uitgevoerd, hebt u drie virtuele machines, gekoppelde tooan Beschikbaarheidsset Azure en zijn toegankelijk via een Azure Load Balancer. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, virtuele machine, beschikbaarheidsset, load balancer en alle gerelateerde resources te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ network vnet maken](https://docs.microsoft.com/cli/azure/network/vnet#create) | Maakt een virtueel Azure-netwerk en subnet. |
| [AZ netwerk openbare ip-maken](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Hiermee maakt een openbaar IP-adres met een statisch IP-adres en een bijbehorende DNS-naam. |
| [AZ network Load Balancer maken](https://docs.microsoft.com/cli/azure/network/lb#create) | Hiermee maakt u een Azure-netwerk Load Balancer (NLB). |
| [AZ network Load Balancer-test maken](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Maakt een NLB-test. Een NLB-test gebruikte toomonitor elke virtuele machine in Hallo NLB set is. Als een virtuele machine niet meer toegankelijk is, wordt verkeer is geen gerouteerde toohello VM. |
| [AZ network Load Balancer-regel maken](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Maakt een regel voor NLB. In dit voorbeeld wordt een regel gemaakt voor poort 80. Zoals HTTP-verkeer bij Hallo NLB aankomt, is het gerouteerde tooport 80 een Hallo VM's in Hallo NLB set. |
| [AZ netwerk lb-nat-regel voor binnenkomende verbindingen maken](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | Maakt een regel voor NLB Network Address Translation (NAT).  NAT-regels toewijzen een poort Hallo NLB tooa poort op een virtuele machine. In dit voorbeeld wordt een NAT-regel gemaakt voor SSH-verkeer tooeach VM in Hallo NLB set.  |
| [nsg voor AZ netwerk maken](https://docs.microsoft.com/cli/azure/network/nsg#create) | Maakt een netwerkbeveiligingsgroep (NSG), die een beveiligingsgrens tussen Hallo internet en Hallo virtuele machine. |
| [AZ netwerk nsg regel maken](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Hiermee maakt u een NSG regel tooallow binnenkomend verkeer. In dit voorbeeld wordt poort 22 voor SSH-verkeer geopend. |
| [AZ netwerk nic maken](https://docs.microsoft.com/cli/azure/network/nic#create) | Maakt een virtueel netwerkkaart en toohello virtueel netwerk, subnet en NSG gekoppeld. |
| [AZ vm beschikbaarheidsset maken](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Hiermee maakt een beschikbaarheidsset. Beschikbaarheidssets waarborgen uptime van toepassingen via Hallo virtuele machines verspreid over fysieke resources zo dat als fout optreedt, wordt de hele set Hallo niet gedaan. |
| [AZ vm maken](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden. Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.  |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
