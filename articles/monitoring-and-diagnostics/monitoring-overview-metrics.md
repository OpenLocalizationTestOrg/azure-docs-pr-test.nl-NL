---
title: aaaOverview van metrische gegevens in Microsoft Azure | Microsoft Docs
description: Overzicht van metrische gegevens en het gebruik ervan in Microsoft Azure
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 2b97f51e0554dae95a929241ae1f0e25e5c215ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Overzicht van metrische gegevens in Microsoft Azure
Dit artikel wordt beschreven wat metrische gegevens zijn in Microsoft Azure, hun voordelen en hoe ze toostart.  

## <a name="what-are-metrics"></a>Wat zijn de metrische gegevens?
Monitor voor Azure kunt u tooconsume telemetrie toogain inzicht in prestaties Hallo en status van uw workloads in Azure. Hallo belangrijkste type Azure telemetriegegevens is Hallo metrische gegevens (ook wel prestatiemeteritems) die door de meeste Azure-resources. Azure Monitor biedt verschillende manieren tooconfigure en gebruiken van deze metrische gegevens voor bewaking en probleemoplossing.

## <a name="what-can-you-do-with-metrics"></a>Wat kunt u doen met metrische gegevens
Metrische gegevens zijn een waardevolle bron van Telemetrie en kunt u toodo Hallo taken te volgen:

* **Hallo prestaties bijhouden** van de bron (zoals een VM, website of logic app) door de metrische gegevens over een portal grafiek uitzetten en die grafiek tooa dashboard vastmaken.
* **Blijf op de hoogte van een probleem** dat invloed op prestaties van uw resource Hallo wanneer een metriek een bepaalde drempelwaarde overschrijden.
* **Configureer automatische acties**, zoals automatisch schalen van een resource of een runbook wordt gestart wanneer een metriek een bepaalde drempelwaarde overschrijden.
* **Geavanceerde analyses uitvoeren** of rapportage over trends prestatie- of informatie over het gebruik van de bron.
* **Archief** Hallo geschiedenis van prestaties of de status van de bron **voor naleving of controle** doeleinden.

## <a name="what-are-hello-characteristics-of-metrics"></a>Wat zijn Hallo kenmerken van metrische gegevens?
Metrische gegevens hebt Hallo volgende kenmerken:

* Alle metrische gegevens hebt **één minuut frequentie**. U ontvangt een metrische waarde elke minuut van uw resource zodat u bijna realtime zicht krijgt op Hallo status en de status van de resource.
* Metrische gegevens zijn **beschikbaar onmiddellijk**. Of u kunt geen tooopt in aanvullende diagnostische gegevens instellen.
* U hebt toegang tot **30 dagen van de geschiedenis** voor elke metriek. U kunt snel zoeken op Hallo recente en een maandelijkse trends in Hallo prestaties of de status van de resource.

U kunt ook:

* Configureren van een metriek **Waarschuwing regel waarmee u een melding verzendt of duurt automatische actie** wanneer Hallo metriek bestrijkt Hallo drempelwaarde die u hebt ingesteld. Automatisch schalen is een speciale geautomatiseerde actie waarmee tooscale uit uw resource toomeet inkomende aanvragen of wordt op uw website of de computerbronnen is geladen. U kunt een instelling voor automatisch schalen regel tooscale in- of uitzoomen op basis van een metriek een drempelwaarde overschrijden.

* **Route** alle metrische gegevens Application Insights of logboekanalyse (OMS) tooenable instant analytics, zoeken en aangepaste waarschuwingen op metrische gegevens van uw resources. U kunt ook streamen metrische gegevens tooan Event Hub, zodat u toothen routeren deze tooAzure Stream Analytics of toocustom apps voor vrijwel in realtime analyses. U instellen kunt de Event Hub met behulp van diagnostische instellingen voor streaming.

