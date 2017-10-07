---
title: aaaManage Netwerkbeveiligingsgroep stroom logboeken met Azure-netwerk-Watcher - REST-API | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toomanage Netwerkbeveiligingsgroep stroom wordt geregistreerd in Azure-netwerk-Watcher met REST-API
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2ab25379-0fd3-4bfe-9d82-425dfc7ad6bb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: be81e35f4d01c67efef99773e9b4e2ae4b8e209e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="6bca9-103">Configureren van Netwerkbeveiligingsgroep stroom logboeken met REST-API</span><span class="sxs-lookup"><span data-stu-id="6bca9-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6bca9-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6bca9-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="6bca9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bca9-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="6bca9-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6bca9-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="6bca9-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6bca9-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="6bca9-108">REST API</span><span class="sxs-lookup"><span data-stu-id="6bca9-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="6bca9-109">Netwerkbeveiligingsgroep stroom logboeken zijn een functie van netwerk-Watcher waarmee u tooview informatie over inkomende en uitgaande IP-verkeer via een Netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="6bca9-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="6bca9-110">Deze stroom logboeken zijn geschreven in json-indeling en weergeven van uitgaande en inkomende stromen per regel op basis van een Hallo NIC Hallo stroom is van toepassing op 5-tuple informatie over het Hallo-stroom (bron/het doel-IP, bron/het doel-poort, het Protocol) en als hello verkeer is toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="6bca9-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6bca9-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="6bca9-111">Before you begin</span></span>

<span data-ttu-id="6bca9-112">ARMclient is gebruikte toocall Hallo REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6bca9-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="6bca9-113">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="6bca9-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="6bca9-114">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="6bca9-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="6bca9-115">Voor de REST-API voor netwerk-Watcher Hallo aanroepen Resourcegroepnaam in Hallo aanvraag-URI is Hallo-resourcegroep met Hallo netwerk-Watcher niet Hallo-bronnen zoals u Hallo diagnostische acties uitvoert op.</span><span class="sxs-lookup"><span data-stu-id="6bca9-115">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="6bca9-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="6bca9-116">Scenario</span></span>

<span data-ttu-id="6bca9-117">Hallo-scenario die in dit artikel wordt beschreven hoe tooenable, uitschakelen en query stromen logboeken met behulp van Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="6bca9-117">hello scenario covered in this article shows you how tooenable, disable, and query flow logs using hello REST API.</span></span> <span data-ttu-id="6bca9-118">toolearn meer informatie over de Netwerkbeveiligingsgroep stroom loggings, gaat u naar [Netwerkbeveiligingsgroep stroom logboekregistratie - overzicht](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6bca9-118">toolearn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="6bca9-119">U wordt in dit scenario:</span><span class="sxs-lookup"><span data-stu-id="6bca9-119">In this scenario, you will:</span></span>

* <span data-ttu-id="6bca9-120">Stroom Logboeken inschakelen</span><span class="sxs-lookup"><span data-stu-id="6bca9-120">Enable flow logs</span></span>
* <span data-ttu-id="6bca9-121">Stroom Logboeken uitschakelen</span><span class="sxs-lookup"><span data-stu-id="6bca9-121">Disable flow logs</span></span>
* <span data-ttu-id="6bca9-122">Status logboeken van de stroom</span><span class="sxs-lookup"><span data-stu-id="6bca9-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="6bca9-123">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="6bca9-123">Log in with ARMClient</span></span>

<span data-ttu-id="6bca9-124">Meld u bij tooarmclient met uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="6bca9-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="6bca9-125">Insights provider registreren</span><span class="sxs-lookup"><span data-stu-id="6bca9-125">Register Insights provider</span></span>

<span data-ttu-id="6bca9-126">Opdat stroom Hallo logboekregistratie toowork, **Microsoft.Insights** provider moet worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="6bca9-126">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="6bca9-127">Als u niet zeker weet of hello **Microsoft.Insights** -provider is geregistreerd, voert hello volgende script.</span><span class="sxs-lookup"><span data-stu-id="6bca9-127">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="6bca9-128">Netwerkbeveiligingsgroep inschakelen stroom Logboeken</span><span class="sxs-lookup"><span data-stu-id="6bca9-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="6bca9-129">Hallo opdracht tooenable stroom Logboeken wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="6bca9-129">hello command tooenable flow logs is shown in hello following example:</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'true',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="6bca9-130">Hallo-antwoord geretourneerd van Hallo voorgaande voorbeeld is als volgt:</span><span class="sxs-lookup"><span data-stu-id="6bca9-130">hello response returned from hello preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="6bca9-131">Netwerkbeveiligingsgroep uitschakelen stroom Logboeken</span><span class="sxs-lookup"><span data-stu-id="6bca9-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="6bca9-132">Gebruik hello voorbeeld toodisable stroom logboeken te volgen.</span><span class="sxs-lookup"><span data-stu-id="6bca9-132">Use hello following example toodisable flow logs.</span></span> <span data-ttu-id="6bca9-133">Hallo aanroep is hetzelfde als het inschakelen van Logboeken van de stroom, met uitzondering van Hallo **false** is ingesteld voor de eigenschap Hallo ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6bca9-133">hello call is hello same as enabling flow logs, except **false** is set for hello enabled property.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'false',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="6bca9-134">Hallo-antwoord geretourneerd van Hallo voorgaande voorbeeld is als volgt:</span><span class="sxs-lookup"><span data-stu-id="6bca9-134">hello response returned from hello preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": false,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="query-flow-logs"></a><span data-ttu-id="6bca9-135">Query stroom Logboeken</span><span class="sxs-lookup"><span data-stu-id="6bca9-135">Query flow logs</span></span>

<span data-ttu-id="6bca9-136">Hallo REST-aanroep query's de status van de stroom Hallo na een Netwerkbeveiligingsgroep zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="6bca9-136">hello following REST call queries hello status of flow logs on a Network Security Group.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/queryFlowLogStatus?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="6bca9-137">Hallo Hieronder volgt een voorbeeld van Hallo-antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="6bca9-137">hello following is an example of hello response returned:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
   "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="download-a-flow-log"></a><span data-ttu-id="6bca9-138">Downloaden van een stroom-logboek</span><span class="sxs-lookup"><span data-stu-id="6bca9-138">Download a flow log</span></span>

<span data-ttu-id="6bca9-139">Hallo-opslaglocatie van een stroom-logboek is gedefinieerd bij het maken.</span><span class="sxs-lookup"><span data-stu-id="6bca9-139">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="6bca9-140">Een handig hulpmiddel tooaccess deze stroom logboeken die zijn opgeslagen tooa storage-account is Microsoft Azure Storage Explorer, die u kunt hier downloaden: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="6bca9-140">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="6bca9-141">Als een opslagaccount is opgegeven, worden bestanden voor pakket tooa storage-account op Hallo na locatie opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="6bca9-141">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="6bca9-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6bca9-142">Next steps</span></span>

<span data-ttu-id="6bca9-143">Meer informatie over hoe te[visualiseren van uw NSG stroom logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="6bca9-143">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="6bca9-144">Meer informatie over hoe te[visualiseren van uw NSG stroom logboeken met open-source hulpprogramma's](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="6bca9-144">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
