---
title: aaaCheck connectiviteit met de Azure-netwerk-Watcher - Azure-portal | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toocheck connectiviteit met de netwerk-Watcher in hello Azure-portal
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
ms.date: 08/02/2017
ms.author: gwallace
ms.openlocfilehash: 8560011906fcce46d31556fc52cbfa671e8e653a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="b59dd-103">Controleer de verbinding met de netwerk-Watcher van Azure met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="b59dd-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b59dd-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b59dd-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="b59dd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b59dd-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="b59dd-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b59dd-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="b59dd-107">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="b59dd-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="b59dd-108">Meer informatie over hoe toouse connectiviteit tooverify als een directe TCP-verbinding van een virtuele machine tooa opgegeven eindpunt kan worden vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="b59dd-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b59dd-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="b59dd-109">Before you begin</span></span>

<span data-ttu-id="b59dd-110">In dit artikel wordt ervan uitgegaan dat er Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="b59dd-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="b59dd-111">Een exemplaar van netwerk-Watcher in Hallo regio die u wilt toocheck connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="b59dd-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="b59dd-112">Virtuele machines toocheck connectiviteit met.</span><span class="sxs-lookup"><span data-stu-id="b59dd-112">Virtual machines toocheck connectivity with.</span></span>

<span data-ttu-id="b59dd-113">ARMclient is gebruikte toocall Hallo REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b59dd-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="b59dd-114">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="b59dd-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="b59dd-115">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="b59dd-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="b59dd-116">Controle van de verbinding zijn nodig voor de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="b59dd-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="b59dd-117">Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="b59dd-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="b59dd-118">Hallo preview mogelijkheid registreren</span><span class="sxs-lookup"><span data-stu-id="b59dd-118">Register hello preview capability</span></span>

<span data-ttu-id="b59dd-119">Controle van de verbinding is momenteel in openbare preview toouse deze functie toobe geregistreerd moet.</span><span class="sxs-lookup"><span data-stu-id="b59dd-119">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="b59dd-120">toodo deze, Voer Hallo PowerShell-voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="b59dd-120">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="b59dd-121">tooverify hello registratie is gelukt, Hallo volgende Powershell-voorbeeld uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b59dd-121">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="b59dd-122">Als het Hallo-functie is juist is geregistreerd, Hallo uitvoer, moet overeenkomen met Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b59dd-122">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="b59dd-123">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="b59dd-123">Log in with ARMClient</span></span>

<span data-ttu-id="b59dd-124">Meld u bij tooarmclient met uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="b59dd-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="b59dd-125">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="b59dd-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="b59dd-126">Hallo script tooreturn na een virtuele machine uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b59dd-126">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="b59dd-127">Deze informatie is nodig voor het uitvoeren van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="b59dd-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="b59dd-128">Hallo na code moet waarden voor Hallo variabelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b59dd-128">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="b59dd-129">**subscriptionId** -Hallo toouse voor abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="b59dd-129">**subscriptionId** - hello subscription ID toouse.</span></span>
- <span data-ttu-id="b59dd-130">**resourceGroupName** - hello naam van een resourcegroep die virtuele machines bevatten.</span><span class="sxs-lookup"><span data-stu-id="b59dd-130">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="b59dd-131">Hallo-ID van Hallo virtuele machine wordt van de volgende Hallo uitvoer, gebruikt in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="b59dd-131">From hello following output, hello ID of hello virtual machine is used in hello following example:</span></span>

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

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="b59dd-132">Controleer de connectiviteit tooa virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b59dd-132">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="b59dd-133">In dit voorbeeld controleert connectiviteit tooa bestemde virtuele machine via poort 80.</span><span class="sxs-lookup"><span data-stu-id="b59dd-133">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="b59dd-134">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b59dd-134">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/Database0"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'resourceId': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="b59dd-135">Omdat deze bewerking lang is wordt uitgevoerd, Hallo URI voor Hallo resultaat geretourneerd als Hallo antwoordheader zoals weergegeven in het volgende antwoord Hallo:</span><span class="sxs-lookup"><span data-stu-id="b59dd-135">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="b59dd-136">**Belangrijke waarden**</span><span class="sxs-lookup"><span data-stu-id="b59dd-136">**Important Values**</span></span>

