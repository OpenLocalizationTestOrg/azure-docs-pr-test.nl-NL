---
title: aaaManage pakket worden vastgelegd met Azure-netwerk-Watcher - REST-API | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toomanage Hallo pakket vastleggen functie van netwerk-Watcher met Azure REST API
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 53fe0324-835f-4005-afc8-145eeb314aeb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7a531fbe796e85e94961bd192d171defb299be05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="10810-103">Pakket opnamen beheren met Azure met Azure REST API netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="10810-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="10810-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="10810-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="10810-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="10810-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="10810-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="10810-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="10810-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="10810-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="10810-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="10810-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="10810-109">Netwerk-Watcher pakketopname kunt u toocreate vastleggen sessies tootrack verkeer tooand van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="10810-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="10810-110">Filters zijn beschikbaar voor Hallo vastleggen sessie tooensure dat u alleen Hallo verkeer die u wilt vastleggen.</span><span class="sxs-lookup"><span data-stu-id="10810-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="10810-111">Pakketopname helpt toodiagnose netwerk afwijkingen reactief en proactief.</span><span class="sxs-lookup"><span data-stu-id="10810-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="10810-112">Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's, toodebug client / server-communicatie en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="10810-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="10810-113">Deze mogelijkheid vergemakkelijkt door kunnen tooremotely trigger pakket opnamen, Hallo last van een pakketopname handmatig en op de gewenste machine hello, die kostbare tijd bespaart worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10810-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="10810-114">In dit artikel leert u Hallo verschillende beheertaken uitvoeren die momenteel beschikbaar zijn voor pakketopname.</span><span class="sxs-lookup"><span data-stu-id="10810-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="10810-115">**Ophalen van een pakketopname**</span><span class="sxs-lookup"><span data-stu-id="10810-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="10810-116">**Lijst van alle pakket-opnamen**</span><span class="sxs-lookup"><span data-stu-id="10810-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="10810-117">**Hallo-status van een pakketopname opvragen**</span><span class="sxs-lookup"><span data-stu-id="10810-117">**Query hello status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="10810-118">**Start een pakketopname**</span><span class="sxs-lookup"><span data-stu-id="10810-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="10810-119">**Stop de pakketopname van een**</span><span class="sxs-lookup"><span data-stu-id="10810-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="10810-120">**Het vastleggen van een pakket verwijderen**</span><span class="sxs-lookup"><span data-stu-id="10810-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="10810-121">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="10810-121">Before you begin</span></span>

<span data-ttu-id="10810-122">In dit scenario moet u Hallo Rest-API voor netwerk-Watcher toorun IP-stromen controleren aanroepen.</span><span class="sxs-lookup"><span data-stu-id="10810-122">In this scenario, you call hello Network Watcher Rest API toorun IP Flow Verify.</span></span> <span data-ttu-id="10810-123">ARMclient is gebruikte toocall Hallo REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10810-123">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="10810-124">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="10810-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="10810-125">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="10810-125">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> <span data-ttu-id="10810-126">Pakketopname vereist dat de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="10810-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="10810-127">Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="10810-127">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="10810-128">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="10810-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="10810-129">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="10810-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="10810-130">Hallo script tooreturn na een virtuele machine uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="10810-130">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="10810-131">Deze informatie is nodig voor het starten van een pakketopname.</span><span class="sxs-lookup"><span data-stu-id="10810-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="10810-132">Hallo moet volgende code variabelen:</span><span class="sxs-lookup"><span data-stu-id="10810-132">hello following code needs variables:</span></span>

- <span data-ttu-id="10810-133">**subscriptionId** -Hallo abonnements-id kan ook worden opgehaald met Hallo **Get-AzureRMSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10810-133">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="10810-134">**resourceGroupName** - hello naam van een resourcegroep die virtuele machines bevatten.</span><span class="sxs-lookup"><span data-stu-id="10810-134">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="10810-135">Hallo-id van Hallo virtuele machine wordt van de volgende Hallo uitvoer, in het volgende voorbeeld Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="10810-135">From hello following output, hello id of hello virtual machine is used in hello next example.</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```


## <a name="get-a-packet-capture"></a><span data-ttu-id="10810-136">Ophalen van een pakketopname</span><span class="sxs-lookup"><span data-stu-id="10810-136">Get a packet capture</span></span>

<span data-ttu-id="10810-137">Hallo volgende voorbeeld wordt opgehaald Hallo status van een enkele pakketopname</span><span class="sxs-lookup"><span data-stu-id="10810-137">hello following example gets hello status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="10810-138">Hallo zijn volgende antwoorden voorbeelden van een typische antwoord geretourneerd bij het Hallo-status van een pakketopname opvragen.</span><span class="sxs-lookup"><span data-stu-id="10810-138">hello following responses are examples of a typical response returned when querying hello status of a packet capture.</span></span>

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Running",
  "packetCaptureError": []
}
```

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Stopped",
  "stopReason": "TimeExceeded",
  "packetCaptureError": []
}
```

## <a name="list-all-packet-captures"></a><span data-ttu-id="10810-139">Lijst van alle pakket-opnamen</span><span class="sxs-lookup"><span data-stu-id="10810-139">List all packet captures</span></span>

