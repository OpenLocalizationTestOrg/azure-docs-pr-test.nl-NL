---
title: Controleer de verbinding met Azure-netwerk-Watcher - Azure-portal | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe u connectiviteit met de netwerk-Watcher in de Azure portal controleren
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
ms.openlocfilehash: ca62bea581acb59d3c3c0b8a204cc9d42de2b27f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-the-azure-portal"></a><span data-ttu-id="9544e-103">Controleer de verbinding met de netwerk-Watcher van Azure met Azure portal</span><span class="sxs-lookup"><span data-stu-id="9544e-103">Check connectivity with Azure Network Watcher using the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9544e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="9544e-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="9544e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9544e-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="9544e-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9544e-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="9544e-107">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="9544e-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="9544e-108">Informatie over het gebruik van verbinding om te controleren als direct TCP-verbinding van een virtuele machine naar een opgegeven eindpunt kan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9544e-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9544e-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="9544e-109">Before you begin</span></span>

<span data-ttu-id="9544e-110">In dit artikel wordt ervan uitgegaan dat u hebt de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="9544e-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="9544e-111">Een exemplaar van netwerk-Watcher in de regio die u wilt controleren, connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="9544e-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="9544e-112">Virtuele machines connectiviteit met controleren.</span><span class="sxs-lookup"><span data-stu-id="9544e-112">Virtual machines to check connectivity with.</span></span>

