---
title: Logboeken verzamelen met behulp van Linux Azure Diagnostics | Microsoft Docs
description: Dit artikel wordt beschreven hoe u Azure Diagnostics instelt voor het verzamelen van Logboeken van een Service Fabric Linux-cluster in Azure wordt uitgevoerd.
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
ms.openlocfilehash: 3e41caaeb38c55d1c6c3bfdce2f81c86b4aff4d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Logboeken verzamelen met Azure Diagnostics
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Wanneer u een Azure Service Fabric-cluster uitvoert, is het een goed idee de logboeken verzamelen van alle knooppunten in een centrale locatie. De logboeken op een centrale locatie die gemakkelijk te analyseren en oplossen van problemen, ongeacht of deze in uw services, uw toepassing of het cluster zelf. Een manier om te uploaden en verzamelen van Logboeken is het gebruik van de extensie Azure Diagnostics, die logboeken naar Azure Storage, Azure Application Insights of Azure Event Hubs uploadt. U kunt ook de gebeurtenissen van opslag- of Event Hubs gelezen en plaats deze in een product zoals [logboekanalyse](../log-analytics/log-analytics-service-fabric.md) of een andere oplossing voor het parseren van het logboek. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) wordt geleverd met een uitgebreide zoeken en analytics logboekservice ingebouwde.

## <a name="log-sources-that-you-might-want-to-collect"></a>Logboek bronnen die u wilt verzamelen
* **Service Fabric-logboeken**: verzonden van het platform via [LTTng](http://lttng.org) en geüpload naar uw storage-account. Logboeken kunnen worden operationele gebeurtenissen of runtime-gebeurtenissen die het platform verzendt. Deze logboeken worden opgeslagen in de locatie die het clustermanifest aangeeft. (Als u de accountdetails van de opslag, zoekt u de tag **AzureTableWinFabETWQueryable** en zoekt u **StoreConnectionString**.)
* **Toepassingsgebeurtenissen**: verzonden vanuit de code van uw service. U kunt een oplossing voor logboekregistratie die op basis van tekst logboekbestanden--bijvoorbeeld LTTng schrijft. Zie voor meer informatie de documentatie van LTTng op de tracering van de toepassing.  

## <a name="deploy-the-diagnostics-extension"></a>De extensie voor diagnostische gegevens implementeren
De eerste stap bij het verzamelen van Logboeken is voor het implementeren van de extensie voor diagnostische gegevens over elk van de virtuele machines in het Service Fabric-cluster. De extensie voor diagnostische gegevens verzamelt logboeken op elke virtuele machine en geüpload naar het opslagaccount dat u opgeeft. De stappen variëren, afhankelijk van of u de Azure portal of Azure Resource Manager gebruiken.

Instellen voor het implementeren van de extensie voor diagnostische gegevens naar de virtuele machines in het cluster als onderdeel van het maken van het cluster, **Diagnostics** naar **op**. Nadat u het cluster hebt gemaakt, kunt u deze instelling niet wijzigen met behulp van de portal.

Configureer vervolgens Linux Azure Diagnostics (LAD) om te verzamelen van de bestanden en plaats deze in uw opslagaccount. Dit proces als het scenario 3 ('uploaden en uw eigen logboekbestanden') in het artikel wordt uitgelegd [LAD bewaken en onderzoeken van virtuele Linux-machines met behulp van](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Deze bewerking, krijgt u toegang tot de traceringen. U kunt de traceringen uploaden naar een visualizer van uw keuze.

U kunt ook de extensie voor diagnostische gegevens implementeren met behulp van Azure Resource Manager. Het proces is vergelijkbaar voor Windows en Linux- en wordt beschreven voor Windows-clusters in [het verzamelen van logboeken met diagnostische gegevens van Azure](service-fabric-diagnostics-how-to-setup-wad.md).

U kunt ook Operations Management Suite, zoals beschreven in [Operations Management Suite-logboekanalyse met Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Nadat u deze configuratie, bewaakt de agent LAD de logboekbestanden van de opgegeven. Wanneer een nieuwe regel wordt toegevoegd aan het bestand, maakt deze een syslog-vermelding die wordt verzonden naar de opslag die u hebt opgegeven.

## <a name="next-steps"></a>Volgende stappen
Zie inzicht in meer detail welke gebeurtenissen u bij het oplossen van problemen te onderzoeken [LTTng documentatie](http://lttng.org/docs) en [LAD met behulp van](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

