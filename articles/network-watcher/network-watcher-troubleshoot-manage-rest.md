---
title: aaaTroubleshoot virtuele netwerkgateway en verbindingen met behulp van Azure-netwerk-Watcher - REST | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe PLAATST u de virtuele netwerkgateways tootroubleshoot en verbindingen met het gebruik van Azure-netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e4d5f195-b839-4394-94ef-a04192766e55
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: cc89b46643fdbfefe53727b45d6b7d06914b58a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="2b36d-103">Problemen met virtuele netwerkgateway en verbindingen met behulp van Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="2b36d-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2b36d-104">Portal</span><span class="sxs-lookup"><span data-stu-id="2b36d-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="2b36d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b36d-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="2b36d-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2b36d-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="2b36d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2b36d-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="2b36d-108">REST API</span><span class="sxs-lookup"><span data-stu-id="2b36d-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="2b36d-109">Netwerk-Watcher biedt veel mogelijkheden met betrekking toounderstanding uw netwerkbronnen in Azure.</span><span class="sxs-lookup"><span data-stu-id="2b36d-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="2b36d-110">Een van deze mogelijkheden resource is het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="2b36d-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="2b36d-111">Het oplossen van bron kan worden aangeroepen via Hallo-portal, PowerShell, CLI of REST-API.</span><span class="sxs-lookup"><span data-stu-id="2b36d-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="2b36d-112">Als deze wordt aangeroepen, netwerk-Watcher Hallo status van de Gateway van een virtueel netwerk of een verbinding inspecteert en retourneert de bevindingen zijn.</span><span class="sxs-lookup"><span data-stu-id="2b36d-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="2b36d-113">In dit artikel leert u Hallo verschillende beheertaken uitvoeren die momenteel beschikbaar zijn voor het oplossen van resource.</span><span class="sxs-lookup"><span data-stu-id="2b36d-113">This article takes you through hello different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="2b36d-114">**Problemen met een virtuele netwerkgateway**</span><span class="sxs-lookup"><span data-stu-id="2b36d-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="2b36d-115">**Problemen met een verbinding**</span><span class="sxs-lookup"><span data-stu-id="2b36d-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="2b36d-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="2b36d-116">Before you begin</span></span>

