---
title: Beheren van opnamen van pakket met de Azure-netwerk-Watcher - REST-API | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe u de functie voor het vastleggen van pakket van netwerk-Watcher met Azure REST API beheren
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
ms.openlocfilehash: 49ec20802a252258d8493eb26510270b925e851a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="0205a-103">Pakket opnamen beheren met Azure met Azure REST API netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="0205a-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="0205a-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0205a-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="0205a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0205a-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="0205a-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0205a-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="0205a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0205a-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="0205a-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="0205a-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="0205a-109">Netwerk-Watcher pakketopname kunt u om sessies vastleggen om bij te houden van verkeer van en naar een virtuele machine te maken.</span><span class="sxs-lookup"><span data-stu-id="0205a-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="0205a-110">Filters zijn beschikbaar voor de opnamesessie om te controleren of dat u alleen het verkeer die u wilt vastleggen.</span><span class="sxs-lookup"><span data-stu-id="0205a-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="0205a-111">Pakketopname helpt op te sporen netwerk afwijkingen reactief en proactief.</span><span class="sxs-lookup"><span data-stu-id="0205a-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="0205a-112">Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's voor foutopsporing van client-servercommunicaties en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="0205a-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="0205a-113">Door op afstand activeren pakket opnamen, deze mogelijkheid kan vergemakkelijken de last van een pakketopname handmatig en op de gewenste machine, die kostbare tijd bespaart worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0205a-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="0205a-114">In dit artikel leert u de verschillende beheertaken die momenteel beschikbaar voor pakketopname zijn.</span><span class="sxs-lookup"><span data-stu-id="0205a-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="0205a-115">**Ophalen van een pakketopname**</span><span class="sxs-lookup"><span data-stu-id="0205a-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="0205a-116">**Lijst van alle pakket-opnamen**</span><span class="sxs-lookup"><span data-stu-id="0205a-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="0205a-117">**De status van een pakketopname opvragen**</span><span class="sxs-lookup"><span data-stu-id="0205a-117">**Query the status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="0205a-118">**Start een pakketopname**</span><span class="sxs-lookup"><span data-stu-id="0205a-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="0205a-119">**Stop de pakketopname van een**</span><span class="sxs-lookup"><span data-stu-id="0205a-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="0205a-120">**Het vastleggen van een pakket verwijderen**</span><span class="sxs-lookup"><span data-stu-id="0205a-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="0205a-121">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="0205a-121">Before you begin</span></span>

<span data-ttu-id="0205a-122">In dit scenario moet u de netwerk-Watcher Rest-API om te worden uitgevoerd met het IP-stromen controleren aanroepen.</span><span class="sxs-lookup"><span data-stu-id="0205a-122">In this scenario, you call the Network Watcher Rest API to run IP Flow Verify.</span></span> <span data-ttu-id="0205a-123">ARMclient wordt gebruikt voor het aanroepen van de REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0205a-123">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="0205a-124">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="0205a-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="0205a-125">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="0205a-125">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> <span data-ttu-id="0205a-126">Pakketopname vereist dat de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="0205a-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="0205a-127">Voor het installeren van de extensie op een Windows-virtuele machine gaat u naar [extensie voor het virtuele machine voor Windows Azure-netwerk-Watcher Agent](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="0205a-127">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="0205a-128">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="0205a-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="0205a-129">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="0205a-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="0205a-130">Voer het volgende script om te retourneren van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0205a-130">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="0205a-131">Deze informatie is nodig voor het starten van een pakketopname.</span><span class="sxs-lookup"><span data-stu-id="0205a-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="0205a-132">De volgende code moet variabelen:</span><span class="sxs-lookup"><span data-stu-id="0205a-132">The following code needs variables:</span></span>

- <span data-ttu-id="0205a-133">**subscriptionId** -de abonnements-id kan ook worden opgehaald met de **Get-AzureRMSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0205a-133">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="0205a-134">**resourceGroupName** -de naam van een resourcegroep die virtuele machines bevatten.</span><span class="sxs-lookup"><span data-stu-id="0205a-134">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="0205a-135">De id van de virtuele machine wordt gebruikt van de volgende uitvoer in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0205a-135">From the following output, the id of the virtual machine is used in the next example.</span></span>

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


