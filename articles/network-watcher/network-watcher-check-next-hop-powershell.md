---
title: de volgende hop aaaFind met Azure-netwerk-Watcher volgende Hop - PowerShell | Microsoft Docs
description: In dit artikel wordt beschreven hoe u kunt zoeken welke Hallo type voor het volgende hop is en gebruik van IP-adres van volgende Hop met behulp van PowerShell.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a>Ontdek welke Hallo volgend hoptype Hallo volgende Hop mogelijkheid gebruikt in Azure met behulp van PowerShell netwerk-Watcher

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST-API](network-watcher-check-next-hop-rest.md)

De volgende hop is een functie van netwerk-Watcher die de mogelijkheid Hallo biedt Hallo volgend hoptype en IP-adres op basis van een opgegeven virtuele machine ophalen. Deze functie is handig bij het bepalen of een virtuele machine uitgaand verkeer van een gateway, internet of virtuele netwerken tooget tooits bestemming passeert.

## <a name="before-you-begin"></a>Voordat u begint

In dit scenario gebruikt u Azure portal toofind Hallo volgend hoptype hello en IP-adres.

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher. Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.

## <a name="scenario"></a>Scenario

Hallo scenario beschreven in dit artikel maakt gebruik van volgende Hop, een functie van netwerk-Watcher waarmee wordt gezocht naar het volgende hoptype hello en IP-adres voor een resource. toolearn meer informatie over het volgende Hop, gaat u naar [volgende Hop overzicht](network-watcher-next-hop-overview.md).

## <a name="retrieve-network-watcher"></a>Ophalen van netwerk-Watcher

de eerste stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar. Hallo `$networkWatcher` variabele is doorgegeven toohello volgende hop cmdlet controleren.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a>Een virtuele machine ophalen

Volgende hop retourneert de volgende hop Hallo en Hallo IP-adres van de volgende hop Hallo van een virtuele machine. Een Id van een virtuele machine is vereist voor het Hallo-cmdlet. Als u al Hallo-ID van virtuele machine-toouse hello weet, kunt u deze stap overslaan.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> Volgende hop is vereist dat de VM-resource Hallo toorun wordt toegewezen.

## <a name="get-hello-network-interfaces"></a>Hallo-netwerkinterfaces ophalen

Hallo IP-adres van een NIC op Hallo virtuele machine is vereist, in dit voorbeeld Hallo NIC's op een virtuele machine worden opgehaald. Als u weet al Hallo IP adres die u wilt dat tootest op Hallo virtuele machine, kunt u deze stap overslaan.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a>Ophalen van de volgende Hop

Nu we Hallo noemen `Get-AzureRmNetworkWatcherNextHop` cmdlet. Wij Hallo cmdlet Hallo netwerk-Watcher virtuele machine Id doorgeven, bron-IP-adres en IP-doeladres. In dit voorbeeld is de IP-doeladres Hallo tooa VM in een ander virtueel netwerk. Er is een virtuele netwerkgateway tussen Hallo twee virtuele netwerken.

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a>Resultaten bekijken

Als u klaar worden Hallo resultaten geleverd. Hallo volgende hop IP-adres wordt geretourneerd en Hallo type resource is. In dit scenario is het openbare IP-adres van de virtuele netwerkgateway Hallo Hallo.

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

Hallo bevat volgende lijst de momenteel beschikbare NextHopType waarden Hallo:

**Volgend Hoptype**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Geen

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooreview uw netwerk groep beveiligingsinstellingen programmatisch in via [NSG controleren met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md)

















