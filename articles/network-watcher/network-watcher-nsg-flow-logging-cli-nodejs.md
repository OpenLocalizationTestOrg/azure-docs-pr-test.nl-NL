---
title: Logboeken met Azure-netwerk-Watcher - Azure CLI 1.0 netwerk beveiliging groep overgebracht beheren | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe u Logboeken netwerk beveiliging groep overgebracht in Azure-netwerk-Watcher met Azure CLI 1.0 beheren
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ea8543857c062e76f96da99fb295ce831c3c5f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a><span data-ttu-id="8cdb2-103">Netwerk beveiliging groep overgebracht logboeken configureren met Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8cdb2-103">Configuring Network Security Group Flow logs with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8cdb2-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8cdb2-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="8cdb2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cdb2-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="8cdb2-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8cdb2-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="8cdb2-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8cdb2-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="8cdb2-108">REST API</span><span class="sxs-lookup"><span data-stu-id="8cdb2-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="8cdb2-109">Netwerkbeveiligingsgroep stroom logboeken zijn een functie van netwerk-Watcher waarmee u informatie bekijken over inkomende en uitgaande IP-verkeer via een Netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="8cdb2-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="8cdb2-110">Deze stroom logboeken zijn geschreven in json-indeling en binnenkomende en uitgaande stromen weergeven op basis van een per regel, de NIC die de stroom van toepassing, 5-tuple informatie over de stroom (bron/het doel-IP, bron/het doel-poort, het Protocol) en als het verkeer is toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="8cdb2-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="8cdb2-111">Dit artikel wordt platformoverschrijdende Azure CLI 1.0 gebruikt die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="8cdb2-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="8cdb2-112">Netwerk-Watcher gebruikt momenteel de Azure CLI 1.0 voor CLI-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="8cdb2-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="8cdb2-113">Insights provider registreren</span><span class="sxs-lookup"><span data-stu-id="8cdb2-113">Register Insights provider</span></span>

<span data-ttu-id="8cdb2-114">Stroom logboekregistratie om te werken, zodat de **Microsoft.Insights** provider moet worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="8cdb2-114">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="8cdb2-115">Als u niet zeker weet of de **Microsoft.Insights** provider is geregistreerd, voer het volgende script.</span><span class="sxs-lookup"><span data-stu-id="8cdb2-115">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="8cdb2-116">Netwerkbeveiligingsgroep inschakelen stroom Logboeken</span><span class="sxs-lookup"><span data-stu-id="8cdb2-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="8cdb2-117">De opdracht uit om Logboeken van de stroom wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8cdb2-117">The command to enable flow logs is shown in the following example:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="8cdb2-118">Netwerkbeveiligingsgroep uitschakelen stroom Logboeken</span><span class="sxs-lookup"><span data-stu-id="8cdb2-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="8cdb2-119">Gebruik het volgende voorbeeld stroom Logboeken uitschakelen:</span><span class="sxs-lookup"><span data-stu-id="8cdb2-119">Use the following example to disable flow logs:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="8cdb2-120">Downloaden van een stroom-logboek</span><span class="sxs-lookup"><span data-stu-id="8cdb2-120">Download a Flow log</span></span>

<span data-ttu-id="8cdb2-121">De locatie voor de opslag van een stroom-logboek is gedefinieerd bij het maken.</span><span class="sxs-lookup"><span data-stu-id="8cdb2-121">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="8cdb2-122">Een handig hulpmiddel voor toegang tot deze stroom logboeken opgeslagen naar een opslagaccount is Microsoft Azure Storage Explorer, die u kunt hier downloaden: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="8cdb2-122">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="8cdb2-123">Als een opslagaccount is opgegeven, worden bestanden voor pakket worden opgeslagen in een opslagaccount op de volgende locatie:</span><span class="sxs-lookup"><span data-stu-id="8cdb2-123">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="8cdb2-124">Ga naar voor informatie over de structuur van het logboek [netwerk beveiliging groep overgebracht logboek overzicht](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8cdb2-124">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8cdb2-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8cdb2-125">Next Steps</span></span>

<span data-ttu-id="8cdb2-126">Meer informatie over hoe [visualiseren van uw NSG stroom logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="8cdb2-126">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="8cdb2-127">Meer informatie over hoe [visualiseren van uw NSG stroom logboeken met open-source hulpprogramma's](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="8cdb2-127">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
