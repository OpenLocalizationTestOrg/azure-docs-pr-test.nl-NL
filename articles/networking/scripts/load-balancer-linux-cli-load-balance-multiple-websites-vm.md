---
title: aaaAzure voorbeeldscript CLI - taakverdeling toe te passen meerdere websites Hello Azure CLI | Microsoft Docs
description: Azure CLI-voorbeeldscript - taakverdeling toe te passen meerdere websites toohello dezelfde virtuele machine
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Taakverdeling maken voor meerdere websites

Dit voorbeeldscript wordt een virtueel netwerk maakt met twee virtuele machines (VM) die lid van een beschikbaarheidsset zijn. Een load balancer stuurt verkeer voor twee afzonderlijke IP-adressen toohello twee virtuele machines. Na het Hallo-script wordt uitgevoerd, kan u web server software toohello virtuele machines implementeren en hosten van meerdere websites, elk met een eigen IP-adres.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep of virtueel netwerk, load balancer en alle gerelateerde resources te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ network vnet maken](https://docs.microsoft.com/cli/azure/network/vnet#create) | Maakt een virtueel Azure-netwerk en subnet. |
| [AZ netwerk openbare ip-maken](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Hiermee maakt een openbaar IP-adres met een statisch IP-adres en een bijbehorende DNS-naam. |
| [AZ network Load Balancer maken](https://docs.microsoft.com/cli/azure/network/lb#create) | Hiermee maakt u een Azure Load Balancer. |
| [AZ network Load Balancer-test maken](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Hiermee maakt u een load balancer-test. Een load balancer-test gebruikte toomonitor elke virtuele machine in Hallo load balancer-set is. Als een virtuele machine niet meer toegankelijk is, wordt verkeer is geen gerouteerde toohello VM. |
| [AZ network Load Balancer-regel maken](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Maakt een regel voor load balancer. In dit voorbeeld wordt een regel gemaakt voor poort 80. HTTP-verkeer ontvangt bij Hallo load balancer is gerouteerde tooport 80 een Hallo VM's in Hallo load balancer-set. |
| [AZ netwerk lb frontend-IP-maken](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | Maak een frontend-IP-adres voor Hallo Load Balancer. |
| [AZ netwerk lb-adresgroep maken](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | Maakt een back-end-adresgroep. |
| [AZ netwerk nic maken](https://docs.microsoft.com/cli/azure/network/nic#create) | Maakt een virtueel netwerkkaart en toohello virtueel netwerk en subnet gekoppeld. |
| [AZ vm beschikbaarheidsset maken](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Hiermee maakt een beschikbaarheidsset. Beschikbaarheidssets waarborgen uptime van toepassingen via Hallo virtuele machines verspreid over fysieke resources zo dat als fout optreedt, wordt de hele set Hallo niet gedaan. |
| [AZ netwerk nic ip-configuratie maken](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | Hiermee maakt u een IP-confiuration. U moet Hallo Microsoft.Network/AllowMultipleIpConfigurationsPerNic functie is ingeschakeld voor uw abonnement hebben. Hallo primaire IP-configuratie per NIC, met behulp van Hallo--primair maken vlag kan slechts één configuratie worden aangeduid. |
| [AZ vm maken](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden. Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.  |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende netwerken CLI scriptvoorbeelden kunnen u vinden in Hallo [overzicht van Azure-netwerken documentatie](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
