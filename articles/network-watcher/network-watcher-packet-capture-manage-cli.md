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
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="69beb-103">Pakket opnamen beheren met Azure met Azure CLI 2.0 netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="69beb-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="69beb-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="69beb-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="69beb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69beb-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="69beb-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="69beb-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="69beb-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="69beb-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="69beb-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="69beb-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="69beb-109">Netwerk-Watcher pakketopname kunt u toocreate vastleggen sessies tootrack verkeer tooand van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="69beb-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="69beb-110">Filters zijn beschikbaar voor Hallo vastleggen sessie tooensure dat u alleen Hallo verkeer die u wilt vastleggen.</span><span class="sxs-lookup"><span data-stu-id="69beb-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="69beb-111">Pakketopname helpt toodiagnose netwerk afwijkingen reactief en proactief.</span><span class="sxs-lookup"><span data-stu-id="69beb-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="69beb-112">Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's, toodebug client / server-communicatie en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="69beb-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="69beb-113">Deze mogelijkheid vergemakkelijkt door kunnen tooremotely trigger pakket opnamen, Hallo last van een pakketopname handmatig en op de gewenste machine hello, die kostbare tijd bespaart worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="69beb-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="69beb-114">In dit artikel gebruikt de volgende generatie CLI voor Hallo resource management-implementatiemodel, Azure CLI 2.0, die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="69beb-114">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="69beb-115">tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="69beb-115">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="69beb-116">In dit artikel leert u Hallo verschillende beheertaken uitvoeren die momenteel beschikbaar zijn voor pakketopname.</span><span class="sxs-lookup"><span data-stu-id="69beb-116">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="69beb-117">**Start een pakketopname**</span><span class="sxs-lookup"><span data-stu-id="69beb-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="69beb-118">**Stop de pakketopname van een**</span><span class="sxs-lookup"><span data-stu-id="69beb-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="69beb-119">**Het vastleggen van een pakket verwijderen**</span><span class="sxs-lookup"><span data-stu-id="69beb-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="69beb-120">**Een pakketopname downloaden**</span><span class="sxs-lookup"><span data-stu-id="69beb-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="69beb-121">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="69beb-121">Before you begin</span></span>

<span data-ttu-id="69beb-122">In dit artikel wordt ervan uitgegaan dat er Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="69beb-122">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="69beb-123">Een exemplaar van netwerk-Watcher in Hallo regio die u wilt een pakketopname toocreate</span><span class="sxs-lookup"><span data-stu-id="69beb-123">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="69beb-124">Een virtuele machine met hello-pakket vastleggen uitbreiding ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="69beb-124">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69beb-125">Pakketopname vereist een agent toobe op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="69beb-125">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="69beb-126">Hallo Agent wordt geïnstalleerd als een uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="69beb-126">hello Agent is installed as an extension.</span></span> <span data-ttu-id="69beb-127">Voor instructies voor het VM-extensies, gaat u naar [uitbreidingen van de virtuele Machine en functies](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="69beb-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="69beb-128">VM-extensie installeren</span><span class="sxs-lookup"><span data-stu-id="69beb-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="69beb-129">Stap 1</span><span class="sxs-lookup"><span data-stu-id="69beb-129">Step 1</span></span>

<span data-ttu-id="69beb-130">Voer Hallo `az vm extension set` cmdlet tooinstall Hallo pakket vastleggen agent op de virtuele gastmachine Hallo.</span><span class="sxs-lookup"><span data-stu-id="69beb-130">Run hello `az vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="69beb-131">Voor Windows virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="69beb-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="69beb-132">Voor virtuele Linux-machines:</span><span class="sxs-lookup"><span data-stu-id="69beb-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="69beb-133">Stap 2</span><span class="sxs-lookup"><span data-stu-id="69beb-133">Step 2</span></span>

<span data-ttu-id="69beb-134">tooensure die Hallo agent is geïnstalleerd, voert u Hallo `vm extension get` cmdlet en geef dit Hallo-resourcegroep en de naam van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="69beb-134">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="69beb-135">Controleer Hallo resulterende lijst tooensure Hallo agent is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="69beb-135">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="69beb-136">Hallo volgende voorbeeld is een voorbeeld van antwoord Hallo wordt uitgevoerd`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="69beb-136">hello following sample is an example of hello response from running `az vm extension show`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="69beb-137">Start een pakketopname</span><span class="sxs-lookup"><span data-stu-id="69beb-137">Start a packet capture</span></span>

<span data-ttu-id="69beb-138">Zodra hello voorgaande stappen voltooid hebt, wordt Hallo pakket vastleggen agent is geïnstalleerd op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="69beb-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="69beb-139">Stap 1</span><span class="sxs-lookup"><span data-stu-id="69beb-139">Step 1</span></span>

<span data-ttu-id="69beb-140">de volgende stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="69beb-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="69beb-141">De naam van de Tkan Hallo netwerk-Watcher wordt doorgegeven toohello `az network watcher show` cmdlet in stap 4.</span><span class="sxs-lookup"><span data-stu-id="69beb-141">TThe name of hello Network Watcher is passed toohello `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="69beb-142">Stap 2</span><span class="sxs-lookup"><span data-stu-id="69beb-142">Step 2</span></span>

