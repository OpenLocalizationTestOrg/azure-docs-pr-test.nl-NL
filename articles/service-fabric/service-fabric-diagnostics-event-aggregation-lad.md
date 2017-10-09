---
title: Aggregatie van Service Fabric-gebeurtenis met Linux Azure Diagnostics aaaAzure | Microsoft Docs
description: Meer informatie over het aggregeren en het verzamelen van gebeurtenissen met LAD voor controle en diagnostische gegevens van Azure Service Fabric-clusters.
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
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>Gebeurtenis-aggregatie en verzameling op basis van Linux Azure Diagnostics
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Wanneer u een Azure Service Fabric-cluster uitvoert, is het een goed idee toocollect Hallo Logboeken uit alle Hallo knooppunten in een centrale locatie. Hallo-logboeken die in een centrale locatie, helpt u bij het analyseren en oplossen van problemen in het cluster of problemen in Hallo toepassingen en services die worden uitgevoerd in het cluster.

Een manier tooupload en verzamelen van Logboeken is toouse Hallo Linux Azure Diagnostics (LAD) extensie, die u uploadt logboeken tooAzure opslag, en heeft ook Hallo optie toosend logboeken tooAzure Application Insights of Event Hubs. U kunt ook gebruikt een extern proces tooread Hallo gebeurtenissen uit de opslag en plaats deze in een analyse platform-product, zoals [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) of een andere oplossing voor het parseren van het logboek.

## <a name="log-and-event-sources"></a>Logboekbestand en de gebeurtenis

### <a name="service-fabric-platform-events"></a>Gebeurtenissen voor service Fabric-platform
Service Fabric verzendt enkele out-of-the-box-logboeken via [LTTng](http://lttng.org), met inbegrip van operationele gebeurtenissen of runtime-gebeurtenissen. Deze logboeken worden opgeslagen in het Hallo-locatie die Hallo van het cluster Resource Manager-sjabloon worden opgegeven. tooget of Hallo opslag accountdetails instellen, zoeken naar label Hallo **AzureTableWinFabETWQueryable** en zoekt u **StoreConnectionString**.

### <a name="application-events"></a>Toepassingsgebeurtenissen
 Gebeurtenissen van uw toepassingen en services code zoals opgegeven door u worden verzonden wanneer het instrumenteren van de software. U kunt een oplossing voor logboekregistratie die op basis van tekst logboekbestanden--bijvoorbeeld LTTng schrijft. Zie voor meer informatie, Hallo LTTng documentatie op de tracering van de toepassing.

[Controle en diagnose van services in de instellingen voor een lokale computer ontwikkeling](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Hallo-extensie voor diagnostische gegevens implementeren
Hallo eerste stap bij het verzamelen van Logboeken is toodeploy Hallo-extensie voor diagnostische gegevens op elk van de VM Hallo in Hallo Service Fabric-cluster. Hallo-extensie voor diagnostische gegevens verzamelt logboeken op elke virtuele machine en geüpload toohello storage-account die u opgeeft. Hallo stappen variëren, afhankelijk van of u hello Azure-portal of Azure Resource Manager gebruiken.

toodeploy hello Diagnostics extensie toohello virtuele machines in Hallo cluster als onderdeel van het maken van een cluster instellen **Diagnostics** te**op**. Nadat u Hallo-cluster maakt, kunt u deze instelling niet wijzigen met behulp van Hallo-portal.

Vervolgens Linux Azure Diagnostics (LAD) toocollect Hallo bestanden configureren en plaats deze in uw opslagaccount. Dit proces als het scenario 3 ('uploaden en uw eigen logboekbestanden') in Hallo artikel wordt uitgelegd [LAD met behulp van toomonitor en onderzoeken van virtuele Linux-machines](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Na dit proces krijgt u toegang tot toohello wordt getraceerd. U kunt uploaden Hallo traceringen tooa visualizer van uw keuze.

U kunt ook Hallo-extensie voor diagnostische gegevens implementeren met behulp van Azure Resource Manager. Hallo proces is vergelijkbaar voor Windows en Linux, en is vastgelegd voor Windows-clusters in [hoe toocollect registreert met Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md).

U kunt ook Operations Management Suite, zoals beschreven in [Operations Management Suite-logboekanalyse met Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Nadat u deze configuratie, Hallo Hallo LAD agent monitors opgegeven logboekbestanden. Wanneer een nieuwe regel toegevoegde toohello bestand is, maakt deze een syslog-item dat is verzonden toohello opslag die u hebt opgegeven.

## <a name="next-steps"></a>Volgende stappen

toounderstand in meer detail welke gebeurtenissen u moet controleren terwijl het oplossen van problemen, Zie [LTTng documentatie](http://lttng.org/docs) en [LAD met behulp van](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
