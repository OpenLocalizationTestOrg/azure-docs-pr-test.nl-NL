---
title: connectiviteit met Azure-netwerk-Watcher - Azure CLI 2.0 aaaCheck | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toouse connectiviteit controleren met behulp van Azure CLI 2.0 netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: e94e0fad03fd36ebf4e1fdf9e3cfee934b289deb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="b4b72-103">Controleer de verbinding met Azure met Azure CLI 2.0 netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="b4b72-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b4b72-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4b72-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="b4b72-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b4b72-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="b4b72-106">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="b4b72-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="b4b72-107">Meer informatie over hoe toouse connectiviteit tooverify als een directe TCP-verbinding van een virtuele machine tooa opgegeven eindpunt kan worden vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="b4b72-107">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b4b72-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="b4b72-108">Before you begin</span></span>

<span data-ttu-id="b4b72-109">In dit artikel wordt ervan uitgegaan dat er Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="b4b72-109">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="b4b72-110">Een exemplaar van netwerk-Watcher in Hallo regio die u wilt toocheck connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="b4b72-110">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="b4b72-111">Virtuele machines toocheck connectiviteit met.</span><span class="sxs-lookup"><span data-stu-id="b4b72-111">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="b4b72-112">Controle van de verbinding zijn nodig voor de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="b4b72-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="b4b72-113">Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="b4b72-113">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="b4b72-114">Hallo preview mogelijkheid registreren</span><span class="sxs-lookup"><span data-stu-id="b4b72-114">Register hello preview capability</span></span> 

