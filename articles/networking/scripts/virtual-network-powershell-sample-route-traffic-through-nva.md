---
title: aaaAzure PowerShell-voorbeeldscript - routeverkeer via een virtueel netwerkapparaat | Microsoft Docs
description: 'Azure PowerShell - voorbeeldscript: de Route-verkeer via een firewall netwerk virtueel apparaat.'
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>-Routeverkeer via een virtueel netwerkapparaat

Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten. Een virtuele machine wordt gemaakt met ingeschakelde tooroute verkeer tussen de twee subnetten Hallo doorsturen via IP. U kunt na het uitvoeren van script Hallo netwerksoftware, zoals een firewalltoepassing toohello VM implementeren.

Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeld van een script


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate na een resourcegroep, het virtuele netwerk en netwerkbeveiligingsgroepen. Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Nieuwe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [Nieuwe-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Maakt een virtueel Azure-netwerk en de front-end-subnet. |
| [Nieuwe AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Maakt back-end en DMZ subnetten. |
| [Nieuwe AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Maakt een openbare IP-adres tooaccess-Hallo VM van Hallo Internet. |
| [Nieuwe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Maakt een virtuele netwerkinterface en doorsturen via IP inschakelen voor deze. |
| [Nieuwe AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Maakt een netwerkbeveiligingsgroep (NSG). |
| [Nieuwe AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | NSG-regels waarmee HTTP en HTTPS-poorten inkomend toohello VM maakt. |
| [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| Gekoppeld Hallo nsg's en route toosubnets tabellen. |
| [Nieuwe AzureRmRouteTable](/powershell/module/azurerm.network/new-azurermroutetable)| Een routetabel voor alle routes maken. |
| [Nieuwe AzureRMRouteConfig](/powershell/module/azurerm.network/new-azurermrouteconfig)| Routes maakt tooroute verkeer tussen subnetten en Hallo Internet via VM Hallo. |
| [Nieuwe-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Een virtuele machine maakt en koppelt Hallo NIC tooit. Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toouse en beheerdersreferenties. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | Hiermee verwijdert u een resourcegroep en alle resources die deze bevat. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Aanvullende voorbeelden voor netwerken PowerShell-script kunnen worden gevonden in Hallo [overzicht van Azure-netwerken documentatie](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