<span data-ttu-id="69beb-143">Een opslagaccount ophalen.</span><span class="sxs-lookup"><span data-stu-id="69beb-143">Retrieve a storage account.</span></span> <span data-ttu-id="69beb-144">Dit opslagaccount is gebruikte toostore Hallo pakket vastleggen bestand.</span><span class="sxs-lookup"><span data-stu-id="69beb-144">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="69beb-145">Stap 3</span><span class="sxs-lookup"><span data-stu-id="69beb-145">Step 3</span></span>

<span data-ttu-id="69beb-146">Filters kunnen gebruikte toolimit Hallo gegevens die zijn opgeslagen door Hallo pakketopname zijn.</span><span class="sxs-lookup"><span data-stu-id="69beb-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="69beb-147">Hallo stelt volgende voorbeeld een pakketopname met verschillende filters.</span><span class="sxs-lookup"><span data-stu-id="69beb-147">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="69beb-148">Hallo eerste drie filters verzamelen uitgaande TCP-verkeer alleen van het lokale IP 10.0.0.3 toodestination poorten 20, 80 en 443.</span><span class="sxs-lookup"><span data-stu-id="69beb-148">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="69beb-149">de laatste filter Hallo verzamelt UDP-verkeer.</span><span class="sxs-lookup"><span data-stu-id="69beb-149">hello last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="69beb-150">Hallo volgende voorbeeld is de Hallo verwacht uitvoer Hallo uitgevoerd `az network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="69beb-150">hello following example is hello expected output from running hello `az network watcher packet-capture create` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="69beb-151">Ophalen van een pakketopname</span><span class="sxs-lookup"><span data-stu-id="69beb-151">Get a packet capture</span></span>

<span data-ttu-id="69beb-152">Hallo uitgevoerd `az network watcher packet-capture show` -cmdlet haalt Hallo status van een pakketopname momenteel wordt uitgevoerd of voltooid is.</span><span class="sxs-lookup"><span data-stu-id="69beb-152">Running hello `az network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="69beb-153">Hallo volgende voorbeeld is Hallo-uitvoer van Hallo `az network watcher packet-capture show` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="69beb-153">hello following example is hello output from hello `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="69beb-154">Hallo wordt volgende voorbeeld nadat Hallo vastleggen voltooid is.</span><span class="sxs-lookup"><span data-stu-id="69beb-154">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="69beb-155">Hallo PacketCaptureStatus waarde is met een StopReason TimeExceeded gestopt.</span><span class="sxs-lookup"><span data-stu-id="69beb-155">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="69beb-156">Deze waarde geeft aan dat Hallo pakketopname voltooid is en de tijd wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="69beb-156">This value shows that hello packet capture was successful and ran its time.</span></span>

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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="69beb-157">Stop de pakketopname van een</span><span class="sxs-lookup"><span data-stu-id="69beb-157">Stop a packet capture</span></span>

<span data-ttu-id="69beb-158">Door het uitvoeren van Hallo `az network watcher packet-capture stop` als een opnamesessie Bezig het is-cmdlet is gestopt.</span><span class="sxs-lookup"><span data-stu-id="69beb-158">By running hello `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="69beb-159">Hallo cmdlet retourneert geen antwoord wanneer uitgevoerd op een actieve opnamesessie of een bestaande sessie die al is gestopt.</span><span class="sxs-lookup"><span data-stu-id="69beb-159">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="69beb-160">Het vastleggen van een pakket verwijderen</span><span class="sxs-lookup"><span data-stu-id="69beb-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="69beb-161">Als een pakketopname, verwijdert Hallo-bestand in Hallo storage-account niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="69beb-161">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="69beb-162">Een pakketopname downloaden</span><span class="sxs-lookup"><span data-stu-id="69beb-162">Download a packet capture</span></span>

<span data-ttu-id="69beb-163">Zodra de sessie van uw pakket vastleggen is voltooid, kan Hallo vastleggen bestand geüploade tooblob opslag of tooa lokaal bestand op Hallo VM zijn.</span><span class="sxs-lookup"><span data-stu-id="69beb-163">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="69beb-164">Hallo-opslaglocatie van Hallo pakketopname is gedefinieerd bij het maken van Hallo-sessie.</span><span class="sxs-lookup"><span data-stu-id="69beb-164">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="69beb-165">Een handig hulpmiddel tooaccess deze bestanden vastleggen, opgeslagen tooa storage-account is Microsoft Azure Storage Explorer, die u kunt hier downloaden: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="69beb-165">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="69beb-166">Als een opslagaccount is opgegeven, worden bestanden voor pakket tooa storage-account op Hallo na locatie opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="69beb-166">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="69beb-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="69beb-167">Next steps</span></span>

<span data-ttu-id="69beb-168">Meer informatie over hoe tooautomate pakket worden vastgelegd met waarschuwingen van de virtuele machine door [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="69beb-168">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="69beb-169">Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="69beb-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
