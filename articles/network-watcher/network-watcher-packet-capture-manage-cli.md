---
title: aaaManage pakket worden vastgelegd met Azure-netwerk-Watcher - Azure CLI 2.0 | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toomanage Hallo functie voor het vastleggen van netwerk-Watcher met Azure CLI 2.0 pakket
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
ms.openlocfilehash: d19cb7d0ca3b7a9bc0546859e07ef6d4df4f42d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a>Pakket opnamen beheren met Azure met Azure CLI 2.0 netwerk-Watcher

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST-API](network-watcher-packet-capture-manage-rest.md)

Netwerk-Watcher pakketopname kunt u toocreate vastleggen sessies tootrack verkeer tooand van een virtuele machine. Filters zijn beschikbaar voor Hallo vastleggen sessie tooensure dat u alleen Hallo verkeer die u wilt vastleggen. Pakketopname helpt toodiagnose netwerk afwijkingen reactief en proactief. Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's, toodebug client / server-communicatie en nog veel meer. Deze mogelijkheid vergemakkelijkt door kunnen tooremotely trigger pakket opnamen, Hallo last van een pakketopname handmatig en op de gewenste machine hello, die kostbare tijd bespaart worden uitgevoerd.

In dit artikel gebruikt de volgende generatie CLI voor Hallo resource management-implementatiemodel, Azure CLI 2.0, die beschikbaar is voor Windows, Mac en Linux.

tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

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

Voer Hallo `az vm extension set` cmdlet tooinstall Hallo pakket vastleggen agent op de virtuele gastmachine Hallo.

Voor Windows virtuele machines:

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

Voor virtuele Linux-machines:

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a>Stap 2

tooensure die Hallo agent is geïnstalleerd, voert u Hallo `vm extension get` cmdlet en geef dit Hallo-resourcegroep en de naam van de virtuele machine. Controleer Hallo resulterende lijst tooensure Hallo agent is geïnstalleerd.

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

Hallo volgende voorbeeld is een voorbeeld van antwoord Hallo wordt uitgevoerd`az vm extension show`

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a>Start een pakketopname

Zodra hello voorgaande stappen voltooid hebt, wordt Hallo pakket vastleggen agent is geïnstalleerd op Hallo virtuele machine.

### <a name="step-1"></a>Stap 1

de volgende stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar. De naam van de Tkan Hallo netwerk-Watcher wordt doorgegeven toohello `az network watcher show` cmdlet in stap 4.

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a>Stap 2

Een opslagaccount ophalen. Dit opslagaccount is gebruikte toostore Hallo pakket vastleggen bestand.

```azurecli
azure storage account list
```

### <a name="step-3"></a>Stap 3

Filters kunnen gebruikte toolimit Hallo gegevens die zijn opgeslagen door Hallo pakketopname zijn. Hallo stelt volgende voorbeeld een pakketopname met verschillende filters.  Hallo eerste drie filters verzamelen uitgaande TCP-verkeer alleen van het lokale IP 10.0.0.3 toodestination poorten 20, 80 en 443.  de laatste filter Hallo verzamelt UDP-verkeer.

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

Hallo volgende voorbeeld is de Hallo verwacht uitvoer Hallo uitgevoerd `az network watcher packet-capture create` cmdlet.

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a>Ophalen van een pakketopname

Hallo uitgevoerd `az network watcher packet-capture show` -cmdlet haalt Hallo status van een pakketopname momenteel wordt uitgevoerd of voltooid is.

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

Hallo volgende voorbeeld is Hallo-uitvoer van Hallo `az network watcher packet-capture show` cmdlet. Hallo wordt volgende voorbeeld nadat Hallo vastleggen voltooid is. Hallo PacketCaptureStatus waarde is met een StopReason TimeExceeded gestopt. Deze waarde geeft aan dat Hallo pakketopname voltooid is en de tijd wordt uitgevoerd.

```
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/providers/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapt
ure_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="stop-a-packet-capture"></a>Stop de pakketopname van een

Door het uitvoeren van Hallo `az network watcher packet-capture stop` als een opnamesessie Bezig het is-cmdlet is gestopt.

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> Hallo cmdlet retourneert geen antwoord wanneer uitgevoerd op een actieve opnamesessie of een bestaande sessie die al is gestopt.

## <a name="delete-a-packet-capture"></a>Het vastleggen van een pakket verwijderen

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
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
