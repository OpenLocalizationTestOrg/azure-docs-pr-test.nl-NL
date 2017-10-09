---
title: logboeken met behulp van Linux Azure Diagnostics aaaCollect | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset van Azure Diagnostics toocollect registreert van een Service Fabric Linux-cluster in Azure wordt uitgevoerd.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a160d469-8b7d-4560-82dd-8500db34a44a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/28/2017
ms.author: subramar
ms.openlocfilehash: f61172876e744ea3e361f9ae513254239d6ba27f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Logboeken verzamelen met Azure Diagnostics
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Wanneer u een Azure Service Fabric-cluster uitvoert, is het een goed idee toocollect Hallo Logboeken uit alle Hallo knooppunten in een centrale locatie. Hallo-logboeken die in een centrale locatie, maakt het eenvoudig tooanalyze en oplossen van problemen, ongeacht of deze in uw services, uw toepassing of Hallo cluster zelf. Een manier tooupload en verzamelen van Logboeken is toouse hello Azure extensie voor diagnostische gegevens, welke uploads logboeken tooAzure opslag, Azure Application Insights of Azure Event Hubs. U kunt ook Hallo gebeurtenissen lezen uit de opslag- of Event Hubs en plaats deze in een product zoals [logboekanalyse](../log-analytics/log-analytics-service-fabric.md) of een andere oplossing voor het parseren van het logboek. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) wordt geleverd met een uitgebreide zoeken en analytics logboekservice ingebouwde.

## <a name="log-sources-that-you-might-want-toocollect"></a>Meld u bronnen die u wilt misschien toocollect
* **Service Fabric-logboeken**: verzonden van Hallo platform via [LTTng](http://lttng.org) en tooyour opslagaccount geüpload. Logboeken kunnen operationele gebeurtenissen of runtime-gebeurtenissen die Hallo platform verzendt. Deze logboeken worden opgeslagen op Hallo locatie die clustermanifest Hallo bevat. (tooget Hallo opslag accountdetails zoeken naar label Hallo **AzureTableWinFabETWQueryable** en zoekt u **StoreConnectionString**.)
* **Toepassingsgebeurtenissen**: verzonden vanuit de code van uw service. U kunt een oplossing voor logboekregistratie die op basis van tekst logboekbestanden--bijvoorbeeld LTTng schrijft. Zie voor meer informatie, Hallo LTTng documentatie op de tracering van de toepassing.  

## <a name="deploy-hello-diagnostics-extension"></a>Hallo-extensie voor diagnostische gegevens implementeren
Hallo eerste stap bij het verzamelen van Logboeken is toodeploy Hallo-extensie voor diagnostische gegevens op elk van de VM Hallo in Hallo Service Fabric-cluster. Hallo-extensie voor diagnostische gegevens verzamelt logboeken op elke virtuele machine en geüpload toohello storage-account die u opgeeft. Hallo stappen variëren, afhankelijk van of u hello Azure-portal of Azure Resource Manager gebruiken.

toodeploy hello Diagnostics extensie toohello virtuele machines in Hallo cluster als onderdeel van het maken van een cluster instellen **Diagnostics** te**op**. Nadat u Hallo-cluster maakt, kunt u deze instelling niet wijzigen met behulp van Hallo-portal.

Vervolgens Linux Azure Diagnostics (LAD) toocollect Hallo bestanden configureren en plaats deze in uw opslagaccount. Dit proces als het scenario 3 ('uploaden en uw eigen logboekbestanden') in Hallo artikel wordt uitgelegd [LAD met behulp van toomonitor en onderzoeken van virtuele Linux-machines](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Na dit proces krijgt u toegang tot toohello wordt getraceerd. U kunt uploaden Hallo traceringen tooa visualizer van uw keuze.

U kunt ook Hallo-extensie voor diagnostische gegevens implementeren met behulp van Azure Resource Manager. Hallo proces is vergelijkbaar voor Windows en Linux, en is vastgelegd voor Windows-clusters in [hoe toocollect registreert met Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md).

U kunt ook Operations Management Suite, zoals beschreven in [Operations Management Suite-logboekanalyse met Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Nadat u deze configuratie, Hallo Hallo LAD agent monitors opgegeven logboekbestanden. Wanneer een nieuwe regel toegevoegde toohello bestand is, maakt deze een syslog-item dat is verzonden toohello opslag die u hebt opgegeven.

## <a name="next-steps"></a>Volgende stappen
toounderstand in meer detail welke gebeurtenissen u moet controleren terwijl het oplossen van problemen, Zie [LTTng documentatie](http://lttng.org/docs) en [LAD met behulp van](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