* <span data-ttu-id="b59dd-137">**Locatie** -deze eigenschap bevat Hallo URI waar Hallo resultaten zijn wanneer hello bewerking is voltooid</span><span class="sxs-lookup"><span data-stu-id="b59dd-137">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: f09b55fe-1d3a-4df7-817f-bceb8d2a94c8
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/f09b55fe-1d3a-4df7-817f-bceb8d2a94c8?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 367a91aa-7142-436a-867d-d3a36f80bc54
x-ms-routing-request-id: WESTUS2:20170602T202117Z:367a91aa-7142-436a-867d-d3a36f80bc54
Date: Fri, 02 Jun 2017 20:21:16 GMT

null
```

### <a name="response"></a><span data-ttu-id="b59dd-138">Antwoord</span><span class="sxs-lookup"><span data-stu-id="b59dd-138">Response</span></span>

<span data-ttu-id="b59dd-139">Hallo na antwoord is van het vorige voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="b59dd-139">hello following response is from hello previous example.</span></span>  <span data-ttu-id="b59dd-140">In dit antwoord Hallo `ConnectionStatus` is **onbereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="b59dd-140">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="b59dd-141">U kunt zien dat alle tests verzonden mislukte Hallo.</span><span class="sxs-lookup"><span data-stu-id="b59dd-141">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="b59dd-142">Hallo-connectiviteit op Hallo virtueel apparaat is mislukt vanwege tooa gebruiker geconfigureerde `NetworkSecurityRule` met de naam **UserRule_Port80**, tooblock binnenkomend verkeer op poort 80 geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b59dd-142">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="b59dd-143">Deze informatie kan gebruikte tooresearch verbindingsproblemen zijn.</span><span class="sxs-lookup"><span data-stu-id="b59dd-143">This information can be used tooresearch connection issues.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "0cb75c91-7ebf-4df8-8424-15594d6fb51c",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684",
      "address": "10.1.2.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "75e0cfa5-f9d2-48d8-b705-2c7016f81570"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "75e0cfa5-f9d2-48d8-b705-2c7016f81570",
      "address": "10.1.3.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "86caf6aa-33b0-48a1-b4da-f3c9ce785072"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule",
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ]
        }
      ]
    },
    {
      "type": "VnetLocal",
      "id": "86caf6aa-33b0-48a1-b4da-f3c9ce785072",
      "address": "10.1.4.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="b59dd-144">Problemen met routing valideren</span><span class="sxs-lookup"><span data-stu-id="b59dd-144">Validate routing issues</span></span>

<span data-ttu-id="b59dd-145">Hallo voorbeeld controleert de connectiviteit tussen een virtuele machine en een extern eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b59dd-145">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="b59dd-146">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b59dd-146">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "13.107.21.200"
$destinationPort = "80"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="b59dd-147">Omdat deze bewerking lang is wordt uitgevoerd, Hallo URI voor Hallo resultaat geretourneerd als Hallo antwoordheader zoals weergegeven in het volgende antwoord Hallo:</span><span class="sxs-lookup"><span data-stu-id="b59dd-147">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="b59dd-148">**Belangrijke waarden**</span><span class="sxs-lookup"><span data-stu-id="b59dd-148">**Important Values**</span></span>

* <span data-ttu-id="b59dd-149">**Locatie** -deze eigenschap bevat Hallo URI waar Hallo resultaten zijn wanneer hello bewerking is voltooid</span><span class="sxs-lookup"><span data-stu-id="b59dd-149">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 15eeeb69-fcef-41db-bc4a-e2adcf2658e0
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/15eeeb69-fcef-41db-bc4a-e2adcf2658e0?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4370b798-cd8b-4d3e-ba28-22232bc81dc5
x-ms-routing-request-id: WESTUS:20170602T202606Z:4370b798-cd8b-4d3e-ba28-22232bc81dc5
Date: Fri, 02 Jun 2017 20:26:05 GMT

null
```

### <a name="response"></a><span data-ttu-id="b59dd-150">Antwoord</span><span class="sxs-lookup"><span data-stu-id="b59dd-150">Response</span></span>

