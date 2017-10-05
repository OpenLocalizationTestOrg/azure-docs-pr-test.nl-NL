---
title: Pakket opnamen met Azure-netwerk-Watcher - Azure CLI 2.0 beheren | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe u voor het beheren van de functie voor het vastleggen van pakket van netwerk-Watcher met Azure CLI 2.0
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
ms.openlocfilehash: c94eb46f31f2f19b843ccd7bf77b8a39943a07d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="2fe49-103">Pakket opnamen beheren met Azure met Azure CLI 2.0 netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="2fe49-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2fe49-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2fe49-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="2fe49-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fe49-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="2fe49-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2fe49-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="2fe49-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2fe49-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="2fe49-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="2fe49-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="2fe49-109">Netwerk-Watcher pakketopname kunt u om sessies vastleggen om bij te houden van verkeer van en naar een virtuele machine te maken.</span><span class="sxs-lookup"><span data-stu-id="2fe49-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="2fe49-110">Filters zijn beschikbaar voor de opnamesessie om te controleren of dat u alleen het verkeer die u wilt vastleggen.</span><span class="sxs-lookup"><span data-stu-id="2fe49-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="2fe49-111">Pakketopname helpt op te sporen netwerk afwijkingen reactief en proactief.</span><span class="sxs-lookup"><span data-stu-id="2fe49-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="2fe49-112">Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's voor foutopsporing van client-servercommunicaties en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="2fe49-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="2fe49-113">Door op afstand activeren pakket opnamen, deze mogelijkheid kan vergemakkelijken de last van een pakketopname handmatig en op de gewenste machine, die kostbare tijd bespaart worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2fe49-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="2fe49-114">Dit artikel wordt de volgende generatie CLI gebruikt voor de resource management-implementatiemodel, Azure CLI 2.0, die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="2fe49-114">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="2fe49-115">Als u wilt de stappen in dit artikel uitvoert, moet u [installeren van de Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="2fe49-115">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="2fe49-116">In dit artikel leert u de verschillende beheertaken die momenteel beschikbaar voor pakketopname zijn.</span><span class="sxs-lookup"><span data-stu-id="2fe49-116">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="2fe49-117">**Start een pakketopname**</span><span class="sxs-lookup"><span data-stu-id="2fe49-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="2fe49-118">**Stop de pakketopname van een**</span><span class="sxs-lookup"><span data-stu-id="2fe49-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="2fe49-119">**Het vastleggen van een pakket verwijderen**</span><span class="sxs-lookup"><span data-stu-id="2fe49-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="2fe49-120">**Een pakketopname downloaden**</span><span class="sxs-lookup"><span data-stu-id="2fe49-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="2fe49-121">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="2fe49-121">Before you begin</span></span>

<span data-ttu-id="2fe49-122">In dit artikel wordt ervan uitgegaan dat u hebt de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="2fe49-122">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="2fe49-123">Een exemplaar van netwerk-Watcher in de regio die u wilt maken van een pakketopname</span><span class="sxs-lookup"><span data-stu-id="2fe49-123">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="2fe49-124">Een virtuele machine met de pakket-capture-extensie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2fe49-124">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fe49-125">Pakketopname vereist een agent te worden uitgevoerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2fe49-125">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="2fe49-126">De Agent wordt geïnstalleerd als een uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="2fe49-126">The Agent is installed as an extension.</span></span> <span data-ttu-id="2fe49-127">Voor instructies voor het VM-extensies, gaat u naar [uitbreidingen van de virtuele Machine en functies](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="2fe49-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="2fe49-128">VM-extensie installeren</span><span class="sxs-lookup"><span data-stu-id="2fe49-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="2fe49-129">Stap 1</span><span class="sxs-lookup"><span data-stu-id="2fe49-129">Step 1</span></span>

<span data-ttu-id="2fe49-130">Voer de `az vm extension set` cmdlet het pakket capture-agent installeren op de virtuele gastmachine.</span><span class="sxs-lookup"><span data-stu-id="2fe49-130">Run the `az vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="2fe49-131">Voor Windows virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="2fe49-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="2fe49-132">Voor virtuele Linux-machines:</span><span class="sxs-lookup"><span data-stu-id="2fe49-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="2fe49-133">Stap 2</span><span class="sxs-lookup"><span data-stu-id="2fe49-133">Step 2</span></span>

<span data-ttu-id="2fe49-134">Om ervoor te zorgen dat de agent is geïnstalleerd, voer de `vm extension get` cmdlet en geef dit door de naam van de resource en de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2fe49-134">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="2fe49-135">Controleer de resulterende lijst om te controleren of dat de agent is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2fe49-135">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="2fe49-136">Het volgende voorbeeld is een voorbeeld van het antwoord worden uitgevoerd`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="2fe49-136">The following sample is an example of the response from running `az vm extension show`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="2fe49-137">Start een pakketopname</span><span class="sxs-lookup"><span data-stu-id="2fe49-137">Start a packet capture</span></span>

<span data-ttu-id="2fe49-138">Als de voorgaande stappen voltooid zijn, wordt het pakket vastleggen-agent geïnstalleerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2fe49-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="2fe49-139">Stap 1</span><span class="sxs-lookup"><span data-stu-id="2fe49-139">Step 1</span></span>

<span data-ttu-id="2fe49-140">De volgende stap is het exemplaar van de netwerk-Watcher ophalen.</span><span class="sxs-lookup"><span data-stu-id="2fe49-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="2fe49-141">Tkan-naam van de netwerk-Watcher wordt doorgegeven aan de `az network watcher show` cmdlet in stap 4.</span><span class="sxs-lookup"><span data-stu-id="2fe49-141">TThe name of the Network Watcher is passed to the `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="2fe49-142">Stap 2</span><span class="sxs-lookup"><span data-stu-id="2fe49-142">Step 2</span></span>

<span data-ttu-id="2fe49-143">Een opslagaccount ophalen.</span><span class="sxs-lookup"><span data-stu-id="2fe49-143">Retrieve a storage account.</span></span> <span data-ttu-id="2fe49-144">Dit opslagaccount wordt gebruikt voor het opslaan van het pakket capture-bestand.</span><span class="sxs-lookup"><span data-stu-id="2fe49-144">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="2fe49-145">Stap 3</span><span class="sxs-lookup"><span data-stu-id="2fe49-145">Step 3</span></span>

<span data-ttu-id="2fe49-146">Filters kunnen worden gebruikt om te beperken van de gegevens die door het vastleggen van het pakket wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2fe49-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="2fe49-147">Het volgende voorbeeld stelt een pakketopname met verschillende filters.</span><span class="sxs-lookup"><span data-stu-id="2fe49-147">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="2fe49-148">De eerste drie filters voor het verzamelen van uitgaande TCP-verkeer alleen van het lokale IP 10.0.0.3 voor doelpoorten 20, 80 en 443.</span><span class="sxs-lookup"><span data-stu-id="2fe49-148">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="2fe49-149">Het laatste filter verzamelt UDP-verkeer.</span><span class="sxs-lookup"><span data-stu-id="2fe49-149">The last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="2fe49-150">Het volgende voorbeeld is de verwachte uitvoer uitvoeren van de `az network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fe49-150">The following example is the expected output from running the `az network watcher packet-capture create` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="2fe49-151">Ophalen van een pakketopname</span><span class="sxs-lookup"><span data-stu-id="2fe49-151">Get a packet capture</span></span>

<span data-ttu-id="2fe49-152">Met de `az network watcher packet-capture show` -cmdlet haalt de status van een pakketopname momenteel wordt uitgevoerd of voltooid is.</span><span class="sxs-lookup"><span data-stu-id="2fe49-152">Running the `az network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="2fe49-153">Het volgende voorbeeld wordt de uitvoer van de `az network watcher packet-capture show` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fe49-153">The following example is the output from the `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="2fe49-154">Het volgende voorbeeld is nadat het vastleggen voltooid is.</span><span class="sxs-lookup"><span data-stu-id="2fe49-154">The following example is after the capture is complete.</span></span> <span data-ttu-id="2fe49-155">De waarde PacketCaptureStatus is gestopt met een StopReason TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="2fe49-155">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="2fe49-156">Deze waarde geeft aan dat het vastleggen van het pakket voltooid is en de tijd wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2fe49-156">This value shows that the packet capture was successful and ran its time.</span></span>

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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="2fe49-157">Stop de pakketopname van een</span><span class="sxs-lookup"><span data-stu-id="2fe49-157">Stop a packet capture</span></span>

<span data-ttu-id="2fe49-158">Door het uitvoeren van de `az network watcher packet-capture stop` als een opnamesessie Bezig het is-cmdlet is gestopt.</span><span class="sxs-lookup"><span data-stu-id="2fe49-158">By running the `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="2fe49-159">De cmdlet retourneert geen antwoord wanneer uitgevoerd op een actieve opnamesessie of een bestaande sessie die al is gestopt.</span><span class="sxs-lookup"><span data-stu-id="2fe49-159">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="2fe49-160">Het vastleggen van een pakket verwijderen</span><span class="sxs-lookup"><span data-stu-id="2fe49-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="2fe49-161">Als u het vastleggen van een pakket verwijdert, verwijdert niet het bestand in het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2fe49-161">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="2fe49-162">Een pakketopname downloaden</span><span class="sxs-lookup"><span data-stu-id="2fe49-162">Download a packet capture</span></span>

<span data-ttu-id="2fe49-163">Zodra de sessie van uw pakket vastleggen is voltooid, kan het bestand vastleggen kan worden geüpload naar de blob-opslag of naar een lokaal bestand op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2fe49-163">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="2fe49-164">De opslaglocatie van de pakketopname is gedefinieerd bij het maken van de sessie.</span><span class="sxs-lookup"><span data-stu-id="2fe49-164">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="2fe49-165">Een handig hulpmiddel voor toegang tot deze capture-bestanden opgeslagen in een opslagaccount is Microsoft Azure Storage Explorer, die u kunt hier downloaden: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="2fe49-165">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="2fe49-166">Als een opslagaccount is opgegeven, worden bestanden voor pakket worden opgeslagen in een opslagaccount op de volgende locatie:</span><span class="sxs-lookup"><span data-stu-id="2fe49-166">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="2fe49-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2fe49-167">Next steps</span></span>

<span data-ttu-id="2fe49-168">Meer informatie over het automatiseren van pakket opnamen met waarschuwingen van de virtuele machine met weer te geven [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="2fe49-168">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="2fe49-169">Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2fe49-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