## <a name="get-a-packet-capture"></a><span data-ttu-id="0205a-136">Ophalen van een pakketopname</span><span class="sxs-lookup"><span data-stu-id="0205a-136">Get a packet capture</span></span>

<span data-ttu-id="0205a-137">Het volgende voorbeeld wordt de status van een enkele pakketopname</span><span class="sxs-lookup"><span data-stu-id="0205a-137">The following example gets the status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="0205a-138">De volgende antwoorden zijn voorbeelden van een typische antwoord geretourneerd bij het opvragen van de status van een pakketopname.</span><span class="sxs-lookup"><span data-stu-id="0205a-138">The following responses are examples of a typical response returned when querying the status of a packet capture.</span></span>

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

## <a name="list-all-packet-captures"></a><span data-ttu-id="0205a-139">Lijst van alle pakket-opnamen</span><span class="sxs-lookup"><span data-stu-id="0205a-139">List all packet captures</span></span>

<span data-ttu-id="0205a-140">Het volgende voorbeeld wordt alle sessies van pakket vastleggen in een regio.</span><span class="sxs-lookup"><span data-stu-id="0205a-140">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="0205a-141">Het antwoord van de volgende is een voorbeeld van een typische antwoord geretourneerd tijdens het ophalen van alle pakketten worden vastgelegd</span><span class="sxs-lookup"><span data-stu-id="0205a-141">The following response is an example of a typical response returned when getting all packet captures</span></span>

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

## <a name="query-packet-capture-status"></a><span data-ttu-id="0205a-142">Status van pakket vastleggen</span><span class="sxs-lookup"><span data-stu-id="0205a-142">Query packet capture status</span></span>

<span data-ttu-id="0205a-143">Het volgende voorbeeld wordt alle sessies van pakket vastleggen in een regio.</span><span class="sxs-lookup"><span data-stu-id="0205a-143">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="0205a-144">Het volgende antwoord is een voorbeeld van een typische antwoord geretourneerd bij het opvragen van de status van een pakketopname.</span><span class="sxs-lookup"><span data-stu-id="0205a-144">The following response is an example of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="0205a-145">Start pakketopname</span><span class="sxs-lookup"><span data-stu-id="0205a-145">Start packet capture</span></span>

<span data-ttu-id="0205a-146">Het volgende voorbeeld wordt een pakketopname op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0205a-146">The following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="0205a-147">In het voorbeeld met parameters om toe te staan voor flexibiliteit bij het maken van een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0205a-147">The example is parameterized to allow for flexibility in creating an example.</span></span>

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

## <a name="stop-packet-capture"></a><span data-ttu-id="0205a-148">Stop de pakketopname</span><span class="sxs-lookup"><span data-stu-id="0205a-148">Stop packet capture</span></span>

<span data-ttu-id="0205a-149">Het volgende voorbeeld wordt een pakketopname gestopt op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0205a-149">The following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="0205a-150">In het voorbeeld met parameters om toe te staan voor flexibiliteit bij het maken van een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0205a-150">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="0205a-151">Pakketopname verwijderen</span><span class="sxs-lookup"><span data-stu-id="0205a-151">Delete packet capture</span></span>

<span data-ttu-id="0205a-152">Het volgende voorbeeld wordt een pakketopname op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0205a-152">The following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="0205a-153">In het voorbeeld met parameters om toe te staan voor flexibiliteit bij het maken van een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0205a-153">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="0205a-154">Verwijderen van een pakketopname, wordt het bestand in het opslagaccount niet verwijderd</span><span class="sxs-lookup"><span data-stu-id="0205a-154">Deleting a packet capture does not delete the file in the storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="0205a-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0205a-155">Next steps</span></span>

<span data-ttu-id="0205a-156">Zie voor instructies over het downloaden van bestanden van azure storage-accounts, [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="0205a-156">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="0205a-157">Een ander hulpprogramma dat kan worden gebruikt, is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="0205a-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="0205a-158">Meer informatie over Opslagverkenner vindt u hier op de volgende koppeling: [Opslagverkenner](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="0205a-158">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="0205a-159">Meer informatie over het automatiseren van pakket opnamen met waarschuwingen van de virtuele machine met weer te geven [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="0205a-159">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