<span data-ttu-id="9544e-113">ARMclient wordt gebruikt voor het aanroepen van de REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9544e-113">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="9544e-114">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="9544e-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="9544e-115">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="9544e-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="9544e-116">Controle van de verbinding zijn nodig voor de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="9544e-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="9544e-117">Voor het installeren van de extensie op een Windows-virtuele machine gaat u naar [extensie voor het virtuele machine voor Windows Azure-netwerk-Watcher Agent](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="9544e-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="9544e-118">Registreren van de preview-mogelijkheden</span><span class="sxs-lookup"><span data-stu-id="9544e-118">Register the preview capability</span></span>

<span data-ttu-id="9544e-119">Controle van de verbinding is momenteel in de openbare preview, voor deze functie moet worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="9544e-119">Connectivity check is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="9544e-120">Voer hiervoor de volgende PowerShell-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9544e-120">To do this, run the following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="9544e-121">Om te controleren of dat de registratie is gelukt, voert u het volgende Powershell-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9544e-121">To verify the registration was successful, run the following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="9544e-122">Als de functie juist is geregistreerd, de uitvoer moet overeenkomen met het volgende:</span><span class="sxs-lookup"><span data-stu-id="9544e-122">If the feature was properly registered, the output should match the following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="9544e-123">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="9544e-123">Log in with ARMClient</span></span>

<span data-ttu-id="9544e-124">Aanmelden bij armclient met uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="9544e-124">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="9544e-125">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="9544e-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="9544e-126">Voer het volgende script om te retourneren van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9544e-126">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="9544e-127">Deze informatie is nodig voor het uitvoeren van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="9544e-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="9544e-128">De volgende code moet waarden voor de volgende variabelen:</span><span class="sxs-lookup"><span data-stu-id="9544e-128">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="9544e-129">**subscriptionId** -de abonnements-ID te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9544e-129">**subscriptionId** - The subscription ID to use.</span></span>
- <span data-ttu-id="9544e-130">**resourceGroupName** -de naam van een resourcegroep die virtuele machines bevatten.</span><span class="sxs-lookup"><span data-stu-id="9544e-130">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="9544e-131">De ID van de virtuele machine wordt gebruikt van de volgende uitvoer in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9544e-131">From the following output, the ID of the virtual machine is used in the following example:</span></span>

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

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="9544e-132">Controleer de verbinding met een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="9544e-132">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="9544e-133">In dit voorbeeld controleert de verbinding met een doel-virtuele machine via poort 80.</span><span class="sxs-lookup"><span data-stu-id="9544e-133">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="9544e-134">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="9544e-134">Example</span></span>

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

<span data-ttu-id="9544e-135">Omdat deze bewerking lang actief is, de URI het resultaat wordt geretourneerd als de antwoordheader zoals weergegeven in het volgende antwoord:</span><span class="sxs-lookup"><span data-stu-id="9544e-135">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="9544e-136">**Belangrijke waarden**</span><span class="sxs-lookup"><span data-stu-id="9544e-136">**Important Values**</span></span>

* <span data-ttu-id="9544e-137">**Locatie** -deze eigenschap bevat de URI waar de resultaten zijn wanneer de bewerking voltooid is</span><span class="sxs-lookup"><span data-stu-id="9544e-137">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="response"></a><span data-ttu-id="9544e-138">Antwoord</span><span class="sxs-lookup"><span data-stu-id="9544e-138">Response</span></span>

<span data-ttu-id="9544e-139">Het antwoord van de volgende is van het vorige voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9544e-139">The following response is from the previous example.</span></span>  <span data-ttu-id="9544e-140">In dit antwoord de `ConnectionStatus` is **onbereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="9544e-140">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="9544e-141">U kunt zien dat alle tests mislukte verzonden.</span><span class="sxs-lookup"><span data-stu-id="9544e-141">You can see that all the probes sent failed.</span></span> <span data-ttu-id="9544e-142">De verbinding is mislukt bij het virtuele apparaat als gevolg van een gebruiker geconfigureerde `NetworkSecurityRule` met de naam **UserRule_Port80**, is geconfigureerd voor het blokkeren van inkomend verkeer op poort 80.</span><span class="sxs-lookup"><span data-stu-id="9544e-142">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="9544e-143">Deze informatie kan worden gebruikt om te onderzoeken verbindingsproblemen.</span><span class="sxs-lookup"><span data-stu-id="9544e-143">This information can be used to research connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="9544e-144">Problemen met routing valideren</span><span class="sxs-lookup"><span data-stu-id="9544e-144">Validate routing issues</span></span>

<span data-ttu-id="9544e-145">Het voorbeeld wordt de verbinding tussen een virtuele machine en een extern eindpunt.</span><span class="sxs-lookup"><span data-stu-id="9544e-145">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="9544e-146">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="9544e-146">Example</span></span>

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

<span data-ttu-id="9544e-147">Omdat deze bewerking lang actief is, de URI het resultaat wordt geretourneerd als de antwoordheader zoals weergegeven in het volgende antwoord:</span><span class="sxs-lookup"><span data-stu-id="9544e-147">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="9544e-148">**Belangrijke waarden**</span><span class="sxs-lookup"><span data-stu-id="9544e-148">**Important Values**</span></span>

* <span data-ttu-id="9544e-149">**Locatie** -deze eigenschap bevat de URI waar de resultaten zijn wanneer de bewerking voltooid is</span><span class="sxs-lookup"><span data-stu-id="9544e-149">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="response"></a><span data-ttu-id="9544e-150">Antwoord</span><span class="sxs-lookup"><span data-stu-id="9544e-150">Response</span></span>

<span data-ttu-id="9544e-151">In het volgende voorbeeld wordt de `connectionStatus` wordt weergegeven als **onbereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="9544e-151">In the following example, the `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="9544e-152">In de `hops` details, kunt u zien onder `issues` dat het verkeer is geblokkeerd vanwege een `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="9544e-152">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span>

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

## <a name="check-website-latency"></a><span data-ttu-id="9544e-153">Latentie van de website controleren</span><span class="sxs-lookup"><span data-stu-id="9544e-153">Check website latency</span></span>

<span data-ttu-id="9544e-154">Het volgende voorbeeld wordt de verbinding met een website.</span><span class="sxs-lookup"><span data-stu-id="9544e-154">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="9544e-155">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="9544e-155">Example</span></span>

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

<span data-ttu-id="9544e-156">Omdat deze bewerking lang actief is, de URI het resultaat wordt geretourneerd als de antwoordheader zoals weergegeven in het volgende antwoord:</span><span class="sxs-lookup"><span data-stu-id="9544e-156">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="9544e-157">**Belangrijke waarden**</span><span class="sxs-lookup"><span data-stu-id="9544e-157">**Important Values**</span></span>

* <span data-ttu-id="9544e-158">**Locatie** -deze eigenschap bevat de URI waar de resultaten zijn wanneer de bewerking voltooid is</span><span class="sxs-lookup"><span data-stu-id="9544e-158">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="response"></a><span data-ttu-id="9544e-159">Antwoord</span><span class="sxs-lookup"><span data-stu-id="9544e-159">Response</span></span>

<span data-ttu-id="9544e-160">In het volgende antwoord ziet u de `connectionStatus` wordt weergegeven als **bereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="9544e-160">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="9544e-161">Als een verbinding geslaagd is, zijn latentie waarden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9544e-161">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="9544e-162">Controleer de verbinding met een opslag-eindpunt</span><span class="sxs-lookup"><span data-stu-id="9544e-162">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="9544e-163">Het volgende voorbeeld wordt de verbinding van een virtuele machine met een blog van storage-account.</span><span class="sxs-lookup"><span data-stu-id="9544e-163">The following example checks the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="9544e-164">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="9544e-164">Example</span></span>

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

<span data-ttu-id="9544e-165">Omdat deze bewerking lang actief is, de URI het resultaat wordt geretourneerd als de antwoordheader zoals weergegeven in het volgende antwoord:</span><span class="sxs-lookup"><span data-stu-id="9544e-165">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="9544e-166">**Belangrijke waarden**</span><span class="sxs-lookup"><span data-stu-id="9544e-166">**Important Values**</span></span>

* <span data-ttu-id="9544e-167">**Locatie** -deze eigenschap bevat de URI waar de resultaten zijn wanneer de bewerking voltooid is</span><span class="sxs-lookup"><span data-stu-id="9544e-167">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="response"></a><span data-ttu-id="9544e-168">Antwoord</span><span class="sxs-lookup"><span data-stu-id="9544e-168">Response</span></span>

<span data-ttu-id="9544e-169">Het volgende voorbeeld is de reactie van de vorige API-aanroep uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9544e-169">The following example is the response from running the previous API call.</span></span> <span data-ttu-id="9544e-170">Als de controle geslaagd is, de `connectionStatus` eigenschap wordt weergegeven als **bereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="9544e-170">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="9544e-171">U vindt de details met betrekking tot het aantal hops is vereist voor het bereiken van de storage-blob en latentie.</span><span class="sxs-lookup"><span data-stu-id="9544e-171">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9544e-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9544e-172">Next steps</span></span>

<span data-ttu-id="9544e-173">Meer informatie over het automatiseren van pakket opnamen met waarschuwingen van de virtuele machine met weer te geven [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="9544e-173">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="9544e-174">Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9544e-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














