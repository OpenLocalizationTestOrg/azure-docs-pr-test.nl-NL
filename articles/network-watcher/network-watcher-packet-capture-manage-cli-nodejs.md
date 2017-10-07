---
title: aaaManage pakket worden vastgelegd met Azure-netwerk-Watcher - Azure CLI 1.0 | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toomanage Hallo functie voor het vastleggen van netwerk-Watcher met behulp van Azure CLI 1.0 pakket
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a>Pakket opnamen beheren met Azure met Azure CLI 1.0 netwerk-Watcher

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST-API](network-watcher-packet-capture-manage-rest.md)

Netwerk-Watcher pakketopname kunt u toocreate vastleggen sessies tootrack verkeer tooand van een virtuele machine. Filters zijn beschikbaar voor Hallo vastleggen sessie tooensure dat u alleen Hallo verkeer die u wilt vastleggen. Pakketopname helpt toodiagnose netwerk afwijkingen reactief en proactief. Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's, toodebug client / server-communicatie en nog veel meer. Deze mogelijkheid vergemakkelijkt door kunnen tooremotely trigger pakket opnamen, Hallo last van een pakketopname handmatig en op de gewenste machine hello, die kostbare tijd bespaart worden uitgevoerd.

Dit artikel wordt platformoverschrijdende Azure CLI 1.0 gebruikt die beschikbaar is voor Windows, Mac en Linux.

In dit artikel leert u Hallo verschillende beheertaken uitvoeren die momenteel beschikbaar zijn voor pakketopname.

- [**Start een pakketopname**](#start-a-packet-capture)
- [**Stop de pakketopname van een**](#stop-a-packet-capture)
- [**Het vastleggen van een pakket verwijderen**](#delete-a-packet-capture)
- [**Een pakketopname downloaden**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Voordat u begint

In dit artikel wordt ervan uitgegaan dat er Hallo resources te volgen:

- Een exemplaar van netwerk-Watcher in Hallo regio die u wilt een pakketopname toocreate
- Een virtuele machine met hello-pakket vastleggen uitbreiding ingeschakeld.

> [!IMPORTANT]
> Pakketopname vereist een agent toobe op Hallo virtuele machine. Hallo Agent wordt geïnstalleerd als een uitbreiding. Voor instructies voor het VM-extensies, gaat u naar [uitbreidingen van de virtuele Machine en functies](../virtual-machines/windows/extensions-features.md).

## <a name="install-vm-extension"></a>VM-extensie installeren

### <a name="step-1"></a>Stap 1

Voer Hallo `azure vm extension set` cmdlet tooinstall Hallo pakket vastleggen agent op de virtuele gastmachine Hallo.

Voor Windows virtuele machines:

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

Voor virtuele Linux-machines:

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a>Stap 2

tooensure die Hallo agent is geïnstalleerd, voert u Hallo `vm extension get` cmdlet en geef dit Hallo-resourcegroep en de naam van de virtuele machine. Controleer Hallo resulterende lijst tooensure Hallo agent is geïnstalleerd.

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

Hallo volgende voorbeeld is een voorbeeld van antwoord Hallo wordt uitgevoerd`azure vm extension get`

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a>Start een pakketopname

Zodra hello voorgaande stappen voltooid hebt, wordt Hallo pakket vastleggen agent is geïnstalleerd op Hallo virtuele machine.

### <a name="step-1"></a>Stap 1

de volgende stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar. Deze variabele wordt doorgegeven toohello `network watcher show` cmdlet in stap 4.

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a>Stap 2

Een opslagaccount ophalen. Dit opslagaccount is gebruikte toostore Hallo pakket vastleggen bestand.

```azurecli
azure storage account list
```

### <a name="step-3"></a>Stap 3

Filters kunnen gebruikte toolimit Hallo gegevens die zijn opgeslagen door Hallo pakketopname zijn. Hallo stelt volgende voorbeeld een pakketopname met verschillende filters.  Hallo eerste drie filters verzamelen uitgaande TCP-verkeer alleen van het lokale IP 10.0.0.3 toodestination poorten 20, 80 en 443.  de laatste filter Hallo verzamelt UDP-verkeer.

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

Meerdere filters kunnen worden gedefinieerd voor het vastleggen van een pakket. Als u van een complexe filter-structuur gebruikmaakt, is het beter toouse filters als een json-bestand tooavoid syntaxisfouten ontdekt. Hallo-vlag bijvoorbeeld gebruiken '-r ' (in plaats van '-f ') en doorgeven Hallo-locatie van een json-bestand met Hallo filters te volgen:

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


Hallo volgende voorbeeld is de Hallo verwacht uitvoer Hallo uitgevoerd `network watcher packet-capture create` cmdlet.

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a>Ophalen van een pakketopname

Hallo uitgevoerd `network watcher packet-capture show` -cmdlet haalt Hallo status van een pakketopname momenteel wordt uitgevoerd of voltooid is.

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

Hallo volgende voorbeeld is Hallo-uitvoer van Hallo `network watcher packet-capture show` cmdlet. Hallo wordt volgende voorbeeld nadat Hallo vastleggen voltooid is. Hallo PacketCaptureStatus waarde is met een StopReason TimeExceeded gestopt. Deze waarde geeft aan dat Hallo pakketopname voltooid is en de tijd wordt uitgevoerd.

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a>Stop de pakketopname van een

Door het uitvoeren van Hallo `network watcher packet-capture stop` als een opnamesessie Bezig het is-cmdlet is gestopt.

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> Hallo cmdlet retourneert geen antwoord wanneer uitgevoerd op een actieve opnamesessie of een bestaande sessie die al is gestopt.

## <a name="delete-a-packet-capture"></a>Het vastleggen van een pakket verwijderen

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> Als een pakketopname, verwijdert Hallo-bestand in Hallo storage-account niet verwijderd.

## <a name="download-a-packet-capture"></a>Een pakketopname downloaden

Zodra de sessie van uw pakket vastleggen is voltooid, kan Hallo vastleggen bestand geüploade tooblob opslag of tooa lokaal bestand op Hallo VM zijn. Hallo-opslaglocatie van Hallo pakketopname is gedefinieerd bij het maken van Hallo-sessie. Een handig hulpmiddel tooaccess deze bestanden vastleggen, opgeslagen tooa storage-account is Microsoft Azure Storage Explorer, die u kunt hier downloaden: http://storageexplorer.com/

Als een opslagaccount is opgegeven, worden bestanden voor pakket tooa storage-account op Hallo na locatie opgeslagen:

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooautomate pakket worden vastgelegd met waarschuwingen van de virtuele machine door [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)

Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
