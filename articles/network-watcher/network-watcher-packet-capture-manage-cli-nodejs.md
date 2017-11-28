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
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="d5f48-103">Pakket opnamen beheren met Azure met Azure CLI 1.0 netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="d5f48-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d5f48-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d5f48-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="d5f48-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5f48-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="d5f48-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d5f48-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="d5f48-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d5f48-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="d5f48-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="d5f48-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="d5f48-109">Netwerk-Watcher pakketopname kunt u toocreate vastleggen sessies tootrack verkeer tooand van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d5f48-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="d5f48-110">Filters zijn beschikbaar voor Hallo vastleggen sessie tooensure dat u alleen Hallo verkeer die u wilt vastleggen.</span><span class="sxs-lookup"><span data-stu-id="d5f48-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="d5f48-111">Pakketopname helpt toodiagnose netwerk afwijkingen reactief en proactief.</span><span class="sxs-lookup"><span data-stu-id="d5f48-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="d5f48-112">Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's, toodebug client / server-communicatie en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="d5f48-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="d5f48-113">Deze mogelijkheid vergemakkelijkt door kunnen tooremotely trigger pakket opnamen, Hallo last van een pakketopname handmatig en op de gewenste machine hello, die kostbare tijd bespaart worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d5f48-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="d5f48-114">Dit artikel wordt platformoverschrijdende Azure CLI 1.0 gebruikt die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="d5f48-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="d5f48-115">In dit artikel leert u Hallo verschillende beheertaken uitvoeren die momenteel beschikbaar zijn voor pakketopname.</span><span class="sxs-lookup"><span data-stu-id="d5f48-115">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="d5f48-116">**Start een pakketopname**</span><span class="sxs-lookup"><span data-stu-id="d5f48-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="d5f48-117">**Stop de pakketopname van een**</span><span class="sxs-lookup"><span data-stu-id="d5f48-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="d5f48-118">**Het vastleggen van een pakket verwijderen**</span><span class="sxs-lookup"><span data-stu-id="d5f48-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="d5f48-119">**Een pakketopname downloaden**</span><span class="sxs-lookup"><span data-stu-id="d5f48-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="d5f48-120">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="d5f48-120">Before you begin</span></span>

<span data-ttu-id="d5f48-121">In dit artikel wordt ervan uitgegaan dat er Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="d5f48-121">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="d5f48-122">Een exemplaar van netwerk-Watcher in Hallo regio die u wilt een pakketopname toocreate</span><span class="sxs-lookup"><span data-stu-id="d5f48-122">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="d5f48-123">Een virtuele machine met hello-pakket vastleggen uitbreiding ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d5f48-123">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5f48-124">Pakketopname vereist een agent toobe op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d5f48-124">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="d5f48-125">Hallo Agent wordt geïnstalleerd als een uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="d5f48-125">hello Agent is installed as an extension.</span></span> <span data-ttu-id="d5f48-126">Voor instructies voor het VM-extensies, gaat u naar [uitbreidingen van de virtuele Machine en functies](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="d5f48-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="d5f48-127">VM-extensie installeren</span><span class="sxs-lookup"><span data-stu-id="d5f48-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="d5f48-128">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d5f48-128">Step 1</span></span>

<span data-ttu-id="d5f48-129">Voer Hallo `azure vm extension set` cmdlet tooinstall Hallo pakket vastleggen agent op de virtuele gastmachine Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5f48-129">Run hello `azure vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="d5f48-130">Voor Windows virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="d5f48-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="d5f48-131">Voor virtuele Linux-machines:</span><span class="sxs-lookup"><span data-stu-id="d5f48-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="d5f48-132">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d5f48-132">Step 2</span></span>

<span data-ttu-id="d5f48-133">tooensure die Hallo agent is geïnstalleerd, voert u Hallo `vm extension get` cmdlet en geef dit Hallo-resourcegroep en de naam van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d5f48-133">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="d5f48-134">Controleer Hallo resulterende lijst tooensure Hallo agent is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d5f48-134">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="d5f48-135">Hallo volgende voorbeeld is een voorbeeld van antwoord Hallo wordt uitgevoerd`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="d5f48-135">hello following sample is an example of hello response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="d5f48-136">Start een pakketopname</span><span class="sxs-lookup"><span data-stu-id="d5f48-136">Start a packet capture</span></span>

<span data-ttu-id="d5f48-137">Zodra hello voorgaande stappen voltooid hebt, wordt Hallo pakket vastleggen agent is geïnstalleerd op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d5f48-137">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="d5f48-138">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d5f48-138">Step 1</span></span>

<span data-ttu-id="d5f48-139">de volgende stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="d5f48-139">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="d5f48-140">Deze variabele wordt doorgegeven toohello `network watcher show` cmdlet in stap 4.</span><span class="sxs-lookup"><span data-stu-id="d5f48-140">This variable is passed toohello `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="d5f48-141">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d5f48-141">Step 2</span></span>

<span data-ttu-id="d5f48-142">Een opslagaccount ophalen.</span><span class="sxs-lookup"><span data-stu-id="d5f48-142">Retrieve a storage account.</span></span> <span data-ttu-id="d5f48-143">Dit opslagaccount is gebruikte toostore Hallo pakket vastleggen bestand.</span><span class="sxs-lookup"><span data-stu-id="d5f48-143">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="d5f48-144">Stap 3</span><span class="sxs-lookup"><span data-stu-id="d5f48-144">Step 3</span></span>