<span data-ttu-id="2b36d-117">ARMclient is gebruikte toocall Hallo REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2b36d-117">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="2b36d-118">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="2b36d-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="2b36d-119">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="2b36d-119">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="2b36d-120">Voor een lijst met ondersteunde gateway typen bezoek, [ondersteund gatewaytypen](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="2b36d-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="2b36d-121">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2b36d-121">Overview</span></span>

<span data-ttu-id="2b36d-122">Netwerk-Watcher Probleemoplossing biedt Hallo mogelijkheid oplossen van problemen die zich bij het virtuele netwerk gateways en verbindingen voordoen.</span><span class="sxs-lookup"><span data-stu-id="2b36d-122">Network Watcher troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="2b36d-123">Wanneer een aanvraag wordt gedaan toohello resource probleemoplossing logboeken query wordt uitgevoerd en gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="2b36d-123">When a request is made toohello resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="2b36d-124">Als controle voltooid is, worden Hallo resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="2b36d-124">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="2b36d-125">Hallo oplossen API-aanvragen zijn lange aanvragen die meerdere minuten tooreturn een resultaat kon worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2b36d-125">hello troubleshoot API requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="2b36d-126">Logboeken worden opgeslagen in een container voor een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2b36d-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="2b36d-127">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="2b36d-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="2b36d-128">Problemen met een virtuele netwerkgateway</span><span class="sxs-lookup"><span data-stu-id="2b36d-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-hello-troubleshoot-request"></a><span data-ttu-id="2b36d-129">POST Hallo aanvraag oplossen</span><span class="sxs-lookup"><span data-stu-id="2b36d-129">POST hello troubleshoot request</span></span>

<span data-ttu-id="2b36d-130">Hallo voorbeeld query's Hallo status van een virtuele netwerkgateway te volgen.</span><span class="sxs-lookup"><span data-stu-id="2b36d-130">hello following example queries hello status of a Virtual Network gateway.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$vnetGatewayName = "ContosoVNETGateway"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @"
{
'TargetResourceId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/virtualNetworkGateways/${vnetGatewayName}',
'Properties': {
'StorageId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}',
'StoragePath': 'https://${storageAccountName}.blob.core.windows.net/${containerName}'
}
}
"@

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

<span data-ttu-id="2b36d-131">Omdat deze bewerking lang hello URI voor het uitvoeren van query's Hallo-bewerking wordt uitgevoerd, en Hallo URI voor Hallo resultaat wordt geretourneerd als Hallo antwoordheader zoals weergegeven in het volgende antwoord Hallo:</span><span class="sxs-lookup"><span data-stu-id="2b36d-131">Since this operation is long running, hello URI for querying hello operation and hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="2b36d-132">**Belangrijke waarden**</span><span class="sxs-lookup"><span data-stu-id="2b36d-132">**Important Values**</span></span>

* <span data-ttu-id="2b36d-133">**Azure-asynchrone bewerking** -deze eigenschap bevat Hallo URI tooquery Hallo asynchrone bewerking oplossen</span><span class="sxs-lookup"><span data-stu-id="2b36d-133">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="2b36d-134">**Locatie** -deze eigenschap bevat Hallo URI waar Hallo resultaten zijn wanneer hello bewerking is voltooid</span><span class="sxs-lookup"><span data-stu-id="2b36d-134">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="2b36d-135">Query uitvoeren op Hallo asynchrone bewerking voor voltooiing</span><span class="sxs-lookup"><span data-stu-id="2b36d-135">Query hello async operation for completion</span></span>

<span data-ttu-id="2b36d-136">Gebruik voor Hallo voortgang van Hallo bewerking Hallo operations URI tooquery zoals te zien is in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="2b36d-136">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="2b36d-137">Tijdens het Hallo-bewerking wordt uitgevoerd, geeft antwoord Hallo **InProgress** zoals gezien in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="2b36d-137">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="2b36d-138">Wanneer is Hallo bewerking voltooid Hallo statuswijzigingen te**geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="2b36d-138">When hello operation is complete hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a><span data-ttu-id="2b36d-139">Hallo resultaten ophalen</span><span class="sxs-lookup"><span data-stu-id="2b36d-139">Retrieve hello results</span></span>

<span data-ttu-id="2b36d-140">Zodra het Hallo-status geretourneerd is **geslaagd**, een GET-methode aanroepen op Hallo operationResult URI tooretrieve Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="2b36d-140">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="2b36d-141">Hallo zijn volgende antwoorden voorbeelden van een typische verslechterde antwoord geretourneerd bij het opvragen van Hallo resultaten van het oplossen van een gateway.</span><span class="sxs-lookup"><span data-stu-id="2b36d-141">hello following responses are examples of a typical degraded response returned when querying hello results of troubleshooting a gateway.</span></span> <span data-ttu-id="2b36d-142">Zie [begrijpen Hallo resultaten](#understanding-the-results) tooget uitleg over welke eigenschappen Hallo in Hallo antwoord gemiddelde.</span><span class="sxs-lookup"><span data-stu-id="2b36d-142">See [Understanding hello results](#understanding-the-results) tooget clarification on what hello properties in hello response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN gateway is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```


## <a name="troubleshoot-connections"></a><span data-ttu-id="2b36d-143">Problemen met verbindingen oplossen</span><span class="sxs-lookup"><span data-stu-id="2b36d-143">Troubleshoot Connections</span></span>

<span data-ttu-id="2b36d-144">Hallo voorbeeld query's Hallo status van een verbinding te volgen.</span><span class="sxs-lookup"><span data-stu-id="2b36d-144">hello following example queries hello status of a Connection.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$connectionName = "VNET2toVNET1Connection"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @{
"TargetResourceId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/connections/${connectionName}",
"Properties": {
"StorageId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}",
"StoragePath": "https://${storageAccountName}.blob.core.windows.net/${containerName}"
}

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

> [!NOTE]
> <span data-ttu-id="2b36d-145">Hallo oplossen bewerking parallel kan niet worden uitgevoerd op een verbinding en de bijbehorende gateways.</span><span class="sxs-lookup"><span data-stu-id="2b36d-145">hello troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="2b36d-146">Hallo-bewerking moet eerdere toorunning voltooien op Hallo vorige resource.</span><span class="sxs-lookup"><span data-stu-id="2b36d-146">hello operation must complete prior toorunning it on hello previous resource.</span></span>

<span data-ttu-id="2b36d-147">Aangezien dit een langdurige transactie in Hallo response-header wordt Hallo URI voor query's in Hallo bewerking en Hallo URI voor Hallo resultaat zoals weergegeven in het volgende antwoord Hallo geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="2b36d-147">Since this is a long running transaction, in hello response header, hello URI for querying hello operation and hello URI for hello result is returned as shown in hello following response:</span></span>

<span data-ttu-id="2b36d-148">**Belangrijke waarden**</span><span class="sxs-lookup"><span data-stu-id="2b36d-148">**Important Values**</span></span>

* <span data-ttu-id="2b36d-149">**Azure-asynchrone bewerking** -deze eigenschap bevat Hallo URI tooquery Hallo asynchrone bewerking oplossen</span><span class="sxs-lookup"><span data-stu-id="2b36d-149">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="2b36d-150">**Locatie** -deze eigenschap bevat Hallo URI waar Hallo resultaten zijn wanneer hello bewerking is voltooid</span><span class="sxs-lookup"><span data-stu-id="2b36d-150">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="2b36d-151">Query uitvoeren op Hallo asynchrone bewerking voor voltooiing</span><span class="sxs-lookup"><span data-stu-id="2b36d-151">Query hello async operation for completion</span></span>

<span data-ttu-id="2b36d-152">Gebruik voor Hallo voortgang van Hallo bewerking Hallo operations URI tooquery zoals te zien is in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="2b36d-152">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="2b36d-153">Tijdens het Hallo-bewerking wordt uitgevoerd, geeft antwoord Hallo **InProgress** zoals gezien in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="2b36d-153">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="2b36d-154">Als Hallo-bewerking voltooid is, Hallo wijzigt de status te**geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="2b36d-154">When hello operation is complete, hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="2b36d-155">Hallo zijn volgende antwoorden voorbeelden van een typische antwoord geretourneerd bij het opvragen van Hallo resultaten van het oplossen van een verbinding.</span><span class="sxs-lookup"><span data-stu-id="2b36d-155">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

### <a name="retrieve-hello-results"></a><span data-ttu-id="2b36d-156">Hallo resultaten ophalen</span><span class="sxs-lookup"><span data-stu-id="2b36d-156">Retrieve hello results</span></span>

<span data-ttu-id="2b36d-157">Zodra het Hallo-status geretourneerd is **geslaagd**, een GET-methode aanroepen op Hallo operationResult URI tooretrieve Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="2b36d-157">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="2b36d-158">Hallo zijn volgende antwoorden voorbeelden van een typische antwoord geretourneerd bij het opvragen van Hallo resultaten van het oplossen van een verbinding.</span><span class="sxs-lookup"><span data-stu-id="2b36d-158">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN Connection is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```

## <a name="understanding-hello-results"></a><span data-ttu-id="2b36d-159">Understanding Hallo resultaten</span><span class="sxs-lookup"><span data-stu-id="2b36d-159">Understanding hello results</span></span>

<span data-ttu-id="2b36d-160">Hallo actietekst bevat algemene richtlijnen over hoe tooresolve probleem Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b36d-160">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="2b36d-161">Als een actie kan worden ondernomen voor Hallo probleem, wordt een koppeling geboden met aanvullende richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="2b36d-161">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="2b36d-162">In geval van Hallo wanneer er geen aanvullende richtlijnen, antwoord Hallo biedt Hallo url tooopen een ondersteuningsaanvraag.</span><span class="sxs-lookup"><span data-stu-id="2b36d-162">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="2b36d-163">Voor meer informatie over het Hallo-eigenschappen van antwoord Hallo en wat is opgenomen, gaat u naar [overzicht van netwerk-Watcher oplossen](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2b36d-163">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="2b36d-164">Voor instructies over het downloaden van bestanden van azure storage-accounts, Raadpleeg te[aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="2b36d-164">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="2b36d-165">Een ander hulpprogramma dat kan worden gebruikt, is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="2b36d-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="2b36d-166">Meer informatie over Opslagverkenner vindt u hier op Hallo koppeling: [Opslagverkenner](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="2b36d-166">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b36d-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2b36d-167">Next steps</span></span>

<span data-ttu-id="2b36d-168">Als de instellingen zijn gewijzigd die stop VPN-verbindingen, raadpleegt u [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="2b36d-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
