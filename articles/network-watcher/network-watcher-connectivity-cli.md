---
title: Controleer de verbinding met Azure-netwerk-Watcher - Azure CLI 2.0 | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe u van connectiviteit controleren met behulp van Azure CLI 2.0 netwerk-Watcher
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
ms.openlocfilehash: c1deaa40bfda0bf3858ad56d3d6a90df34351278
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="8a0f0-103">Controleer de verbinding met Azure met Azure CLI 2.0 netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="8a0f0-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8a0f0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a0f0-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="8a0f0-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8a0f0-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="8a0f0-106">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="8a0f0-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="8a0f0-107">Informatie over het gebruik van verbinding om te controleren als direct TCP-verbinding van een virtuele machine naar een opgegeven eindpunt kan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-107">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8a0f0-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="8a0f0-108">Before you begin</span></span>

<span data-ttu-id="8a0f0-109">In dit artikel wordt ervan uitgegaan dat u hebt de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="8a0f0-109">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="8a0f0-110">Een exemplaar van netwerk-Watcher in de regio die u wilt controleren, connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-110">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="8a0f0-111">Virtuele machines connectiviteit met controleren.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-111">Virtual machines to check connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="8a0f0-112">Controle van de verbinding zijn nodig voor de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="8a0f0-113">Voor het installeren van de extensie op een Windows-virtuele machine gaat u naar [extensie voor het virtuele machine voor Windows Azure-netwerk-Watcher Agent](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="8a0f0-113">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="8a0f0-114">Registreren van de preview-mogelijkheden</span><span class="sxs-lookup"><span data-stu-id="8a0f0-114">Register the preview capability</span></span> 

<span data-ttu-id="8a0f0-115">Controle van de verbinding is momenteel in de openbare preview, voor deze functie moet worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-115">Connectivity check is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="8a0f0-116">U doet dit door de volgende CLI-voorbeeld uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8a0f0-116">To do this, run the following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="8a0f0-117">Om te controleren of dat de registratie is gelukt, voer de volgende CLI-opdracht:</span><span class="sxs-lookup"><span data-stu-id="8a0f0-117">To verify the registration was successful, run the following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="8a0f0-118">Als de functie juist is geregistreerd, de uitvoer moet overeenkomen met het volgende:</span><span class="sxs-lookup"><span data-stu-id="8a0f0-118">If the feature was properly registered, the output should match the following:</span></span> 

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

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="8a0f0-119">Controleer de verbinding met een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8a0f0-119">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="8a0f0-120">In dit voorbeeld controleert de verbinding met een doel-virtuele machine via poort 80.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-120">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="8a0f0-121">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8a0f0-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="8a0f0-122">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8a0f0-122">Response</span></span>

<span data-ttu-id="8a0f0-123">Het antwoord van de volgende is van het vorige voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-123">The following response is from the previous example.</span></span>  <span data-ttu-id="8a0f0-124">In dit antwoord de `ConnectionStatus` is **onbereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-124">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="8a0f0-125">U kunt zien dat alle tests mislukte verzonden.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-125">You can see that all the probes sent failed.</span></span> <span data-ttu-id="8a0f0-126">De verbinding is mislukt bij het virtuele apparaat als gevolg van een gebruiker geconfigureerde `NetworkSecurityRule` met de naam **UserRule_Port80**, is geconfigureerd voor het blokkeren van inkomend verkeer op poort 80.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-126">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="8a0f0-127">Deze informatie kan worden gebruikt om te onderzoeken verbindingsproblemen.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-127">This information can be used to research connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="8a0f0-128">Problemen met routing valideren</span><span class="sxs-lookup"><span data-stu-id="8a0f0-128">Validate routing issues</span></span>

<span data-ttu-id="8a0f0-129">Het voorbeeld wordt de verbinding tussen een virtuele machine en een extern eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-129">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="8a0f0-130">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8a0f0-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="8a0f0-131">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8a0f0-131">Response</span></span>

<span data-ttu-id="8a0f0-132">In het volgende voorbeeld wordt de `connectionStatus` wordt weergegeven als **onbereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-132">In the following example, the `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="8a0f0-133">In de `hops` details, kunt u zien onder `issues` dat het verkeer is geblokkeerd vanwege een `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-133">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span>

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

## <a name="check-website-latency"></a><span data-ttu-id="8a0f0-134">Latentie van de website controleren</span><span class="sxs-lookup"><span data-stu-id="8a0f0-134">Check website latency</span></span>

<span data-ttu-id="8a0f0-135">Het volgende voorbeeld wordt de verbinding met een website.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-135">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="8a0f0-136">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8a0f0-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="8a0f0-137">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8a0f0-137">Response</span></span>

<span data-ttu-id="8a0f0-138">In het volgende antwoord ziet u de `connectionStatus` wordt weergegeven als **bereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-138">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="8a0f0-139">Als een verbinding geslaagd is, zijn latentie waarden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-139">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="8a0f0-140">Controleer de verbinding met een opslag-eindpunt</span><span class="sxs-lookup"><span data-stu-id="8a0f0-140">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="8a0f0-141">Het volgende voorbeeld wordt de verbinding van een virtuele machine met een blog van storage-account.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-141">The following example checks the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="8a0f0-142">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8a0f0-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="8a0f0-143">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8a0f0-143">Response</span></span>

<span data-ttu-id="8a0f0-144">De volgende json is de voorbeeld-reactie van de vorige cmdlet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-144">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="8a0f0-145">Als de controle geslaagd is, de `connectionStatus` eigenschap wordt weergegeven als **bereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-145">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="8a0f0-146">U vindt de details met betrekking tot het aantal hops is vereist voor het bereiken van de storage-blob en latentie.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-146">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8a0f0-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a0f0-147">Next steps</span></span>

<span data-ttu-id="8a0f0-148">Meer informatie over het automatiseren van pakket opnamen met waarschuwingen van de virtuele machine met weer te geven [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="8a0f0-148">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="8a0f0-149">Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8a0f0-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
