---
title: aaaAzure Systeemmonitor-overzicht | Microsoft Docs
description: Monitor voor Azure verzamelt statistieken voor gebruik in waarschuwingen, webhooks, automatisch schalen en automatisering. Artikel ook de naam van andere Microsoft-controle-opties.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a>Overzicht van Azure Monitor
Dit artikel bevat een overzicht van hello Azure Monitor-service in Microsoft Azure. Wordt besproken wat Azure Monitor biedt en aanwijzers tooadditional informatie bevat over het toouse Azure bewaken.  Als u liever een video-inleiding, Zie de volgende stappen koppelingen op Hallo onder aan dit artikel. 

## <a name="why-monitor-your-application-or-system"></a>Uw toepassing of het systeem waarom te bewaken
Cloud-toepassingen zijn complexe met veel bewegende onderdelen. Monitoring biedt gegevens tooensure die uw toepassing up blijft en wordt uitgevoerd in een foutloze toestand bevindt. Ook kunt u toostave potentiële problemen uitgeschakeld of het oplossen van het verleden zijn. Bovendien kunt u bewaking gegevens toogain uitgebreide statistieken over uw toepassing. Deze kennis kan u helpen de prestaties van toepassingen tooimprove of onderhoud of acties die anders worden handmatige interventie moeten automatiseren.


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a>Monitor voor Azure en Microsoft's andere bewaking producten
Azure biedt een basisniveau infrastructuur metrische gegevens en logboeken voor de meeste services in Microsoft Azure. Azure-services die nog plaats niet hun gegevens naar Azure-Monitor wordt deze geplaatst er in Hallo toekomstige.

Microsoft geleverd aanvullende producten en services die extra bewakingsmogelijkheden bieden voor ontwikkelaars, DevOps of IT-Ops waarvoor ook on-premises installaties. Zie voor een overzicht van en kennis van hoe deze verschillende producten en services samenwerken [bewaken in Microsoft Azure](monitoring-overview.md).

## <a name="monitoring-sources---compute"></a>Bronnen - Compute bewaking

