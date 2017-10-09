---
title: Service Fabric operationele kanaal aaaAzure | Microsoft Docs
description: Uitgebreide lijst met Logboeken die worden gegenereerd in Hallo operationele kanaal van Azure Service Fabric-clusters.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: 358782420ed62b202d6a89fe0f200b5ef0384c9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="operational-channel"></a>Operationele kanaal 

Hallo operationele kanaal bestaat uit de logboeken van hoog niveau acties die door Service Fabric wordt uitgevoerd op de knooppunten als uw cluster. Wanneer ' diagnostische gegevens ' is ingeschakeld voor een cluster hello Azure Diagnostics-agent op het cluster is geïmplementeerd en is standaard geconfigureerd voor tooread logboeken van het operationele kanaal Hallo. Meer informatie over het configureren van Hallo [Azure Diagnostics agent](service-fabric-diagnostics-event-aggregation-wad.md) toomodify Hallo diagnostische configuratie van uw cluster toopick meer logboeken of prestatiemeteritems. 

## <a name="operational-channel-logs"></a>Operationele kanaal Logboeken 

Hier volgt een uitgebreide lijst met Logboeken die worden geleverd door de Service Fabric in Hallo operationele kanaal. 

| Gebeurtenis-id | Naam | Bron (taak) | Niveau |
| --- | --- | --- | --- |
| 25620 | NodeOpening | FabricNode | Informatief |
| 25621 | NodeOpenedSuccess | FabricNode | Informatief |
| 25622 | NodeOpenedFailed | FabricNode | Informatief |
| 25623 | NodeClosing | FabricNode | Informatief |
| 25624 | NodeClosed | FabricNode | Informatief |
| 25625 | NodeAborting | FabricNode | Informatief |
| 25626 | NodeAborted | FabricNode | Informatief |
| 29627 | ClusterUpgradeStart | CM | Informatief |
| 29628 | ClusterUpgradeComplete | CM | Informatief |
| 29629 | ClusterUpgradeRollback | CM | Informatief |
| 29630 | ClusterUpgradeRollbackComplete | CM | Informatief |
| 29631 | ClusterUpgradeDomainComplete | CM | Informatief |
| 23074 | ContainerActivated | Die als host fungeert | Informatief |
| 23075 | ContainerDeactivated | Die als host fungeert | Informatief |
| 29620 | ApplicationCreated | CM | Informatief |
| 29621 | ApplicationUpgradeStart | CM | Informatief |
| 29622 | ApplicationUpgradeComplete | CM | Informatief |
| 29623 | ApplicationUpgradeRollback | CM | Informatief |
| 29624 | ApplicationUpgradeRollbackComplete | CM | Informatief |
| 29625 | ApplicationDeleted | CM | Informatief |
| 29626 | ApplicationUpgradeDomainComplete | CM | Informatief |
| 18566 | ServiceCreated | FM | Informatief |
| 18567 | ServiceDeleted | FM | Informatief |

## <a name="next-steps"></a>Volgende stappen

* Meer informatie over algemene [genereren van gebeurtenissen op Hallo platform niveau](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric
* Wijzigen van uw [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) configuratie toocollect meer logboeken
* [Instellen van Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) toosee het operationele kanaal Logboeken
