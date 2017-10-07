---
title: aaaIntroduction tooAzure netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo netwerk-Watcher-service voor bewaking en visualiseren netwerk verbonden bronnen in Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 14bc2266-99e3-42a2-8d19-bd7257fec35e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 283b3fa6add05d9bad6d5dbdae1524344d1bfc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-monitoring-overview"></a>Bewaking Azure network-overzicht

Een end-to-end-netwerk in Azure opbouwen klanten door te organiseren en samenstellen van verschillende afzonderlijke netwerkbronnen zoals VNet, ExpressRoute, Application Gateway, Load balancers en meer. Bewaking is beschikbaar op elke Hallo netwerkbronnen. We verwijzen toothis bewaakt als resource niveau bewaking.

Hallo-endnetwerk tooend kunt complexe configuraties en interacties tussen resources, het maken van complexe scenario's die bewaking op basis van een scenario via netwerk-Watcher nodig hebben.

In dit artikel bevat informatie over scenario en Broncontrole niveau. Netwerkbewaking in Azure is uitgebreid en bevat informatie over twee hoofdcategorieën:

* [**Netwerk-Watcher** ](#network-watcher) -bewaking op basis van een Scenario bij Hallo-functies in netwerk-Watcher wordt geleverd. Deze service omvat pakketopname, volgende hop, IP-stroom controleren, groep beveiligingsweergave, NSG stroom Logboeken. Scenario niveau bewaking biedt een end-tooend-weergave van netwerkbronnen in contrast tooindividual resource netwerkbewaking.
* [**Broncontrole** ](#network-resource-level-monitoring) -niveau Broncontrole bestaat uit vier onderdelen, diagnostische logboeken, metrische gegevens, het oplossen van problemen en resourcestatus. Al deze functies zijn gebouwd op niveau van de bron van de Hallo.

## <a name="network-watcher"></a>Network Watcher

Netwerk-Watcher is een regionale service waarmee u toomonitor en onderzoeken van voorwaarden op een netwerk scenario niveau in, en naar Azure. Netwerkcontrole en visualisatie hulpprogramma's beschikbaar met de netwerk-Watcher kunnen u begrijpen, diagnoses stellen en krijgen insights tooyour netwerk in Azure.

Netwerk-Watcher heeft momenteel Hallo volgende mogelijkheden:

* **[Topologie](network-watcher-topology-overview.md)**  -voorziet in een netwerk niveau weergave tonen Hallo verschillende verbindingskabels en koppelingen tussen netwerkbronnen in een resourcegroep.
* **[Variabele pakketopname](network-watcher-packet-capture-overview.md)**  -pakketgegevens naar en vanuit een virtuele machine worden vastgelegd. Geavanceerde opties en verfijnd besturingselementen zoals kunnen tooset tijd wordt voor het filteren en beperkingen van de bestandsgrootte veelzijdigheid bieden. Hallo pakketgegevens kunnen worden opgeslagen in een blob-opslag of op Hallo lokale schijf in de CAP-indeling.
* **[IP-stroom controleren](network-watcher-ip-flow-verify-overview.md)**  -controleert of een pakket wordt toegestaan of geweigerd op basis van stroom informatie 5-tuple pakket parameters (doel-IP, bron-IP, doelpoort, bronpoort en Protocol). Als hello-pakket is geweigerd door een beveiligingsgroep, wordt hello regel en -groep die geweigerd hello-pakket geretourneerd.
* **[Volgende hop](network-watcher-next-hop-overview.md)**  -Hallo volgende hop voor pakketten worden gerouteerd in hello Azure Network-Fabric, zodat u toodiagnose een verkeerd geconfigureerde gebruiker gedefinieerde routes bepaalt.
* **[Groep beveiligingsweergave](network-watcher-security-group-view-overview.md)**  -Hallo effectieve en toegepaste beveiligingsregels voor verbindingen die worden toegepast op een virtuele machine opgehaald.
* **[Logboekregistratie NSG Flow](network-watcher-nsg-flow-logging-overview.md)**  -logboeken van de stroom voor Netwerkbeveiligingsgroepen kunt u toocapture gerelateerde tootraffic logboeken die worden toegestaan of geweigerd door Hallo beveiligingsregels voor verbindingen in groep Hallo. Hallo-stroom wordt gedefinieerd door de gegevens van een 5-tuple: bron-IP, doel-IP, bronpoort, doelpoort en -Protocol.
* **[Virtuele netwerkgateway en verbinding probleemoplossing](network-watcher-troubleshoot-manage-rest.md)**  -Hallo mogelijkheid tootroubleshoot biedt virtuele netwerkgateways en verbindingen.
* **[Netwerk-abonnementen](#network-subscription-limits)**  -kunt u gebruik van netwerkbronnen tooview tegen limieten.
* **[Configureren van diagnostische gegevens logboek](#diagnostic-logs)**  : biedt een enkel deelvenster tooenable of diagnostische logboeken voor netwerkbronnen in een resourcegroep uitschakelen.
* **[Connectiviteit (Preview)](network-watcher-connectivity-overview.md)**  -controleert of Hallo mogelijkheid tot stand brengen van een directe TCP-verbinding van een virtuele machine tooa opgegeven eindpunt.

### <a name="role-based-access-control-rbac-in-network-watcher"></a>Op rollen gebaseerde toegangsbeheer (RBAC) in de netwerk-Watcher

Hallo maakt gebruik van netwerk-watcher [gebaseerd toegangsbeheer (RBAC) model](../active-directory/role-based-access-control-what-is.md). Hallo netwerk-Watcher zijn Hallo volgende machtigingen vereist. Het is belangrijk toomake ervoor dat die rol Hallo is gebruikt voor het initiëren van netwerk-Watcher-API's of het gebruik van netwerk-Watcher vanuit de portal Hallo Hallo vereist toegang heeft.

|Resource| Machtiging|
|---|---| 
|Microsoft.Storage/ |Lezen|
|Microsoft.Authorization/| Lezen| 
|Microsoft.Resources/subscriptions/resourceGroups/| Lezen|
|Microsoft.Storage/storageAccounts/listServiceSas/ | Actie|
|Microsoft.Storage/storageAccounts/listAccountSas/ |Actie|
|Microsoft.Storage/storageAccounts/listKeys/ | Actie|
|Microsoft.Compute/virtualMachines/ |Lezen|
|Microsoft.Compute/virtualMachines/ |Schrijven|
|Microsoft.Compute/virtualMachineScaleSets/ |Lezen|
|Microsoft.Compute/virtualMachineScaleSets/ |Schrijven|
|Microsoft.Network/networkWatchers/packetCaptures/ |Lezen|
|Microsoft.Network/networkWatchers/packetCaptures/| Schrijven|
|Microsoft.Network/networkWatchers/packetCaptures/| Verwijderen|
|Microsoft.Network/networkWatchers/ |Schrijven |
|Microsoft.Network/networkWatchers/| Lezen |
|Microsoft.Insights/alertRules/ |*|
|Microsoft.Support/ | *|

### <a name="network-subscription-limits"></a>Netwerk-abonnementen

Netwerk-abonnementen bieden u details van Hallo informatie over het gebruik van elk van de netwerkbron Hallo in een abonnement in een regio tegen Hallo kunt u het maximum aantal bronnen die beschikbaar zijn.

![limiet van het abonnement][nsl]

## <a name="network-resource-level-monitoring"></a>Resource niveau netwerkbewaking

Hallo volgende functies zijn beschikbaar voor het niveau Broncontrole:

### <a name="audit-log"></a>Controlelogboek

Bewerkingen die worden uitgevoerd als onderdeel van de configuratie van netwerken Hallo worden geregistreerd. Deze logboeken kunnen worden weergegeven in hello Azure-portal of opgehaald met behulp van Microsoft-hulpprogramma's zoals Power BI of hulpprogramma's van derden. Controlelogboeken zijn beschikbaar via het Hallo-portal, PowerShell, CLI en Rest-API. Zie voor meer informatie over controlelogboeken [bewerkingen met Resource Manager controleren](../resource-group-audit.md)

Controlelogboeken zijn beschikbaar voor bewerkingen die op alle netwerkbronnen.

### <a name="metrics"></a>Metrische gegevens

Metrische gegevens zijn metingen van de prestaties en prestatiemeteritems die gedurende een periode worden verzameld. Metrische gegevens zijn momenteel beschikbaar voor de toepassingsgateway. Metrische gegevens kunnen worden gebruikt tootrigger waarschuwingen op basis van de drempelwaarde. Zie [Application Gateway Diagnostics](../application-gateway/application-gateway-diagnostics.md) tooview hoe metrische gegevens gebruikte toocreate waarschuwingen kunnen worden.

![metrische gegevens weergeven][metrics]

### <a name="diagnostic-logs"></a>Diagnostische logboeken

Periodieke en eigen initiatief gebeurtenissen zijn gemaakt door netwerkbronnen en vastgelegd in de storage-accounts, tooan Event Hub of Log Analytics verzonden. Deze logboeken bieden inzicht in het Hallo-status van een resource. Deze logboeken kunnen worden weergegeven in de hulpprogramma's, zoals Power BI en Log Analytics. hoe diagnostische logboeken tooview, gaat u naar toolearn [logboekanalyse](../log-analytics/log-analytics-azure-networking-analytics.md).

Diagnostische logboeken beschikbaar zijn voor [Load Balancer](../load-balancer/load-balancer-monitor-log.md), [Netwerkbeveiligingsgroepen](../virtual-network/virtual-network-nsg-manage-log.md), Routes, en [Application Gateway](../application-gateway/application-gateway-diagnostics.md).

Netwerk-Watcher biedt dat een diagnostische logboeken weergeven. Deze weergave bevat alle netwerkresources die ondersteuning bieden voor diagnostische gegevens vastleggen. U kunt in deze weergave inschakelen en uitschakelen van netwerkresources snel en gemakkelijk.

![logboeken][logs]

### <a name="troubleshooting"></a>Problemen oplossen

Hallo-blade een ervaring in Hallo portal probleemoplossing is beschikbaar op netwerkbronnen vandaag toodiagnose veelvoorkomende problemen die zijn gekoppeld aan een afzonderlijke resource. Deze ervaring is beschikbaar voor Hallo netwerkbronnen - ExpressRoute, VPN-Gateway, Application Gateway, netwerk-beveiligingslogboeken, Routes, DNS, Load Balancer en Traffic Manager te volgen. toolearn meer informatie over resource niveau problemen wilt oplossen, gaat u naar [diagnosticeren en oplossen van problemen bij het oplossen van Azure](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)

![informatie over probleemoplossing][TS]

### <a name="resource-health"></a>Status van resources

Hallo-status van een netwerkbron wordt periodiek verstrekt. Deze bronnen omvatten VPN-Gateway en VPN-tunnel. De resourcestatus is toegankelijk op Hallo Azure-portal. toolearn meer informatie over de resourcestatus, gaat u naar [bron Health-overzicht](../resource-health/resource-health-overview.md)

## <a name="next-steps"></a>Volgende stappen

Na het leren over de netwerk-Watcher leert u:

Voer een pakketopname op de virtuele machine in via [variabele pakketopname in hello Azure-portal](network-watcher-packet-capture-manage-portal.md)

Proactieve controle en diagnostische gegevens met behulp van [waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md).

Beveiligingsproblemen met detecteren [pakketopname met Wireshark analyseren](network-watcher-deep-packet-inspection.md), met open-source hulpprogramma's.

Meer informatie over een aantal Hallo andere sleutel [netwerkmogelijkheden](../networking/networking-overview.md) van Azure.

<!--Image references-->
[TS]: ./media/network-watcher-monitoring-overview/troubleshooting.png
[logs]: ./media/network-watcher-monitoring-overview/logs.png
[metrics]: ./media/network-watcher-monitoring-overview/metrics.png
[nsl]: ./media/network-watcher-monitoring-overview/nsl.png











