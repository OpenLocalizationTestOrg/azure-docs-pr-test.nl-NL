---
title: aaaManage netwerk beveiliging groep overgebracht logboeken met Azure-netwerk-Watcher - Azure CLI | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toomanage netwerk beveiliging groep overgebracht wordt geregistreerd in Azure-netwerk-Watcher met Azure CLI
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
ms.openlocfilehash: 2d0b02e7d0a5a9ab20beb491d49a5747f976a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a><span data-ttu-id="6ac8c-103">Netwerk beveiliging groep overgebracht logboeken configureren met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6ac8c-103">Configuring Network Security Group Flow logs with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6ac8c-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6ac8c-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="6ac8c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ac8c-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="6ac8c-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6ac8c-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="6ac8c-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6ac8c-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="6ac8c-108">REST API</span><span class="sxs-lookup"><span data-stu-id="6ac8c-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="6ac8c-109">Netwerkbeveiligingsgroep stroom logboeken zijn een functie van netwerk-Watcher waarmee u tooview informatie over inkomende en uitgaande IP-verkeer via een Netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="6ac8c-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="6ac8c-110">Deze stroom logboeken zijn geschreven in json-indeling en weergeven van uitgaande en inkomende stromen per regel op basis van een Hallo NIC Hallo stroom is van toepassing op 5-tuple informatie over het Hallo-stroom (bron/het doel-IP, bron/het doel-poort, het Protocol) en als hello verkeer is toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="6ac8c-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="6ac8c-111">In dit artikel gebruikt de volgende generatie CLI voor Hallo resource management-implementatiemodel, Azure CLI 2.0, die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="6ac8c-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="6ac8c-112">tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="6ac8c-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="6ac8c-113">Insights provider registreren</span><span class="sxs-lookup"><span data-stu-id="6ac8c-113">Register Insights provider</span></span>

<span data-ttu-id="6ac8c-114">Opdat stroom Hallo logboekregistratie toowork, **Microsoft.Insights** provider moet worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="6ac8c-114">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="6ac8c-115">Als u niet zeker weet of hello **Microsoft.Insights** -provider is geregistreerd, voert hello volgende script.</span><span class="sxs-lookup"><span data-stu-id="6ac8c-115">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="6ac8c-116">Netwerkbeveiligingsgroep inschakelen stroom Logboeken</span><span class="sxs-lookup"><span data-stu-id="6ac8c-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="6ac8c-117">Hallo opdracht tooenable stroom Logboeken wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="6ac8c-117">hello command tooenable flow logs is shown in hello following example:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="6ac8c-118">Netwerkbeveiligingsgroep uitschakelen stroom Logboeken</span><span class="sxs-lookup"><span data-stu-id="6ac8c-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="6ac8c-119">Gebruik Hallo voorbeeld toodisable stroom logboeken te volgen:</span><span class="sxs-lookup"><span data-stu-id="6ac8c-119">Use hello following example toodisable flow logs:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a><span data-ttu-id="6ac8c-120">Downloaden van een stroom-logboek</span><span class="sxs-lookup"><span data-stu-id="6ac8c-120">Download a Flow log</span></span>

<span data-ttu-id="6ac8c-121">Hallo-opslaglocatie van een stroom-logboek is gedefinieerd bij het maken.</span><span class="sxs-lookup"><span data-stu-id="6ac8c-121">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="6ac8c-122">Een handig hulpmiddel tooaccess deze stroom logboeken die zijn opgeslagen tooa storage-account is Microsoft Azure Storage Explorer, die u kunt hier downloaden: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="6ac8c-122">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="6ac8c-123">Als een opslagaccount is opgegeven, worden bestanden voor pakket tooa storage-account op Hallo na locatie opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="6ac8c-123">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="6ac8c-124">Vindt u informatie over de structuur van logboek Hallo Hallo [netwerk beveiliging groep overgebracht logboek overzicht](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6ac8c-124">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ac8c-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6ac8c-125">Next Steps</span></span>

<span data-ttu-id="6ac8c-126">Meer informatie over hoe te[visualiseren van uw NSG stroom logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="6ac8c-126">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="6ac8c-127">Meer informatie over hoe te[visualiseren van uw NSG stroom logboeken met open-source hulpprogramma's](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="6ac8c-127">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
