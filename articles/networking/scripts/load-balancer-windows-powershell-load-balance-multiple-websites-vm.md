---
title: aaaAzure PowerShell-voorbeeldscript - taakverdeling toe te passen meerdere websites met Azure PowerShell | Microsoft Docs
description: Azure PowerShell-voorbeeldscript - taakverdeling toe te passen meerdere websites toohello dezelfde virtuele machine
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 316818964eb6928fe4163ef69eb7f05da2dc9636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Taakverdeling maken voor meerdere websites

Dit voorbeeldscript wordt een virtueel netwerk maakt met twee virtuele machines (VM) die lid van een beschikbaarheidsset zijn. Een load balancer stuurt verkeer voor twee afzonderlijke IP-adressen toohello twee virtuele machines. Na het Hallo-script wordt uitgevoerd, kan u web server software toohello virtuele machines implementeren en hosten van meerdere websites, elk met een eigen IP-adres.

Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep of virtueel netwerk, load balancer en alle gerelateerde resources te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Nieuwe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [Nieuwe AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) | Hiermee maakt u een Azure beschikbaarheid set tooprovide hoge beschikbaarheid. |
| [Nieuwe AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Hiermee maakt u de subnetconfiguratie van een. Deze configuratie wordt gebruikt met Hallo-proces voor het maken van virtuele netwerk. |
| [Nieuwe-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Hiermee maakt u een virtueel netwerk. |
| [Nieuwe AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Hiermee maakt u een openbaar IP-adres. |
| [Nieuwe AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | Maakt een front-end-IP-configuratie voor een load balancer. |
| [Nieuwe AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | Maakt een back-end-pool-adresconfiguratie voor een load balancer. |
| [Nieuwe AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | Maakt een NLB-test. Een NLB-test gebruikte toomonitor elke virtuele machine in Hallo NLB set is. Als een virtuele machine niet meer toegankelijk is, wordt verkeer is geen gerouteerde toohello VM. |
| [Nieuwe AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | Maakt een regel voor NLB. In dit voorbeeld wordt een regel gemaakt voor poort 80. Zoals HTTP-verkeer bij Hallo NLB aankomt, is het gerouteerde tooport 80 een Hallo VM's in Hallo NLB set. |
| [Nieuwe AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) | Hiermee maakt u een load balancer. |
| [Nieuwe AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | Hiermee definieert u geavanceerde functies voor de virtuele netwerkinterface. |
| [Nieuwe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Maakt een netwerkinterface. |
| [Nieuwe AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Maakt een VM-configuratie. Deze configuratie bevat informatie zoals de naam, het besturingssysteem en de beheerdersreferenties VM. Hallo-configuratie wordt gebruikt tijdens het maken van VM. |
| [Nieuwe-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Maak een virtuele machine. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Hiermee verwijdert u een resourcegroep en alle resources binnen. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Aanvullende voorbeelden voor netwerken PowerShell-script kunnen worden gevonden in Hallo [overzicht van Azure-netwerken documentatie](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