<span data-ttu-id="d5f48-145">Filters kunnen gebruikte toolimit Hallo gegevens die zijn opgeslagen door Hallo pakketopname zijn.</span><span class="sxs-lookup"><span data-stu-id="d5f48-145">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="d5f48-146">Hallo stelt volgende voorbeeld een pakketopname met verschillende filters.</span><span class="sxs-lookup"><span data-stu-id="d5f48-146">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="d5f48-147">Hallo eerste drie filters verzamelen uitgaande TCP-verkeer alleen van het lokale IP 10.0.0.3 toodestination poorten 20, 80 en 443.</span><span class="sxs-lookup"><span data-stu-id="d5f48-147">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="d5f48-148">de laatste filter Hallo verzamelt UDP-verkeer.</span><span class="sxs-lookup"><span data-stu-id="d5f48-148">hello last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="d5f48-149">Meerdere filters kunnen worden gedefinieerd voor het vastleggen van een pakket.</span><span class="sxs-lookup"><span data-stu-id="d5f48-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="d5f48-150">Als u van een complexe filter-structuur gebruikmaakt, is het beter toouse filters als een json-bestand tooavoid syntaxisfouten ontdekt.</span><span class="sxs-lookup"><span data-stu-id="d5f48-150">If you are using a complex filter structure, it is better toouse filters as a json file tooavoid syntax errors.</span></span> <span data-ttu-id="d5f48-151">Hallo-vlag bijvoorbeeld gebruiken '-r ' (in plaats van '-f ') en doorgeven Hallo-locatie van een json-bestand met Hallo filters te volgen:</span><span class="sxs-lookup"><span data-stu-id="d5f48-151">For example, use hello flag "-r" (instead of "-f") and pass hello location of a json file containing hello following filters:</span></span>

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


<span data-ttu-id="d5f48-152">Hallo volgende voorbeeld is de Hallo verwacht uitvoer Hallo uitgevoerd `network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f48-152">hello following example is hello expected output from running hello `network watcher packet-capture create` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="d5f48-153">Ophalen van een pakketopname</span><span class="sxs-lookup"><span data-stu-id="d5f48-153">Get a packet capture</span></span>

<span data-ttu-id="d5f48-154">Hallo uitgevoerd `network watcher packet-capture show` -cmdlet haalt Hallo status van een pakketopname momenteel wordt uitgevoerd of voltooid is.</span><span class="sxs-lookup"><span data-stu-id="d5f48-154">Running hello `network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="d5f48-155">Hallo volgende voorbeeld is Hallo-uitvoer van Hallo `network watcher packet-capture show` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f48-155">hello following example is hello output from hello `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="d5f48-156">Hallo wordt volgende voorbeeld nadat Hallo vastleggen voltooid is.</span><span class="sxs-lookup"><span data-stu-id="d5f48-156">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="d5f48-157">Hallo PacketCaptureStatus waarde is met een StopReason TimeExceeded gestopt.</span><span class="sxs-lookup"><span data-stu-id="d5f48-157">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="d5f48-158">Deze waarde geeft aan dat Hallo pakketopname voltooid is en de tijd wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d5f48-158">This value shows that hello packet capture was successful and ran its time.</span></span>

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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="d5f48-159">Stop de pakketopname van een</span><span class="sxs-lookup"><span data-stu-id="d5f48-159">Stop a packet capture</span></span>

<span data-ttu-id="d5f48-160">Door het uitvoeren van Hallo `network watcher packet-capture stop` als een opnamesessie Bezig het is-cmdlet is gestopt.</span><span class="sxs-lookup"><span data-stu-id="d5f48-160">By running hello `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="d5f48-161">Hallo cmdlet retourneert geen antwoord wanneer uitgevoerd op een actieve opnamesessie of een bestaande sessie die al is gestopt.</span><span class="sxs-lookup"><span data-stu-id="d5f48-161">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="d5f48-162">Het vastleggen van een pakket verwijderen</span><span class="sxs-lookup"><span data-stu-id="d5f48-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="d5f48-163">Als een pakketopname, verwijdert Hallo-bestand in Hallo storage-account niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d5f48-163">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="d5f48-164">Een pakketopname downloaden</span><span class="sxs-lookup"><span data-stu-id="d5f48-164">Download a packet capture</span></span>

<span data-ttu-id="d5f48-165">Zodra de sessie van uw pakket vastleggen is voltooid, kan Hallo vastleggen bestand geüploade tooblob opslag of tooa lokaal bestand op Hallo VM zijn.</span><span class="sxs-lookup"><span data-stu-id="d5f48-165">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="d5f48-166">Hallo-opslaglocatie van Hallo pakketopname is gedefinieerd bij het maken van Hallo-sessie.</span><span class="sxs-lookup"><span data-stu-id="d5f48-166">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="d5f48-167">Een handig hulpmiddel tooaccess deze bestanden vastleggen, opgeslagen tooa storage-account is Microsoft Azure Storage Explorer, die u kunt hier downloaden: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="d5f48-167">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="d5f48-168">Als een opslagaccount is opgegeven, worden bestanden voor pakket tooa storage-account op Hallo na locatie opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="d5f48-168">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="d5f48-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d5f48-169">Next steps</span></span>

<span data-ttu-id="d5f48-170">Meer informatie over hoe tooautomate pakket worden vastgelegd met waarschuwingen van de virtuele machine door [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="d5f48-170">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="d5f48-171">Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d5f48-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