* **Archiveren van metrische gegevens toostorage** voor het bewaren van langer of te gebruiken voor het melden van offline. U kunt de metrische gegevens tooAzure Blob-opslag versturen bij het configureren van diagnostische instellingen voor uw resource.

* Eenvoudig detecteren, openen, en **alle metrische gegevens weergeven** via hello Azure-portal als u een resource selecteert en Hallo metrische gegevens in een grafiek te tekenen.

* **Verbruiken** Hallo metrische gegevens via Hallo nieuwe Azure Monitor REST-API's.

* **Query** metrische gegevens met behulp van PowerShell-cmdlets Hallo of Hallo platformoverschrijdende REST-API.

  ![Routering van metrische gegevens in Azure Monitor](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-hello-portal"></a>Toegang tot metrische gegevens via het Hallo-portal
Hier volgt een snel overzicht van hoe een metrische grafiek met behulp van toocreate hello Azure-portal.

### <a name="tooview-metrics-after-creating-a-resource"></a>tooview metrische gegevens na het maken van een resource
1. Open hello Azure-portal.
2. Maak een Azure App Service-website.
3. Nadat u een website gemaakt, gaat u toohello **overzicht** blade van Hallo-website.
4. U kunt bekijken nieuwe metrische gegevens als een **bewaking** tegel. U kunt bewerken Hallo tegel en meer metrische gegevens te selecteren.

   ![Metrische gegevens van een resource in de Azure-Monitor](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="tooaccess-all-metrics-in-a-single-place"></a>tooaccess alle metrische gegevens op één plaats
1. Open hello Azure-portal.
2. Navigeer toohello nieuwe **Monitor** tabblad en vervolgens en selecteer Hallo **metrische gegevens** optie eronder.
3. Selecteer uw abonnement, de resourcegroep en het Hallo-naam van Hallo resource in de vervolgkeuzelijst Hallo.
4. De lijst weergeven Hallo beschikbare metrische gegevens. Selecteer vervolgens Hallo metriek u geïnteresseerd bent in en het tekenen.
5. U kunt het vastmaken toohello dashboard door te klikken op Hallo pincode op Hallo rechterbovenhoek.

   ![Toegang tot alle metrische gegevens op één plaats in de Azure-Monitor](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> U toegang hebt tot hostniveau metrische gegevens van virtuele machines (op een Azure Resource Manager gebaseerde) en virtuele-machineschaalsets zonder aanvullende diagnostische instellingen. Deze nieuwe hostniveau metrische gegevens zijn beschikbaar voor Windows en Linux-exemplaren. Deze metrische gegevens zijn niet toobe verward met Hallo Guest-OS-niveau metrische gegevens die u hebt toegang toowhen die u diagnostische Azure-gegevens op uw virtuele machines of virtuele-machineschaalsets inschakelen. toolearn meer informatie over het configureren van diagnostische gegevens, Zie [wat is Microsoft Azure Diagnostics](../azure-diagnostics.md).
>
>

## <a name="access-metrics-via-hello-rest-api"></a>Toegang tot metrische gegevens via Hallo REST-API
Azure metrische gegevens zijn toegankelijk via hello Azure Monitor-API's. Er zijn twee API's die u helpen detecteren en toegang tot metrische gegevens:

* Gebruik Hallo [Azure Monitor metriek definities REST-API](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess Hallo lijst met metrische gegevens die beschikbaar voor een service zijn.
* Gebruik Hallo [REST API voor de metrische gegevens van de Monitor van de Azure](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess Hallo werkelijke metrische gegevens.

> [!NOTE]
> In dit artikel bevat informatie over metrische gegevens Hallo via Hallo [nieuwe API voor metrieken](https://msdn.microsoft.com/library/dn931930.aspx) voor Azure-resources. Hallo-API-versie voor Hallo nieuwe metrische definities API is 2016-03-01 en Hallo-versie voor metrieken API is 2016-09-01. Hallo verouderde metrische definities en metrische gegevens zijn toegankelijk door hello API versie 2014-04-01.
>
>

Zie voor een meer gedetailleerde uitleg Hallo Monitor REST-API's van Azure met [Azure Monitor REST-API-overzicht](monitoring-rest-api-walkthrough.md).

## <a name="export-metrics"></a>Metrische gegevens exporteren
U kunt gaan toohello **diagnostische instellingen** blade onder Hallo **Monitor** tabblad en bekijkt hello exportopties voor metrische gegevens. U kunt metrische gegevens (en de logboeken met diagnostische gegevens) toobe gerouteerd tooBlob opslag, tooAzure Event Hubs of tooOMS voor aanvragen die zijn vermeld eerder selecteren in dit artikel.

 ![Opties voor exporteren van metrische gegevens die in de Azure-Monitor](./media/monitoring-overview-metrics/MetricsOverview3.png)

U kunt dit configureren via Resource Manager-sjablonen, [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md), of [REST-API's](https://msdn.microsoft.com/library/dn931943.aspx).

## <a name="take-action-on-metrics"></a>Metrische gegevens van actie ondernemen
tooreceive meldingen of nemen geautomatiseerde acties op metrische gegevens, kunt u regels voor waarschuwingen of instellingen voor automatisch schalen configureren.

### <a name="configure-alert-rules"></a>Regels voor waarschuwingen configureren
U kunt regels voor waarschuwingen configureren op de metrische gegevens. Deze regels voor waarschuwingen kunnen controleren als een waarde een bepaalde drempelwaarde is overschreden. Ze kunnen vervolgens een melding via e-mail of een aangepast script van een webhook die gebruikte toorun kan worden gestart. U kunt ook Hallo webhook tooconfigure product van derden integraties gebruiken.

 ![Metrische gegevens en regels voor waarschuwingen in de Azure-Monitor](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a>Automatisch schalen van uw Azure resources
Sommige Azure-resources ondersteuning Hallo schalen of van meerdere exemplaren toohandle uw werkbelastingen. Automatisch schalen is van toepassing tooApp Service (Web Apps), de virtuele-machineschaalsets en de klassieke Azure-Cloud-Services. Wanneer een bepaalde meetwaarde die van invloed is op uw werkbelasting overschrijdt de drempelwaarde die u opgeeft, kunt u automatisch schalen regels tooscale of configureren. Zie voor meer informatie [overzicht van automatisch schalen](monitoring-overview-autoscale.md).

 ![Metrische gegevens en automatisch schalen in Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a>Meer informatie over ondersteunde services en metrische gegevens
Monitor voor Azure is een nieuwe infrastructuur met metrische gegevens. Het ondersteunt volgende op Azure-services in Azure portal en Hallo nieuwe versie van Azure Monitor API Hallo HALLO hallo:

* Virtuele machines (Azure Resource Manager gebaseerde)
* Virtuele-machineschaalsets
* Batch
* Event Hubs-naamruimte
* Service Bus-naamruimte (alleen premium SKU)
* SQL-Database (versie 12)
* Elastische SQL-groep
* Websites
* Webserver-farms
* Logic Apps
* IoT-hubs
* Redis Cache
* Netwerken: Toepassingsgateways
* Search

U kunt een gedetailleerde lijst met alle Hallo ondersteund services en hun metrische gegevens weergeven [Azure Monitor metrische gegevens--ondersteunde metrische gegevens per resourcetype](monitoring-supported-metrics.md).

## <a name="next-steps"></a>Volgende stappen
Raadpleeg toohello koppelingen in dit artikel. Bovendien kunt u meer over:  

* [Algemene metrische gegevens voor automatisch schalen](insights-autoscale-common-metrics.md)
* [Hoe toocreate waarschuwingsregels](insights-alerts-portal.md)
* [Logboeken van de Azure-opslag met logboekanalyse analyseren](../log-analytics/log-analytics-azure-storage.md)