<span data-ttu-id="10810-140">Hallo volgt haalt alle sessies van pakket vastleggen in een regio.</span><span class="sxs-lookup"><span data-stu-id="10810-140">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="10810-141">Hallo is volgende antwoord een voorbeeld van een typische antwoord geretourneerd tijdens het ophalen van alle pakketten worden vastgelegd</span><span class="sxs-lookup"><span data-stu-id="10810-141">hello following response is an example of a typical response returned when getting all packet captures</span></span>

```json
{
  "value": [
    {
      "name": "TestPacketCapture6",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Succeeded",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_19_53_056.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    },
    {
      "name": "TestPacketCapture7",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture7",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Failed",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_23_15_364.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    }
  ]
}
```

## <a name="query-packet-capture-status"></a><span data-ttu-id="10810-142">Status van pakket vastleggen</span><span class="sxs-lookup"><span data-stu-id="10810-142">Query packet capture status</span></span>

<span data-ttu-id="10810-143">Hallo volgt haalt alle sessies van pakket vastleggen in een regio.</span><span class="sxs-lookup"><span data-stu-id="10810-143">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="10810-144">Hallo is volgende antwoord een voorbeeld van een typische antwoord geretourneerd bij het Hallo-status van een pakketopname opvragen.</span><span class="sxs-lookup"><span data-stu-id="10810-144">hello following response is an example of a typical response returned when querying hello status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="10810-145">Start pakketopname</span><span class="sxs-lookup"><span data-stu-id="10810-145">Start packet capture</span></span>

<span data-ttu-id="10810-146">Hallo volgende voorbeeld maakt een pakketopname op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="10810-146">hello following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="10810-147">Hallo-voorbeeld is geparameteriseerd tooallow voor flexibiliteit bij het maken van een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="10810-147">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
$storageaccountname = "contosoexamplergdiag374"
$vmName = "ContosoVM"
$bytestoCaptureperPacket = "0"
$bytesPerSession = "1073741824"
$captureTimeinSeconds = "60"
$localIP = ""
$localPort = "" # Examples are: 80, or 80-120
$remoteIP = ""
$remotePort = "" # Examples are: 80, or 80-120
$protocol = "" # Valid values are TCP, UDP and Any.
$targetUri = "" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName
$storageId = "" # Example: "https://mytestaccountname.blob.core.windows.net/capture/vm1Capture.cap"
$storagePath = ""
$localFilePath = "c:\\temp\\packetcapture.cap" # Example: "d:\capture\vm1Capture.cap"

$requestBody = @"
{
    'properties':  {
                       'target':  '/${targetUri}',
                       'bytesToCapturePerPacket':  '${bytestoCaptureperPacket}',
                       'totalBytesPerSession':  '${bytesPerSession}',
                       'timeLimitinSeconds':  '${captureTimeinSeconds}',
                       'storageLocation':  {
                                               'storageId':  '${storageId}',
                                               'storagePath':  '${storagePath}',
                                               'filePath':  '${localFilePath}'
                                           },
                       'filters':  [
                                       {
                                           'protocol':  '${protocol}',
                                           'localIPAddress':  '${localIP}',
                                           'localPort':  '${localPort}',
                                           'remoteIPAddress':  '${remoteIP}',
                                           'remotePort':  '${remotePort}'
                                       }
                                   ]
                   }
}
"@

armclient PUT "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-07-01" $requestbody
```

## <a name="stop-packet-capture"></a><span data-ttu-id="10810-148">Stop de pakketopname</span><span class="sxs-lookup"><span data-stu-id="10810-148">Stop packet capture</span></span>

<span data-ttu-id="10810-149">Hallo volgende voorbeeld wordt een pakketopname gestopt op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="10810-149">hello following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="10810-150">Hallo-voorbeeld is geparameteriseerd tooallow voor flexibiliteit bij het maken van een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="10810-150">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="10810-151">Pakketopname verwijderen</span><span class="sxs-lookup"><span data-stu-id="10810-151">Delete packet capture</span></span>

<span data-ttu-id="10810-152">Hallo volgende voorbeeld wordt een pakketopname op een virtuele machine verwijderd.</span><span class="sxs-lookup"><span data-stu-id="10810-152">hello following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="10810-153">Hallo-voorbeeld is geparameteriseerd tooallow voor flexibiliteit bij het maken van een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="10810-153">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="10810-154">Verwijderen van een pakketopname verwijderen Hallo-bestand in Hallo storage-account niet</span><span class="sxs-lookup"><span data-stu-id="10810-154">Deleting a packet capture does not delete hello file in hello storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="10810-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="10810-155">Next steps</span></span>

<span data-ttu-id="10810-156">Voor instructies over het downloaden van bestanden van azure storage-accounts, Raadpleeg te[aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="10810-156">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="10810-157">Een ander hulpprogramma dat kan worden gebruikt, is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="10810-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="10810-158">Meer informatie over Opslagverkenner vindt u hier op Hallo koppeling: [Opslagverkenner](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="10810-158">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="10810-159">Meer informatie over hoe tooautomate pakket worden vastgelegd met waarschuwingen van de virtuele machine door [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="10810-159">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













