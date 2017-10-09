---
title: aaaManage pakket worden vastgelegd met Azure-netwerk-Watcher - PowerShell | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe de functie van netwerk-Watcher met behulp van PowerShell voor het vastleggen van toomanage hello-pakket
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77a522a1b05e020a73ba7140c1410615eb8761da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a>Pakket opnamen beheren met Azure met behulp van PowerShell netwerk-Watcher

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST-API](network-watcher-packet-capture-manage-rest.md)

Netwerk-Watcher pakketopname kunt u toocreate vastleggen sessies tootrack verkeer tooand van een virtuele machine. Filters zijn beschikbaar voor Hallo vastleggen sessie tooensure dat u alleen Hallo verkeer die u wilt vastleggen. Pakketopname helpt toodiagnose netwerk afwijkingen reactief en proactief. Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's, toodebug client / server-communicatie en nog veel meer. Deze mogelijkheid vergemakkelijkt door kunnen tooremotely trigger pakket opnamen, Hallo last van een pakketopname handmatig en op de gewenste machine hello, die kostbare tijd bespaart worden uitgevoerd.

In dit artikel leert u Hallo verschillende beheertaken uitvoeren die momenteel beschikbaar zijn voor pakketopname.

- [**Start een pakketopname**](#start-a-packet-capture)
- [**Stop de pakketopname van een**](#stop-a-packet-capture)
- [**Het vastleggen van een pakket verwijderen**](#delete-a-packet-capture)
- [**Een pakketopname downloaden**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Voordat u begint

In dit artikel wordt ervan uitgegaan dat er Hallo resources te volgen:

* Een exemplaar van netwerk-Watcher in Hallo regio die u wilt een pakketopname toocreate

* Een virtuele machine met hello-pakket vastleggen uitbreiding ingeschakeld.

> [!IMPORTANT]
> Pakketopname vereist dat de extensie van een virtuele machine `AzureNetworkWatcherExtension`. Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="install-vm-extension"></a>VM-extensie installeren

### <a name="step-1"></a>Stap 1

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a>Stap 2

Hallo volgende voorbeeld haalt Hallo extensiegegevens nodig toorun hello `Set-AzureRmVMExtension` cmdlet. Deze cmdlet wordt Hallo pakket vastleggen agent geïnstalleerd op de virtuele gastmachine Hallo.

> [!NOTE]
> Hallo `Set-AzureRmVMExtension` cmdlet toocomplete van enkele minuten kan duren.

Voor Windows virtuele machines:

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

Voor virtuele Linux-machines:

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

Hallo volgende voorbeeld is een geslaagde reactie na het uitvoeren van Hallo `Set-AzureRmVMExtension` cmdlet.

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a>Stap 3

tooensure die Hallo agent is geïnstalleerd, voert u Hallo `Get-AzureRmVMExtension` cmdlet en geef dit Hallo naam virtuele machine en Hallo extensienaam.

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

Hallo volgende voorbeeld is een voorbeeld van antwoord Hallo wordt uitgevoerd`Get-AzureRmVMExtension`

```
ResourceGroupName       : testrg
VMName                  : testvm1
Name                    : AzureNetworkWatcherExtension
Location                : westcentralus
Etag                    : null
Publisher               : Microsoft.Azure.NetworkWatcher
ExtensionType           : NetworkWatcherAgentWindows
TypeHandlerVersion      : 1.4
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1/
                          extensions/AzureNetworkWatcherExtension
PublicSettings          : 
ProtectedSettings       : 
ProvisioningState       : Succeeded
Statuses                : 
SubStatuses             : 
AutoUpgradeMinorVersion : True
ForceUpdateTag          : 
```

## <a name="start-a-packet-capture"></a>Start een pakketopname

Zodra hello voorgaande stappen voltooid hebt, wordt Hallo pakket vastleggen agent is geïnstalleerd op Hallo virtuele machine.

### <a name="step-1"></a>Stap 1

de volgende stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar. Deze variabele wordt doorgegeven toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet in stap 4.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a>Stap 2

Een opslagaccount ophalen. Dit opslagaccount is gebruikte toostore Hallo pakket vastleggen bestand.

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a>Stap 3

Filters kunnen gebruikte toolimit Hallo gegevens die zijn opgeslagen door Hallo pakketopname zijn. Hallo volgende voorbeeld wordt een twee filters.  Een filter verzamelt uitgaande TCP-verkeer alleen van het lokale IP 10.0.0.3 toodestination poorten 20, 80 en 443.  de tweede filter Hallo verzamelt UDP-verkeer.

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> Meerdere filters kunnen worden gedefinieerd voor het vastleggen van een pakket.

### <a name="step-4"></a>Stap 4

Voer Hallo `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart Hallo pakket vastleggen, Hallo vereiste waarden in de vorige stappen Hallo opgehaald wordt doorgegeven.
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

Hallo volgende voorbeeld is de Hallo verwacht uitvoer Hallo uitgevoerd `New-AzureRmNetworkWatcherPacketCapture` cmdlet.

```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"3bf27278-8251-4651-9546-c7f369855e4e"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]


```

## <a name="get-a-packet-capture"></a>Ophalen van een pakketopname

Hallo uitgevoerd `Get-AzureRmNetworkWatcherPacketCapture` -cmdlet haalt Hallo status van een pakketopname momenteel wordt uitgevoerd of voltooid is.

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

Hallo volgende voorbeeld is Hallo-uitvoer van Hallo `Get-AzureRmNetworkWatcherPacketCapture` cmdlet. Hallo wordt volgende voorbeeld nadat Hallo vastleggen voltooid is. Hallo PacketCaptureStatus waarde is met een StopReason TimeExceeded gestopt. Deze waarde geeft aan dat Hallo pakketopname voltooid is en de tijd wordt uitgevoerd.
```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"4b9a81ed-dc63-472e-869e-96d7166ccb9b"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]
CaptureStartTime        : 2/1/2017 10:43:01 PM
PacketCaptureStatus     : Stopped
StopReason              : TimeExceeded
PacketCaptureError      : []
```

## <a name="stop-a-packet-capture"></a>Stop de pakketopname van een

Door het uitvoeren van Hallo `Stop-AzureRmNetworkWatcherPacketCapture` als een opnamesessie Bezig het is-cmdlet is gestopt.

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> Hallo cmdlet retourneert geen antwoord wanneer uitgevoerd op een actieve opnamesessie of een bestaande sessie die al is gestopt.

## <a name="delete-a-packet-capture"></a>Het vastleggen van een pakket verwijderen

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
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

Als bepaalde verkeer is toegestaan in orr buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->














