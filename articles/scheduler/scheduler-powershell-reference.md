---
title: aaaScheduler referentiemateriaal voor PowerShell-Cmdlets
description: Scheduler-referentiemateriaal voor PowerShell-Cmdlets
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 9a26c457-d7a1-4e4a-bc79-f26592155218
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: a2b23bcd3e4493ffba1dbf21fbb87818be7c01e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-powershell-cmdlets-reference"></a>Scheduler-referentiemateriaal voor PowerShell-Cmdlets
Hallo volgende tabel worden beschreven en koppelingen toohello-verwijzingspagina van elk van de belangrijkste Hallo-cmdlets in Azure Scheduler.

tooinstall Azure PowerShell en deze koppelen aan uw Azure-abonnement, Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). 

Voor meer informatie over [Azure Resource Manager-cmdlets](/powershell/azure/overview), Zie [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md).

| Cmdlet | Beschrijving van de cmdlet |
| --- | --- |
| [Schakel AzureRmSchedulerJobCollection](/powershell/module/azurerm.scheduler/disable-azurermschedulerjobcollection) |Hiermee schakelt u een taakverzameling bevat. |
| [Schakel AzureRmSchedulerJobCollection](/powershell/module/azurerm.scheduler/enable-azurermschedulerjobcollection) |Een jobverzameling kunt. |
| [Get-AzureRmSchedulerJob](/powershell/module/azurerm.scheduler/get-azurermschedulerjob) |Scheduler-taken opgehaald. |
| [Get-AzureRmSchedulerJobCollection](/powershell/module/azurerm.scheduler/get-azurermschedulerjobcollection) |Taakverzamelingen opgehaald. |
| [Get-AzureRmSchedulerJobHistory](/powershell/module/azurerm.scheduler/get-azurermschedulerjobhistory) |Taakgeschiedenis opgehaald. |
| [Nieuwe AzureRmSchedulerHttpJob](/powershell/module/azurerm.scheduler/new-azurermschedulerhttpjob) |Maakt een HTTP-taak. |
| [Nieuwe AzureRmSchedulerJobCollection](/powershell/module/azurerm.scheduler/new-azurermschedulerjobcollection) |Een jobverzameling maakt. |
| [Nieuwe AzureRmSchedulerServiceBusQueueJob](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebusqueuejob) |Een service bus-wachtrijtaak maakt. |
| [Nieuwe AzureRmSchedulerServiceBusTopicJob](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebustopicjob) |Maakt een taak van service bus-onderwerp. |
| [Nieuwe AzureRmSchedulerStorageQueueJob](/powershell/module/azurerm.scheduler/new-azurermschedulerstoragequeuejob) |Maakt een taak van de wachtrij opslag. |
| [Verwijder AzureRmSchedulerJob](/powershell/module/azurerm.scheduler/remove-azurermschedulerjob) |Hiermee verwijdert u een geplande taak. |
| [Verwijder AzureRmSchedulerJobCollection](/powershell/module/azurerm.scheduler/remove-azurermschedulerjobcollection) |Hiermee verwijdert u een taakverzameling bevat. |
| [Set-AzureRmSchedulerHttpJob](/powershell/module/azurerm.scheduler/set-azurermschedulerhttpjob) |Hiermee wijzigt u een HTTP-Scheduler-taak. |
| [Set-AzureRmSchedulerJobCollection](/powershell/module/azurerm.scheduler/set-azurermschedulerjobcollection) |Een jobverzameling wijzigt. |
| [Set-AzureRmSchedulerServiceBusQueueJob](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebusqueuejob) |Hiermee wijzigt u een service bus-wachtrijtaak. |
| [Set-AzureRmSchedulerServiceBusTopicJob](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebustopicjob) |Hiermee wijzigt u een service bus-onderwerp taak. |
| [Set-AzureRmSchedulerStorageQueueJob](/powershell/module/azurerm.scheduler/set-azurermschedulerstoragequeuejob) |Hiermee wijzigt u een taak van de wachtrij opslag. |

Voor meer gedetailleerde informatie kunt u een van de volgende cmdlets Hallo uitvoeren: 

```
Get-Help <cmdlet name> -Detailed
```
```
Get-Help <cmdlet name> -Examples
```
```
Get-Help <cmdlet name> -Full
```

## <a name="see-also"></a>Zie ook
 [Wat is Scheduler?](scheduler-intro.md)

 [Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie](scheduler-concepts-terms.md)

 [Aan de slag met behulp van Scheduler in hello Azure-portal](scheduler-get-started-portal.md)

 [Plannen en facturering in Azure Scheduler](scheduler-plans-billing.md)

 [Naslaginformatie over REST API van Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler](scheduler-high-availability-reliability.md)

 [Azure Scheduler-limieten, standaardwaarden en foutcodes](scheduler-limits-defaults-errors.md)

 [Azure Scheduler uitgaande verificatie](scheduler-outbound-authentication.md)

