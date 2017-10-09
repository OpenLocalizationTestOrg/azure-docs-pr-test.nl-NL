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
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="031e0-103">Pakket opnamen beheren met Azure met behulp van PowerShell netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="031e0-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="031e0-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="031e0-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="031e0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="031e0-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="031e0-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="031e0-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="031e0-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="031e0-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="031e0-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="031e0-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="031e0-109">Netwerk-Watcher pakketopname kunt u toocreate vastleggen sessies tootrack verkeer tooand van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="031e0-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="031e0-110">Filters zijn beschikbaar voor Hallo vastleggen sessie tooensure dat u alleen Hallo verkeer die u wilt vastleggen.</span><span class="sxs-lookup"><span data-stu-id="031e0-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="031e0-111">Pakketopname helpt toodiagnose netwerk afwijkingen reactief en proactief.</span><span class="sxs-lookup"><span data-stu-id="031e0-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="031e0-112">Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's, toodebug client / server-communicatie en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="031e0-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="031e0-113">Deze mogelijkheid vergemakkelijkt door kunnen tooremotely trigger pakket opnamen, Hallo last van een pakketopname handmatig en op de gewenste machine hello, die kostbare tijd bespaart worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="031e0-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="031e0-114">In dit artikel leert u Hallo verschillende beheertaken uitvoeren die momenteel beschikbaar zijn voor pakketopname.</span><span class="sxs-lookup"><span data-stu-id="031e0-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="031e0-115">**Start een pakketopname**</span><span class="sxs-lookup"><span data-stu-id="031e0-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="031e0-116">**Stop de pakketopname van een**</span><span class="sxs-lookup"><span data-stu-id="031e0-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="031e0-117">**Het vastleggen van een pakket verwijderen**</span><span class="sxs-lookup"><span data-stu-id="031e0-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="031e0-118">**Een pakketopname downloaden**</span><span class="sxs-lookup"><span data-stu-id="031e0-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="031e0-119">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="031e0-119">Before you begin</span></span>

<span data-ttu-id="031e0-120">In dit artikel wordt ervan uitgegaan dat er Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="031e0-120">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="031e0-121">Een exemplaar van netwerk-Watcher in Hallo regio die u wilt een pakketopname toocreate</span><span class="sxs-lookup"><span data-stu-id="031e0-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>

* <span data-ttu-id="031e0-122">Een virtuele machine met hello-pakket vastleggen uitbreiding ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="031e0-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="031e0-123">Pakketopname vereist dat de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="031e0-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="031e0-124">Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="031e0-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="031e0-125">VM-extensie installeren</span><span class="sxs-lookup"><span data-stu-id="031e0-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="031e0-126">Stap 1</span><span class="sxs-lookup"><span data-stu-id="031e0-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="031e0-127">Stap 2</span><span class="sxs-lookup"><span data-stu-id="031e0-127">Step 2</span></span>

<span data-ttu-id="031e0-128">Hallo volgende voorbeeld haalt Hallo extensiegegevens nodig toorun hello `Set-AzureRmVMExtension` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="031e0-128">hello following example retrieves hello extension information needed toorun hello `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="031e0-129">Deze cmdlet wordt Hallo pakket vastleggen agent geïnstalleerd op de virtuele gastmachine Hallo.</span><span class="sxs-lookup"><span data-stu-id="031e0-129">This cmdlet installs hello packet capture agent on hello guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="031e0-130">Hallo `Set-AzureRmVMExtension` cmdlet toocomplete van enkele minuten kan duren.</span><span class="sxs-lookup"><span data-stu-id="031e0-130">hello `Set-AzureRmVMExtension` cmdlet may take several minutes toocomplete.</span></span>

<span data-ttu-id="031e0-131">Voor Windows virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="031e0-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="031e0-132">Voor virtuele Linux-machines:</span><span class="sxs-lookup"><span data-stu-id="031e0-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="031e0-133">Hallo volgende voorbeeld is een geslaagde reactie na het uitvoeren van Hallo `Set-AzureRmVMExtension` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="031e0-133">hello following example is a successful response after running hello `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="031e0-134">Stap 3</span><span class="sxs-lookup"><span data-stu-id="031e0-134">Step 3</span></span>

