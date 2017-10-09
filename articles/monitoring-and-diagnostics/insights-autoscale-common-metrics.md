---
title: Monitor voor automatisch schalen algemene metrische gegevens aaaAzure | Microsoft Docs
description: Meer informatie over welke metrische gegevens vaak worden gebruikt voor automatisch schalen uw Cloudservices, virtuele Machines en Web-Apps.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 189b2a13-01c8-4aca-afd5-90711903ca59
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/6/2016
ms.author: ancav
ms.openlocfilehash: 372a40d72d7a6c22c5ff854b1460ec8a3b7ed1d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a>Azure Monitor automatisch schalen de algemene metrische gegevens
Azure Monitor-automatisch schalen kunt u tooscale Hallo aantal actieve exemplaren omhoog of omlaag, op basis van telemetriegegevens (metrische gegevens). Dit document beschrijft algemene metrische gegevens die u wilt misschien toouse. U kunt in Azure-portal voor Cloudservices en serverfarms Hallo, Hallo meetwaarde van Hallo resource tooscale door. Echter, u kunt ook alle metrische gegevens van een andere resource tooscale door.

Monitor voor automatisch schalen die Azure geldt alleen te[virtuele-Machineschaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Cloudservices](https://azure.microsoft.com/services/cloud-services/), en [App Service - Web-Apps](https://azure.microsoft.com/services/app-service/web/). Andere Azure-services verschillende schalen methoden gebruiken.

## <a name="compute-metrics-for-resource-manager-based-vms"></a>Metrische gegevens voor Resource Manager gebaseerde virtuele machines te berekenen
Standaard verzenden Resource Manager gebaseerde virtuele Machines en virtuele-Machineschaalsets basismetrieken (hostniveau). Bovendien bij het configureren van diagnostische gegevens te verzamelen voor een virtuele machine van Azure en VMSS verzendt Hallo diagnostische Azure-extensie ook prestatiemeteritems guest-OS (bekend als "Guest-OS metrische gegevens").  U gebruikt deze metrische gegevens in de regels voor automatisch schalen.

U kunt Hallo `Get MetricDefinitions` PoSH/API/CLI tooview Hallo metrische gegevens beschikbaar voor uw resource VMSS.

Als u VM-schaalsets en u een bepaalde metriek vermeld niet ziet, dan is het waarschijnlijk *uitgeschakeld* in de extensie voor diagnostische gegevens.

Als een bepaalde waarde niet opgevangen of overgedragen op Hallo frequentie die u wilt wordt, kunt u de configuratie van diagnostische Hallo bijwerken.

Als beide bovenstaande gevallen waar is, controleert u [Gebruik PowerShell tooenable diagnostische Azure-gegevens in een virtuele machine met Windows](../virtual-machines/windows/ps-extensions-diagnostics.md) over PowerShell tooconfigure en werk uw Azure VM Diagnostics extensie tooenable Hallo metriek. Dit artikel bevat ook een voorbeeldbestand voor de configuratie van diagnostische gegevens.

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a>Host metrische gegevens voor Resource Manager gebaseerde Windows- en Linux-machines
Hallo hostniveau metrische gegevens te volgen worden standaard verzonden voor virtuele machine van Azure en VMSS in Windows- en Linux-exemplaren. Deze metrische gegevens van de Azure VM beschreven, maar worden verzameld van hello Azure VM-host in plaats van via agent is geïnstalleerd op Hallo Gast-VM. U kunt deze metrische gegevens in de regels voor automatisch schalen.

- [Host metrische gegevens voor Resource Manager gebaseerde Windows- en Linux-machines](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [Host metrische gegevens voor Resource Manager gebaseerde Windows- en Linux VM-Schaalsets](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a>Gastbesturingssysteem metrische Resource Manager gebaseerde Windows-VM 's
Wanneer u een virtuele machine in Azure maakt, worden diagnostische gegevens wordt ingeschakeld met behulp van Hallo-extensie voor diagnostische gegevens. Hallo-extensie voor diagnostische gegevens verzendt een set van metrische gegevens die afkomstig zijn uit binnen Hallo VM. Dit betekent dat kunt u automatisch schalen van metrische gegevens die niet standaard worden gegenereerd.

U kunt een lijst met Hallo metrische gegevens genereren met behulp van de volgende opdracht in PowerShell Hallo.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

U kunt een waarschuwing voor Hallo metrische gegevens te volgen:

| Metrische naam | Eenheid |
| --- | --- |
| \Processor(_Total)\% Processor Time |Procent |
| \Processor(_Total)\% tijd in beschermde modus |Procent |
| \Processor(_Total)\% tijd in gebruikersmodus |Procent |
| \Processor informatie (_Totaal) \Processor frequentie |Count |
| \System\Processes |Count |
| Het aantal \Thread \Process (_Total) |Count |
| Het aantal \Handle \Process (_Total) |Count |
| \Memory\% toegewezen Bytes In gebruik |Procent |
| \Memory\Available Bytes |Bytes |
| \Memory\Committed bytes |Bytes |
| \Memory\Commit limiet |Bytes |
| \Memory\Pool wisselbaar geheugen: Bytes |Bytes |
| \Memory\Pool wisselbaar geheugen: Bytes |Bytes |
| \PhysicalDisk(_Total)\% schijftijd |Procent |
| \PhysicalDisk(_Total)\% leestijd schijf |Procent |
| \PhysicalDisk(_Total)\% schrijftijd schijf |Procent |
| \PhysicalDisk (_Totaal) \Disk Schijfoverdrachten per seconde |CountPerSecond |
| \PhysicalDisk (_Totaal) \Disk leesbewerkingen per seconde |CountPerSecond |
| \PhysicalDisk (_Totaal) \Disk per seconde |CountPerSecond |
| \PhysicalDisk (_Totaal) \Disk bytes per seconde |BytesPerSecond |
| \PhysicalDisk (_Totaal) \Disk gelezen Bytes per seconde |BytesPerSecond |
| \PhysicalDisk (_Totaal) \Disk geschreven Bytes per seconde |BytesPerSecond |
| \Avg \PhysicalDisk (_Totaal). Wachtrijlengte voor schijf |Count |
| \Avg \PhysicalDisk (_Totaal). Wachtrijlengte voor schijf lezen |Count |
| \Avg \PhysicalDisk (_Totaal). Wachtrijlengte voor schijf schrijven |Count |
| \LogicalDisk(_Total)\% vrije ruimte |Procent |
| \LogicalDisk (_Totaal) \Free megabytes |Count |

### <a name="guest-os-metrics-linux-vms"></a>Gastbesturingssysteem metrische gegevens Linux VM 's
Wanneer u een virtuele machine in Azure maakt, wordt er met behulp van de extensie voor diagnostische gegevens diagnostics standaard ingeschakeld.

U kunt een lijst met Hallo metrische gegevens genereren met behulp van de volgende opdracht in PowerShell Hallo.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 U kunt een waarschuwing voor Hallo metrische gegevens te volgen:

| Metrische naam | Eenheid |
| --- | --- |
| \Memory\AvailableMemory |Bytes |
| \Memory\PercentAvailableMemory |Procent |
| \Memory\UsedMemory |Bytes |
| \Memory\PercentUsedMemory |Procent |
| \Memory\PercentUsedByCache |Procent |
| \Memory\PagesPerSec |CountPerSecond |
| \Memory\PagesReadPerSec |CountPerSecond |
| \Memory\PagesWrittenPerSec |CountPerSecond |
| \Memory\AvailableSwap |Bytes |
| \Memory\PercentAvailableSwap |Procent |
| \Memory\UsedSwap |Bytes |
| \Memory\PercentUsedSwap |Procent |
| \Processor\PercentIdleTime |Procent |
| \Processor\PercentUserTime |Procent |
| \Processor\PercentNiceTime |Procent |
| \Processor\PercentPrivilegedTime |Procent |
| \Processor\PercentInterruptTime |Procent |
| \Processor\PercentDPCTime |Procent |
| \Processor\PercentProcessorTime |Procent |
| \Processor\PercentIOWaitTime |Procent |
| \PhysicalDisk\BytesPerSecond |BytesPerSecond |
| \PhysicalDisk\ReadBytesPerSecond |BytesPerSecond |
| \PhysicalDisk\WriteBytesPerSecond |BytesPerSecond |
| \PhysicalDisk\TransfersPerSecond |CountPerSecond |
| \PhysicalDisk\ReadsPerSecond |CountPerSecond |
| \PhysicalDisk\WritesPerSecond |CountPerSecond |
| \PhysicalDisk\AverageReadTime |Seconden |
| \PhysicalDisk\AverageWriteTime |Seconden |
| \PhysicalDisk\AverageTransferTime |Seconden |
| \PhysicalDisk\AverageDiskQueueLength |Count |
| \NetworkInterface\BytesTransmitted |Bytes |
| \NetworkInterface\BytesReceived |Bytes |
| \NetworkInterface\PacketsTransmitted |Count |
| \NetworkInterface\PacketsReceived |Count |
| \NetworkInterface\BytesTotal |Bytes |
| \NetworkInterface\TotalRxErrors |Count |
| \NetworkInterface\TotalTxErrors |Count |
| \NetworkInterface\TotalCollisions |Count |

## <a name="commonly-used-web-server-farm-metrics"></a>Gangbare metrische gegevens van Web (serverfarm)
U kunt ook automatisch schalen op basis van algemene web server-gegevens zoals Hallo Http-wachtrijlengte uitvoeren. De naam van de meetwaarde is **HttpQueueLength**.  Hallo sectie een lijst met beschikbare serverfarm (Web-Apps) metrische gegevens te volgen.

### <a name="web-apps-metrics"></a>Metrische gegevens van Web-Apps
U kunt een lijst met metrische gegevens Hallo-Web-Apps met behulp van de volgende opdracht in PowerShell Hallo genereren.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

U kunt op een waarschuwing of schalen door deze metrische gegevens.

| Metrische naam | Eenheid |
| --- | --- |
| CpuPercentage |Procent |
| MemoryPercentage |Procent |
| DiskQueueLength |Count |
| HttpQueueLength |Count |
| BytesReceived |Bytes |
| BytesSent |Bytes |

## <a name="commonly-used-storage-metrics"></a>Gangbare metrische gegevens voor opslag
U kunt schalen door wachtrijlengte voor opslag, het aantal berichten in wachtrij voor Hallo opslag Hallo. Wachtrijlengte van Storage is een speciale metriek en Hallo drempelwaarde Hallo aantal berichten per exemplaar is. Bijvoorbeeld, als er twee exemplaren en Hallo drempelwaarde too100 is ingesteld, schalen treedt op wanneer totaal aantal berichten in wachtrij Hallo Hallo 200. Dat kan worden 100 berichten per exemplaar, 120 en 80, of een andere combinatie die too200 of meer opgeteld.

Configureer deze instelling in hello Azure-portal op Hallo **instellingen** blade. U kunt Hallo-instelling voor automatisch schalen in Hallo Resource Manager-sjabloon toouse bijwerken voor VM-schaalsets *metricName* als *ApproximateMessageCount* en het Hallo-ID van de opslagwachtrij Hallo als doorgeeft  *metricResourceUri*.

Een klassieke Opslagaccount Hello omvat automatisch schalen instelling metricTrigger bijvoorbeeld:

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

Voor een opslagaccount met (niet-klassiek) omvat Hallo metricTrigger:

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a>Gangbare metrische gegevens van Service Bus
U kunt schalen door Service Bus-wachtrijlengte, het aantal berichten in de Service Bus-wachtrij Hallo Hallo. Wachtrijlengte van Service Bus is een speciale metriek en Hallo drempelwaarde Hallo aantal berichten per exemplaar is. Bijvoorbeeld, als er twee exemplaren en Hallo drempelwaarde too100 is ingesteld, schalen treedt op wanneer totaal aantal berichten in wachtrij Hallo Hallo 200. Dat kan worden 100 berichten per exemplaar, 120 en 80, of een andere combinatie die too200 of meer opgeteld.

U kunt Hallo-instelling voor automatisch schalen in Hallo Resource Manager-sjabloon toouse bijwerken voor VM-schaalsets *metricName* als *ApproximateMessageCount* en het Hallo-ID van de opslagwachtrij Hallo als doorgeeft  *metricResourceUri*.

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> Hallo resource groep concept bestaat niet voor Service Bus, maar Azure Resource Manager maakt een standaardresourcegroep per regio. Hallo resourcegroep bevindt zich doorgaans in Hallo 'Default - ServiceBus-[regio]'-indeling. Bijvoorbeeld 'Service Bus-standaard-EastUS', 'Service Bus-standaard-WestUS', 'standaard-ServiceBus-AustraliaEast, enzovoort.
>
>