<span data-ttu-id="b4b72-115">Controle van de verbinding is momenteel in openbare preview toouse deze functie toobe geregistreerd moet.</span><span class="sxs-lookup"><span data-stu-id="b4b72-115">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="b4b72-116">toodo deze, Voer Hallo CLI voorbeeld te volgen</span><span class="sxs-lookup"><span data-stu-id="b4b72-116">toodo this, run hello following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="b4b72-117">tooverify hello registratie is gelukt, Hallo na CLI-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b4b72-117">tooverify hello registration was successful, run hello following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="b4b72-118">Als het Hallo-functie is juist is geregistreerd, Hallo uitvoer, moet overeenkomen met Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b4b72-118">If hello feature was properly registered, hello output should match hello following:</span></span> 

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Features/providers/Microsoft.Network/features/AllowNetworkWatcherConnectivityCheck",
  "name": "Microsoft.Network/AllowNetworkWatcherConnectivityCheck",
  "properties": {
    "state": "Registered"
  },
  "type": "Microsoft.Features/providers/features"
}
``` 

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="b4b72-119">Controleer de connectiviteit tooa virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b4b72-119">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="b4b72-120">In dit voorbeeld controleert connectiviteit tooa bestemde virtuele machine via poort 80.</span><span class="sxs-lookup"><span data-stu-id="b4b72-120">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="b4b72-121">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b4b72-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="b4b72-122">Antwoord</span><span class="sxs-lookup"><span data-stu-id="b4b72-122">Response</span></span>

<span data-ttu-id="b4b72-123">Hallo na antwoord is van het vorige voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="b4b72-123">hello following response is from hello previous example.</span></span>  <span data-ttu-id="b4b72-124">In dit antwoord Hallo `ConnectionStatus` is **onbereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="b4b72-124">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="b4b72-125">U kunt zien dat alle tests verzonden mislukte Hallo.</span><span class="sxs-lookup"><span data-stu-id="b4b72-125">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="b4b72-126">Hallo-connectiviteit op Hallo virtueel apparaat is mislukt vanwege tooa gebruiker geconfigureerde `NetworkSecurityRule` met de naam **UserRule_Port80**, tooblock binnenkomend verkeer op poort 80 geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b4b72-126">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="b4b72-127">Deze informatie kan gebruikte tooresearch verbindingsproblemen zijn.</span><span class="sxs-lookup"><span data-stu-id="b4b72-127">This information can be used tooresearch connection issues.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "bb01d336-d881-4808-9fbc-72f091974d68",
      "issues": [],
      "nextHopIds": [
        "f8b074e9-9980-496b-a35e-619f9bcbf648"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "10.1.2.4",
      "id": "f8b074e9-9980-496b-a35e-619f9bcbf648",
      "issues": [],
      "nextHopIds": [
        "8a5857f3-6ab8-4b11-b9bf-a046d66b8696"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fw
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.3.4",
      "id": "8a5857f3-6ab8-4b11-b9bf-a046d66b8696",
      "issues": [
        {
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule"
        }
      ],
      "nextHopIds": [
        "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/au
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.4.4",
      "id": "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/db
Nic0/ipConfigurations/ipconfig1",
      "type": "VnetLocal"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="b4b72-128">Problemen met routing valideren</span><span class="sxs-lookup"><span data-stu-id="b4b72-128">Validate routing issues</span></span>

<span data-ttu-id="b4b72-129">Hallo voorbeeld controleert de connectiviteit tussen een virtuele machine en een extern eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b4b72-129">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="b4b72-130">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b4b72-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="b4b72-131">Antwoord</span><span class="sxs-lookup"><span data-stu-id="b4b72-131">Response</span></span>

<span data-ttu-id="b4b72-132">Hallo in Hallo voorbeeld te volgen, `connectionStatus` wordt weergegeven als **onbereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="b4b72-132">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="b4b72-133">In Hallo `hops` details, kunt u zien onder `issues` dat Hallo verkeer is geblokkeerd vanwege tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="b4b72-133">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "f2cb1868-2049-4839-b8ed-57a480d06f95",
      "issues": [
        {
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute"
        }
      ],
      "nextHopIds": [
        "da4022db-0ab0-48c4-a507-dd4c03561ca5"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "13.107.21.200",
      "id": "da4022db-0ab0-48c4-a507-dd4c03561ca5",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Unknown",
      "type": "Destination"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="b4b72-134">Latentie van de website controleren</span><span class="sxs-lookup"><span data-stu-id="b4b72-134">Check website latency</span></span>

<span data-ttu-id="b4b72-135">Hallo volgende voorbeeld wordt gecontroleerd Hallo connectiviteit tooa website.</span><span class="sxs-lookup"><span data-stu-id="b4b72-135">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="b4b72-136">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b4b72-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="b4b72-137">Antwoord</span><span class="sxs-lookup"><span data-stu-id="b4b72-137">Response</span></span>

<span data-ttu-id="b4b72-138">In Hallo antwoord te volgen, ziet u Hallo `connectionStatus` wordt weergegeven als **bereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="b4b72-138">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="b4b72-139">Als een verbinding geslaagd is, zijn latentie waarden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b4b72-139">When a connection is successful, latency values are provided.</span></span>

```json
{
  "avgLatencyInMs": 2,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "639c2d19-e163-4dfd-8737-5018dd1168ae",
      "issues": [],
      "nextHopIds": [
        "fd43a6e7-c758-4f48-90aa-8db99105a4a3"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "204.79.197.200",
      "id": "fd43a6e7-c758-4f48-90aa-8db99105a4a3",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="b4b72-140">Controleer de connectiviteit tooa opslag eindpunt</span><span class="sxs-lookup"><span data-stu-id="b4b72-140">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="b4b72-141">Hallo volgende voorbeeld wordt gecontroleerd Hallo verbinding hebben met een virtuele machine tooa blog van storage-account.</span><span class="sxs-lookup"><span data-stu-id="b4b72-141">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="b4b72-142">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b4b72-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="b4b72-143">Antwoord</span><span class="sxs-lookup"><span data-stu-id="b4b72-143">Response</span></span>

<span data-ttu-id="b4b72-144">Hallo is volgende json Hallo voorbeeld reactie van de vorige Hallo-cmdlet uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b4b72-144">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="b4b72-145">Als het Hallo-controle is geslaagd, Hallo `connectionStatus` eigenschap wordt weergegeven als **bereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="b4b72-145">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="b4b72-146">U vindt Hallo-gegevens met betrekking tot Hallo aantal hops vereist tooreach Hallo storage-blob en latentie.</span><span class="sxs-lookup"><span data-stu-id="b4b72-146">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "avgLatencyInMs": 1,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "5136acff-bf26-4c93-9966-4edb7dd40353",
      "issues": [],
      "nextHopIds": [
        "f8d958b7-3636-4d63-9441-602c1eb2fd56"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "1.2.3.4",
      "id": "f8d958b7-3636-4d63-9441-602c1eb2fd56",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="next-steps"></a><span data-ttu-id="b4b72-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b4b72-147">Next steps</span></span>

<span data-ttu-id="b4b72-148">Meer informatie over hoe tooautomate pakket worden vastgelegd met waarschuwingen van de virtuele machine door [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="b4b72-148">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="b4b72-149">Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b4b72-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