<span data-ttu-id="b59dd-151">Hallo in Hallo voorbeeld te volgen, `connectionStatus` wordt weergegeven als **onbereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="b59dd-151">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="b59dd-152">In Hallo `hops` details, kunt u zien onder `issues` dat Hallo verkeer is geblokkeerd vanwege tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="b59dd-152">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "5528055a-b393-4751-97bc-353d8c0aaeff",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "66eefa79-5bfe-48b2-b6ca-eec8247457a3"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute",
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ]
        }
      ]
    },
    {
      "type": "Destination",
      "id": "66eefa79-5bfe-48b2-b6ca-eec8247457a3",
      "address": "13.107.21.200",
      "resourceId": "Unknown",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="b59dd-153">Latentie van de website controleren</span><span class="sxs-lookup"><span data-stu-id="b59dd-153">Check website latency</span></span>

<span data-ttu-id="b59dd-154">Hallo volgende voorbeeld wordt gecontroleerd Hallo connectiviteit tooa website.</span><span class="sxs-lookup"><span data-stu-id="b59dd-154">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="b59dd-155">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b59dd-155">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "http://bing.com"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="b59dd-156">Omdat deze bewerking lang is wordt uitgevoerd, Hallo URI voor Hallo resultaat geretourneerd als Hallo antwoordheader zoals weergegeven in het volgende antwoord Hallo:</span><span class="sxs-lookup"><span data-stu-id="b59dd-156">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="b59dd-157">**Belangrijke waarden**</span><span class="sxs-lookup"><span data-stu-id="b59dd-157">**Important Values**</span></span>

* <span data-ttu-id="b59dd-158">**Locatie** -deze eigenschap bevat Hallo URI waar Hallo resultaten zijn wanneer hello bewerking is voltooid</span><span class="sxs-lookup"><span data-stu-id="b59dd-158">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: e49b12c7-c232-472c-b6d2-6c257ce80fa5
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/e49b12c7-c232-472c-b6d2-6c257ce80fa5?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: c3d9744f-5683-427d-bdd1-636b68ab01b6
x-ms-routing-request-id: WESTUS:20170602T203101Z:c3d9744f-5683-427d-bdd1-636b68ab01b6
Date: Fri, 02 Jun 2017 20:31:00 GMT

null
```

### <a name="response"></a><span data-ttu-id="b59dd-159">Antwoord</span><span class="sxs-lookup"><span data-stu-id="b59dd-159">Response</span></span>

<span data-ttu-id="b59dd-160">In Hallo antwoord te volgen, ziet u Hallo `connectionStatus` wordt weergegeven als **bereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="b59dd-160">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="b59dd-161">Als een verbinding geslaagd is, zijn latentie waarden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b59dd-161">When a connection is successful, latency values are provided.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "204.79.197.200",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="b59dd-162">Controleer de connectiviteit tooa opslag eindpunt</span><span class="sxs-lookup"><span data-stu-id="b59dd-162">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="b59dd-163">Hallo volgende voorbeeld wordt gecontroleerd Hallo verbinding hebben met een virtuele machine tooa blog van storage-account.</span><span class="sxs-lookup"><span data-stu-id="b59dd-163">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="b59dd-164">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b59dd-164">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "https://build2017nwdiag360.blob.core.windows.net/"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="b59dd-165">Omdat deze bewerking lang is wordt uitgevoerd, Hallo URI voor Hallo resultaat geretourneerd als Hallo antwoordheader zoals weergegeven in het volgende antwoord Hallo:</span><span class="sxs-lookup"><span data-stu-id="b59dd-165">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="b59dd-166">**Belangrijke waarden**</span><span class="sxs-lookup"><span data-stu-id="b59dd-166">**Important Values**</span></span>

* <span data-ttu-id="b59dd-167">**Locatie** -deze eigenschap bevat Hallo URI waar Hallo resultaten zijn wanneer hello bewerking is voltooid</span><span class="sxs-lookup"><span data-stu-id="b59dd-167">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
x-ms-routing-request-id: WESTUS2:20170602T200504Z:93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
Date: Fri, 02 Jun 2017 20:05:03 GMT

null
```

### <a name="response"></a><span data-ttu-id="b59dd-168">Antwoord</span><span class="sxs-lookup"><span data-stu-id="b59dd-168">Response</span></span>

<span data-ttu-id="b59dd-169">Hallo is volgende voorbeeld antwoord Hallo Hallo vorige API-aanroep wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b59dd-169">hello following example is hello response from running hello previous API call.</span></span> <span data-ttu-id="b59dd-170">Als het Hallo-controle is geslaagd, Hallo `connectionStatus` eigenschap wordt weergegeven als **bereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="b59dd-170">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="b59dd-171">U vindt Hallo-gegevens met betrekking tot Hallo aantal hops vereist tooreach Hallo storage-blob en latentie.</span><span class="sxs-lookup"><span data-stu-id="b59dd-171">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "13.71.200.248",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="next-steps"></a><span data-ttu-id="b59dd-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b59dd-172">Next steps</span></span>

<span data-ttu-id="b59dd-173">Meer informatie over hoe tooautomate pakket worden vastgelegd met waarschuwingen van de virtuele machine door [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="b59dd-173">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="b59dd-174">Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b59dd-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














