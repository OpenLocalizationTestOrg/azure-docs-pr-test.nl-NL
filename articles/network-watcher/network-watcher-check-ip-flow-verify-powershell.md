---
title: Controleer aaaverify verkeer met Azure-netwerk-Watcher IP-flow - PowerShell | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocheck als tooor van een virtuele machine verkeer wordt toegestaan of geweigerd met behulp van PowerShell
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Controleer of het verkeer wordt toegestaan of geweigerd tooor van een virtuele machine met IP-stroom controleren of een onderdeel van Azure-netwerk-Watcher

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST-API](network-watcher-check-ip-flow-verify-rest.md)


IP-stroom controleren is een functie van netwerk-Watcher waarmee u tooverify als verkeer wordt toegestaan tooor van een virtuele machine. Dit scenario is nuttig tooget een huidige status van of een virtuele machine tooan externe bron- of back-end praten kunt. IP-stroom controleren gebruikte tooverify is als uw regels Netwerkbeveiligingsgroep (NSG) juist zijn geconfigureerd en oplossen van stromen die worden geblokkeerd door het NSG-regels. Een andere reden voor het gebruik van IP-stroom controleren die u blokkeren wilt tooensure-verkeer wordt geblokkeerd goed door Hallo NSG.

## <a name="before-you-begin"></a>Voordat u begint

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher of een bestaand exemplaar van netwerk-Watcher hebben. Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.

## <a name="scenario"></a>Scenario

Dit scenario maakt gebruik van IP-stroom tooverify verifiëren als een virtuele machine kunt praten tooa bekende Bing IP-adres. Als het Hallo-verkeer wordt geweigerd, wordt Hallo beveiligingsregel die dat verkeer wordt geweigerd. toolearn meer over IP-stroom controleren, gaat u naar [IP-stroom overzicht controleren](network-watcher-ip-flow-verify-overview.md)

## <a name="retrieve-network-watcher"></a>Ophalen van netwerk-Watcher

de eerste stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar. Hallo `$networkWatcher` variabele is doorgegeven toohello IP stroom cmdlet controleren.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Een virtuele machine ophalen

IP-stroom controleren tests verkeer tooor van een IP-adres op een virtuele machine tooor vanaf een externe bestemming. Een Id van een virtuele machine is vereist voor het Hallo-cmdlet. Als u al Hallo-ID van virtuele machine-toouse hello weet, kunt u deze stap overslaan.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a>Hallo NIC's ophalen

Hallo IP-adres van een NIC op Hallo virtuele machine is vereist, in dit voorbeeld Hallo NIC's op een virtuele machine worden opgehaald. Als u weet al Hallo IP adres die u wilt dat tootest op Hallo virtuele machine, kunt u deze stap overslaan.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a>Voer IP-stroom controleren

Nu dat we Hallo informatie nodig toorun Hallo cmdlet hebben, voeren we Hallo `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest Hallo verkeer. In dit voorbeeld gebruiken we Hallo eerste IP-adres op Hallo eerste NIC.

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> IP-stroom controleren vereist dat de VM-resource Hallo toorun wordt toegewezen.

## <a name="review-results"></a>Resultaten bekijken

Nadat u `Test-AzureRmNetworkWatcherIPFlow` Hallo resultaten worden geretourneerd, hello volgende voorbeeld is Hallo resultaten geretourneerd door de voorgaande stap Hallo.

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a>Volgende stappen

Zie als verkeer wordt geblokkeerd en mag geen [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die zijn gedefinieerd.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