![Model voor controle en diagnostische gegevens voor niet-rekenresources](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

Hallo Compute services bevatten 
- Cloudservices 
- Virtuele machines 
- Virtuele-machineschaalsets 
- Service Fabric

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a>Toepassing - Logboeken met diagnostische gegevens, logboeken en metrische gegevens
Toepassingen kunnen worden uitgevoerd in Hallo Gastbesturingssysteem in Hallo compute-model. Ze verzenden hun eigen set logboeken en metrische gegevens. Monitor voor Azure is afhankelijk van hello Azure diagnostics-extensie (Windows of Linux) toocollect meeste logboeken en niveau metrische gegevens voor een toepassing. Hallo-typen zijn

* Prestatiemeteritems
* Toepassingslogboeken
* Windows-gebeurtenislogboeken
* De gebeurtenisbron .NET
* IIS-logboeken
* ETW op basis van het manifest
* Crashdumps
* Klant-foutenlogboeken

Zonder Hallo-extensie voor diagnostische gegevens zijn slechts enkele metrische gegevens zoals CPU-gebruik beschikbaar. 

### <a name="host-and-guest-vm-metrics"></a>Host en de Gast-VM metrische gegevens
Hallo hebben eerder vermelde rekenresources en een toegewezen host VM gastbesturingssysteem ze met communiceren. Hallo host, VM en gastbesturingssysteem zijn Hallo equivalent van basis-VM en Gast-VM in Hallo Hyper-V-hypervisor model. U kunt metrische gegevens verzamelen op beide. U kunt ook diagnostische logboeken verzamelen op Hallo gastbesturingssysteem.   

### <a name="activity-log"></a>Activiteitenlogboek
U kunt Hallo activiteitenlogboek (eerder operationele of controlelogboeken genoemd) voor meer informatie zoeken over uw resource volgens hello Azure-infrastructuur. Hallo-logboek bevat informatie zoals de tijden waarop resources worden gemaakt of vernietigd.  Zie voor meer informatie [overzicht activiteitenlogboek](monitoring-overview-activity-logs.md). 

## <a name="monitoring-sources---everything-else"></a>Bronnen - alle andere bewaking

![Model voor controle en diagnostische gegevens voor de compute-bronnen](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a>Resource - diagnostische logboeken en metrische gegevens
Verzamelbaar metrische gegevens en diagnostische logboeken variëren, afhankelijk van het brontype Hallo. Web-Apps biedt bijvoorbeeld statistieken op Hallo schijf-i/o en CPU procent. Deze metrische gegevens bestaan voor een Service Bus-wachtrij die in plaats daarvan metrische gegevens zoals de grootte en het bericht doorvoer wachtrij biedt niet. Een lijst met verzamelbaar metrische gegevens voor elke resource is beschikbaar op [ondersteund metrische gegevens](monitoring-supported-metrics.md). 

### <a name="host-and-guest-vm-metrics"></a>Host en de Gast-VM metrische gegevens
Er is niet noodzakelijkerwijs een 1:1-toewijzing tussen de bron en een bepaalde Host of Gast-VM zodat metrische gegevens niet beschikbaar zijn.

### <a name="activity-log"></a>Activiteitenlogboek
Hallo activiteitenlogboek is hetzelfde als voor de rekenresources Hallo.  

## <a name="uses-for-monitoring-data"></a>Gebruikt voor het bewaken van gegevens
Nadat u uw gegevens verzamelt, kunt u doen met het volgende in de Azure-Monitor Hallo

### <a name="route"></a>Route
U kunt bewaking gegevens tooother locaties in realtime streamen.

Voorbeelden zijn:

- TooApplication Insights verzenden zodat u de bijbehorende uitgebreidere visualisatie en analyse hulpprogramma's kunt gebruiken.
- Stuur tooEvent Hubs zodat u hulpprogramma's toothird derden kunt versturen. 

### <a name="store-and-archive"></a>Store en archiveren
Sommige bewakingsgegevens is al opgeslagen en beschikbaar zijn in de Azure-Monitor voor een bepaalde tijdsduur. 
- Metrische gegevens worden opgeslagen voor 30 dagen. 
- Logboekvermeldingen activiteit worden gedurende 90 dagen opgeslagen. 
- Diagnostische logboeken worden niet op alle opgeslagen. 

Als u toostore gegevens langer dan Hallo perioden die wilt hierboven worden genoemd, kunt u een Azure-opslag. Het bewaken van gegevens wordt opgeslagen in uw storage-account op basis van een bewaarbeleid instellen. U hebt toopay voor Hallo ruimte Hallo gegevens in Azure-opslag in beslag. 

Enkele manieren toouse deze gegevens:

- U kunt andere hulpprogramma's binnen of buiten Azure worden gelezen en verwerkt hebben eenmaal geschreven.
- U downloadt Hallo-gegevens voor een lokale archief lokaal of uw bewaarbeleid in Hallo tookeep cloudgegevens voor langere tijd wijzigen.  
- U laten Hallo gegevens in Azure-opslag voor onbepaalde tijd voor archief doeleinden. 

### <a name="query"></a>Query’s uitvoeren
U kunt hello Azure Monitor REST API, platformoverschrijdende opdrachtregelinterface (CLI)-opdrachten, PowerShell-cmdlets gebruiken of Hallo .NET SDK tooaccess Hallo gegevens in Hallo systeem- of Azure-opslag

Voorbeelden zijn:

* Ophalen van gegevens voor een aangepaste bewaking toepassing die u hebt geschreven
* Aangepaste query's maken en verzenden van die toepassing gegevens tooa van derden.

### <a name="visualize"></a>Visualiseren
De controlegegevens in de afbeeldingen en grafieken visualiseren, kunt u trends sneller dan het opzoeken via Hallo gegevens zelf te vinden.  

Een aantal visualisatie methoden zijn:

* Gebruik hello Azure-portal
* Route gegevens tooAzure Application Insights
* Route gegevens tooMicrosoft Power BI
* Route Hallo gegevens tooa van derden visualisatie hulpprogramma met ofwel live te streamen of doordat de Hallo hulpprogramma lezen vanuit een archief in Azure-opslag


### <a name="automate"></a>Automatiseren
U kunt gegevens tootrigger bewakingswaarschuwingen gebruiken of zelfs hele processen. Voorbeelden zijn:

* Gebruik gegevens tooautoscale compute-exemplaren omhoog of omlaag op basis van het laden van toepassingen.
* Verzend een e-mailberichten wanneer een metriek een vooraf ingestelde drempelwaarde overschrijdt.
* Een actie van een web-URL (webhook) tooexecute aanroepen in een systeem buiten Azure
* Een runbook in Azure automation tooperform een verscheidenheid aan taken starten

## <a name="methods-of-accessing-azure-monitor"></a>Methoden van de toegang tot Azure-Monitor
In het algemeen kunt u gegevens bijhouden, Routering en ophalen via een van de volgende methoden Hallo bewerken. Niet alle methoden zijn beschikbaar voor alle acties of gegevenstypen.

* [Azure Portal](https://portal.azure.com)
* [PowerShell](insights-powershell-samples.md)  
* [Platformoverschrijdende opdrachtregelinterface (CLI)](insights-cli-samples.md)
* [REST API](https://docs.microsoft.com/rest/api/monitor/)
* [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a>Volgende stappen
Meer informatie over
- Een video-overzicht van alleen Azure-Monitor is beschikbaar op  
[Aan de slag met Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor). Een extra video uitleg over een scenario waarin u Azure-Monitor kunt is beschikbaar op [verkennen Microsoft Azure-bewaking en diagnostische gegevens](https://channel9.msdn.com/events/Ignite/2016/BRK2234) en [Azure Monitor in een video Ignite 2016](https://myignite.microsoft.com/videos/4977)
- Uitvoeren via hello Azure Monitor interface in [aan de slag met Azure-Monitor](monitoring-get-started.md)
- Hallo instellen [Azure Diagnostics Extensions](../azure-diagnostics.md) als u toodiagnose problemen in uw Cloud-Service, de virtuele Machine probeert virtuele machine instellen of Service Fabric-toepassing schalen.
- [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) als u toodiagnostic problemen in uw App Service-Web-app probeert.
- [Het oplossen van Azure Storage](../storage/common/storage-e2e-troubleshooting.md) bij gebruik van Storage-Blobs, tabellen of wachtrijen
- [Meld u Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) en Hallo [Operations Management Suite](https://www.microsoft.com/oms/)