<span data-ttu-id="031e0-135">tooensure die Hallo agent is geïnstalleerd, voert u Hallo `Get-AzureRmVMExtension` cmdlet en geef dit Hallo naam virtuele machine en Hallo extensienaam.</span><span class="sxs-lookup"><span data-stu-id="031e0-135">tooensure that hello agent is installed, run hello `Get-AzureRmVMExtension` cmdlet and pass it hello virtual machine name and hello extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="031e0-136">Hallo volgende voorbeeld is een voorbeeld van antwoord Hallo wordt uitgevoerd`Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="031e0-136">hello following sample is an example of hello response from running `Get-AzureRmVMExtension`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="031e0-137">Start een pakketopname</span><span class="sxs-lookup"><span data-stu-id="031e0-137">Start a packet capture</span></span>

<span data-ttu-id="031e0-138">Zodra hello voorgaande stappen voltooid hebt, wordt Hallo pakket vastleggen agent is geïnstalleerd op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="031e0-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="031e0-139">Stap 1</span><span class="sxs-lookup"><span data-stu-id="031e0-139">Step 1</span></span>

<span data-ttu-id="031e0-140">de volgende stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="031e0-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="031e0-141">Deze variabele wordt doorgegeven toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet in stap 4.</span><span class="sxs-lookup"><span data-stu-id="031e0-141">This variable is passed toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="031e0-142">Stap 2</span><span class="sxs-lookup"><span data-stu-id="031e0-142">Step 2</span></span>

<span data-ttu-id="031e0-143">Een opslagaccount ophalen.</span><span class="sxs-lookup"><span data-stu-id="031e0-143">Retrieve a storage account.</span></span> <span data-ttu-id="031e0-144">Dit opslagaccount is gebruikte toostore Hallo pakket vastleggen bestand.</span><span class="sxs-lookup"><span data-stu-id="031e0-144">This storage account is used toostore hello packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="031e0-145">Stap 3</span><span class="sxs-lookup"><span data-stu-id="031e0-145">Step 3</span></span>

<span data-ttu-id="031e0-146">Filters kunnen gebruikte toolimit Hallo gegevens die zijn opgeslagen door Hallo pakketopname zijn.</span><span class="sxs-lookup"><span data-stu-id="031e0-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="031e0-147">Hallo volgende voorbeeld wordt een twee filters.</span><span class="sxs-lookup"><span data-stu-id="031e0-147">hello following example sets up two filters.</span></span>  <span data-ttu-id="031e0-148">Een filter verzamelt uitgaande TCP-verkeer alleen van het lokale IP 10.0.0.3 toodestination poorten 20, 80 en 443.</span><span class="sxs-lookup"><span data-stu-id="031e0-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="031e0-149">de tweede filter Hallo verzamelt UDP-verkeer.</span><span class="sxs-lookup"><span data-stu-id="031e0-149">hello second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="031e0-150">Meerdere filters kunnen worden gedefinieerd voor het vastleggen van een pakket.</span><span class="sxs-lookup"><span data-stu-id="031e0-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="031e0-151">Stap 4</span><span class="sxs-lookup"><span data-stu-id="031e0-151">Step 4</span></span>

<span data-ttu-id="031e0-152">Voer Hallo `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart Hallo pakket vastleggen, Hallo vereiste waarden in de vorige stappen Hallo opgehaald wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="031e0-152">Run hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello packet capture process, passing hello required values retrieved in hello preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="031e0-153">Hallo volgende voorbeeld is de Hallo verwacht uitvoer Hallo uitgevoerd `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="031e0-153">hello following example is hello expected output from running hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="031e0-154">Ophalen van een pakketopname</span><span class="sxs-lookup"><span data-stu-id="031e0-154">Get a packet capture</span></span>

<span data-ttu-id="031e0-155">Hallo uitgevoerd `Get-AzureRmNetworkWatcherPacketCapture` -cmdlet haalt Hallo status van een pakketopname momenteel wordt uitgevoerd of voltooid is.</span><span class="sxs-lookup"><span data-stu-id="031e0-155">Running hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="031e0-156">Hallo volgende voorbeeld is Hallo-uitvoer van Hallo `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="031e0-156">hello following example is hello output from hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="031e0-157">Hallo wordt volgende voorbeeld nadat Hallo vastleggen voltooid is.</span><span class="sxs-lookup"><span data-stu-id="031e0-157">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="031e0-158">Hallo PacketCaptureStatus waarde is met een StopReason TimeExceeded gestopt.</span><span class="sxs-lookup"><span data-stu-id="031e0-158">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="031e0-159">Deze waarde geeft aan dat Hallo pakketopname voltooid is en de tijd wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="031e0-159">This value shows that hello packet capture was successful and ran its time.</span></span>
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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="031e0-160">Stop de pakketopname van een</span><span class="sxs-lookup"><span data-stu-id="031e0-160">Stop a packet capture</span></span>

<span data-ttu-id="031e0-161">Door het uitvoeren van Hallo `Stop-AzureRmNetworkWatcherPacketCapture` als een opnamesessie Bezig het is-cmdlet is gestopt.</span><span class="sxs-lookup"><span data-stu-id="031e0-161">By running hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="031e0-162">Hallo cmdlet retourneert geen antwoord wanneer uitgevoerd op een actieve opnamesessie of een bestaande sessie die al is gestopt.</span><span class="sxs-lookup"><span data-stu-id="031e0-162">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="031e0-163">Het vastleggen van een pakket verwijderen</span><span class="sxs-lookup"><span data-stu-id="031e0-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="031e0-164">Als een pakketopname, verwijdert Hallo-bestand in Hallo storage-account niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="031e0-164">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="031e0-165">Een pakketopname downloaden</span><span class="sxs-lookup"><span data-stu-id="031e0-165">Download a packet capture</span></span>

<span data-ttu-id="031e0-166">Zodra de sessie van uw pakket vastleggen is voltooid, kan Hallo vastleggen bestand geüploade tooblob opslag of tooa lokaal bestand op Hallo VM zijn.</span><span class="sxs-lookup"><span data-stu-id="031e0-166">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="031e0-167">Hallo-opslaglocatie van Hallo pakketopname is gedefinieerd bij het maken van Hallo-sessie.</span><span class="sxs-lookup"><span data-stu-id="031e0-167">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="031e0-168">Een handig hulpmiddel tooaccess deze bestanden vastleggen, opgeslagen tooa storage-account is Microsoft Azure Storage Explorer, die u kunt hier downloaden: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="031e0-168">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="031e0-169">Als een opslagaccount is opgegeven, worden bestanden voor pakket tooa storage-account op Hallo na locatie opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="031e0-169">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="031e0-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="031e0-170">Next steps</span></span>

<span data-ttu-id="031e0-171">Meer informatie over hoe tooautomate pakket worden vastgelegd met waarschuwingen van de virtuele machine door [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="031e0-171">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="031e0-172">Als bepaalde verkeer is toegestaan in orr buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="031e0-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














