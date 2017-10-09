---
title: aaaManage netwerk beveiliging groep overgebracht logboeken met Azure-netwerk-Watcher - PowerShell | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toomanage netwerk beveiliging groep overgebracht wordt geregistreerd in Azure-netwerk-Watcher met PowerShell
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
ms.openlocfilehash: 987e8728fb6459fd6ff8eb5cd3d36ff855f2ccfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-powershell"></a>Netwerk beveiliging groep overgebracht logboeken configureren met PowerShell

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

Netwerkbeveiligingsgroep stroom logboeken zijn een functie van netwerk-Watcher waarmee u tooview informatie over inkomende en uitgaande IP-verkeer via een Netwerkbeveiligingsgroep. Deze stroom logboeken zijn geschreven in json-indeling en weergeven van uitgaande en inkomende stromen per regel op basis van een Hallo NIC Hallo stroom is van toepassing op 5-tuple informatie over het Hallo-stroom (bron/het doel-IP, bron/het doel-poort, het Protocol) en als hello verkeer is toegestaan of geweigerd.

## <a name="register-insights-provider"></a>Insights provider registreren

Opdat stroom Hallo logboekregistratie toowork, **Microsoft.Insights** provider moet worden geregistreerd. Als u niet zeker weet of hello **Microsoft.Insights** -provider is geregistreerd, voert hello volgende script.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>Netwerkbeveiligingsgroep inschakelen stroom Logboeken

Hallo opdracht tooenable stroom Logboeken wordt weergegeven in Hallo voorbeeld te volgen:

```powershell
$NW = Get-AzurermNetworkWatcher -ResourceGroupName NetworkWatcherRg -Name NetworkWatcher_westcentralus
$nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName nsgRG-Name nsgName
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName StorageRG -Name contosostorage123
Get-AzureRmNetworkWatcherFlowLogStatus -NetworkWatcher $NW -TargetResourceId $nsg.Id
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $true
```

## <a name="disable-network-security-group-flow-logs"></a>Netwerkbeveiligingsgroep uitschakelen stroom Logboeken

Gebruik Hallo voorbeeld toodisable stroom logboeken te volgen:

```powershell
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $false
```

## <a name="download-a-flow-log"></a>Downloaden van een stroom-logboek

Hallo-opslaglocatie van een stroom-logboek is gedefinieerd bij het maken. Een handig hulpmiddel tooaccess deze stroom logboeken die zijn opgeslagen tooa storage-account is Microsoft Azure Storage Explorer, die u kunt hier downloaden: http://storageexplorer.com/

Als een opslagaccount is opgegeven, worden bestanden voor pakket tooa storage-account op Hallo na locatie opgeslagen:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Vindt u informatie over de structuur van logboek Hallo Hallo [netwerk beveiliging groep overgebracht logboek overzicht](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe te[visualiseren van uw NSG stroom logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

Meer informatie over hoe te[visualiseren van uw NSG stroom logboeken met open-source hulpprogramma's](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
