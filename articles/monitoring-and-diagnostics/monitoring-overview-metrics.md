---
title: Overzicht van metrische gegevens in Microsoft Azure | Microsoft Docs
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
ms.openlocfilehash: 3aff83ab2c157a18f4af6200a79bae7e5d6f0ea2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Overzicht van metrische gegevens in Microsoft Azure
Dit artikel wordt beschreven wat metrische gegevens zijn in Microsoft Azure, hun voordelen en het gebruik ervan.  

## <a name="what-are-metrics"></a>Wat zijn de metrische gegevens?
Monitor voor Azure kunt u telemetrie om meer inzicht verkrijgen in de prestaties en de status van uw workloads in Azure gebruiken. De belangrijkste type Azure telemetriegegevens is de metrische gegevens die (ook wel prestatiemeteritems) die door de meeste Azure-resources. Monitor voor Azure biedt verschillende manieren configureren en gebruiken van deze metrische gegevens voor bewaking en probleemoplossing.

## <a name="what-can-you-do-with-metrics"></a>Wat kunt u doen met metrische gegevens
Metrische gegevens zijn een waardevolle bron van Telemetrie en kunt u de volgende taken uitvoeren:

* **De prestaties bijhouden** van de bron (zoals een VM, website of logic app) door de metrische gegevens over een portal grafiek uitzetten en dat de grafiek aan een dashboard vastmaken.
* **Blijf op de hoogte van een probleem** die van invloed is op de prestaties van uw resource wanneer een metriek een bepaalde drempelwaarde overschrijden.
* **Configureer automatische acties**, zoals automatisch schalen van een resource of een runbook wordt gestart wanneer een metriek een bepaalde drempelwaarde overschrijden.
* **Geavanceerde analyses uitvoeren** of rapportage over trends prestatie- of informatie over het gebruik van de bron.
* **Archief** de geschiedenis van de prestaties of de status van de bron **voor naleving of controle** doeleinden.

## <a name="what-are-the-characteristics-of-metrics"></a>Wat zijn de kenmerken van metrische gegevens?
Metrische gegevens hebben de volgende kenmerken:

* Alle metrische gegevens hebt **één minuut frequentie**. U ontvangt een metrische waarde elke minuut van uw resource zodat u bijna real-time inzicht in de status en gezondheid van uw resource.
* Metrische gegevens zijn **beschikbaar onmiddellijk**. U hoeft niet te opt-in- of aanvullende diagnostische gegevens in te stellen.
* U hebt toegang tot **30 dagen van de geschiedenis** voor elke metriek. U kunt snel zoeken op de recente en een maandelijkse trends in de prestaties of de status van de resource.

U kunt ook:

* Configureren van een metriek **Waarschuwing regel waarmee u een melding verzendt of duurt automatische actie** wanneer de metriek overschrijdt de drempelwaarde die u hebt ingesteld. Automatisch schalen is een speciale geautomatiseerde actie op die u kunt u de bron om te voldoen aan de inkomende aanvragen worden uitgebreid of wordt op uw website of de computerbronnen is geladen. U kunt een regel van de instelling voor automatisch schalen schalen in- of configureren op basis van een metriek een drempelwaarde overschrijden.

* **Route** alle metrische gegevens Application Insights of logboekanalyse (OMS) om in te schakelen instant analytics, zoeken en aangepaste waarschuwingen op metrische gegevens van uw resources. U kunt ook de metrische gegevens naar een Event Hub, zodat u kunt ze vervolgens doorsturen naar Azure Stream Analytics of aangepaste apps voor vrijwel in realtime analyse streamen. U instellen kunt de Event Hub met behulp van diagnostische instellingen voor streaming.

* **Archiveren van metrische gegevens naar opslag** voor het bewaren van langer of te gebruiken voor het melden van offline. Bij het configureren van diagnostische instellingen voor uw resource, kunt u uw metrische gegevens routeren naar Azure Blob-opslag.

* Eenvoudig detecteren, openen, en **alle metrische gegevens weergeven** via Azure portal als u een resource selecteert en de metrische gegevens in een grafiek te tekenen.

* **Verbruiken** de metrische gegevens via de nieuwe Azure Monitor REST-API's.

* **Query** metrische gegevens met behulp van de PowerShell-cmdlets of de REST-API voor Cross-Platform.

  ![Routering van metrische gegevens in Azure Monitor](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-the-portal"></a>Toegang tot metrische gegevens via de portal
Hier volgt een snel overzicht van hoe een metrische grafiek te maken met behulp van de Azure-portal.

### <a name="to-view-metrics-after-creating-a-resource"></a>Metrische gegevens na het maken van een resource weergeven
1. Open de Azure-portal.
2. Maak een Azure App Service-website.
3. Nadat u een website gemaakt, gaat u naar de **overzicht** blade van de website.
4. U kunt bekijken nieuwe metrische gegevens als een **bewaking** tegel. U kunt de tegel bewerken en meer metrische gegevens te selecteren.

   ![Metrische gegevens van een resource in de Azure-Monitor](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="to-access-all-metrics-in-a-single-place"></a>Voor toegang tot alle metrische gegevens op één plaats
1. Open de Azure-portal.
2. Navigeer naar de nieuwe **Monitor** tabblad en vervolgens selecteert de **metrische gegevens** optie eronder.
3. Selecteer uw abonnement, resourcegroep en de naam van de resource in de vervolgkeuzelijst.
4. De lijst beschikbare metrische gegevens weergeven. Selecteer vervolgens de metriek u geïnteresseerd bent in en het tekenen.
5. U kunt het vastmaken aan het dashboard door te klikken op de pincode op de rechterbovenhoek.

   ![Toegang tot alle metrische gegevens op één plaats in de Azure-Monitor](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> U toegang hebt tot hostniveau metrische gegevens van virtuele machines (op een Azure Resource Manager gebaseerde) en virtuele-machineschaalsets zonder aanvullende diagnostische instellingen. Deze nieuwe hostniveau metrische gegevens zijn beschikbaar voor Windows en Linux-exemplaren. Deze metrische gegevens zijn niet te verwarren met de Guest-OS-niveau metrische gegevens die u hebt toegang tot wanneer u Azure diagnostische gegevens op uw virtuele machines of virtuele-machineschaalset sets inschakelen. Zie voor meer informatie over het configureren van diagnostische gegevens, [wat is Microsoft Azure Diagnostics](../azure-diagnostics.md).
>
>

## <a name="access-metrics-via-the-rest-api"></a>Toegang tot metrische gegevens via de REST-API
Azure metrische gegevens zijn toegankelijk via de Azure-Monitor API's. Er zijn twee API's die u helpen detecteren en toegang tot metrische gegevens:

* Gebruik de [Azure Monitor metriek definities REST-API](https://msdn.microsoft.com/library/mt743621.aspx) voor toegang tot de lijst met metrische gegevens die beschikbaar voor een service zijn.
* Gebruik de [REST API voor de metrische gegevens van de Monitor van de Azure](https://msdn.microsoft.com/library/mt743622.aspx) toegang tot de werkelijke metrische gegevens.

> [!NOTE]
> In dit artikel bevat informatie over de metrische gegevens via de [nieuwe API voor metrieken](https://msdn.microsoft.com/library/dn931930.aspx) voor Azure-resources. De API-versie voor de nieuwe metrische definities API 2016-03-01 is en de versie van metrische gegevens die API is 2016-09-01. De verouderde metrische definities en metrische gegevens kunnen worden geopend met de API-versie 2014-04-01.
>
>

Zie voor een meer gedetailleerd overzicht met de Azure-Monitor REST API's, [Azure Monitor REST-API-overzicht](monitoring-rest-api-walkthrough.md).

## <a name="export-metrics"></a>Metrische gegevens exporteren
Gaat u naar de **diagnostische instellingen** blade onder de **Monitor** tabblad en de opties voor exporteren van metrische gegevens weergeven. U kunt selecteren metrische gegevens (en diagnostische logboeken) worden doorgestuurd naar Blob storage, Azure Event Hubs of OMS voor use cases die eerder werden vermeld in dit artikel.

 ![Opties voor exporteren van metrische gegevens die in de Azure-Monitor](./media/monitoring-overview-metrics/MetricsOverview3.png)

U kunt dit configureren via Resource Manager-sjablonen, [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md), of [REST-API's](https://msdn.microsoft.com/library/dn931943.aspx).

## <a name="take-action-on-metrics"></a>Metrische gegevens van actie ondernemen
Als u meldingen ontvangen of geautomatiseerde acties ondernemen met metrische gegevens, kunt u regels voor waarschuwingen of instellingen voor automatisch schalen configureren.

### <a name="configure-alert-rules"></a>Regels voor waarschuwingen configureren
U kunt regels voor waarschuwingen configureren op de metrische gegevens. Deze regels voor waarschuwingen kunnen controleren als een waarde een bepaalde drempelwaarde is overschreden. Vervolgens kunnen ze u een melding via e-mail of gestart van een webhook die kan worden gebruikt om een aangepast script uitvoeren. U kunt ook de webhook gebruiken voor het product van derden integraties configureren.

 ![Metrische gegevens en regels voor waarschuwingen in de Azure-Monitor](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a>Automatisch schalen van uw Azure resources
Sommige Azure-resources ondersteuning voor het schalen of van meerdere exemplaren worden uw workloads verwerken. Automatisch schalen is van toepassing op App Service (Web-Apps), virtuele-machineschaalsets en klassieke Azure-Cloud-Services. U kunt regels voor automatisch schalen om te schalen of wanneer een bepaalde meetwaarde die van invloed is op uw werkbelasting overschrijdt de drempelwaarde die u opgeeft. Zie voor meer informatie [overzicht van automatisch schalen](monitoring-overview-autoscale.md).

 ![Metrische gegevens en automatisch schalen in Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a>Meer informatie over ondersteunde services en metrische gegevens
Monitor voor Azure is een nieuwe infrastructuur met metrische gegevens. Het ondersteunt de volgende Azure-services in de Azure portal en de nieuwe versie van de Monitor-API van Azure:

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

U kunt een gedetailleerde lijst met alle ondersteunde services en hun metrische gegevens weergeven [Azure Monitor metrische gegevens--ondersteunde metrische gegevens per resourcetype](monitoring-supported-metrics.md).

## <a name="next-steps"></a>Volgende stappen
Raadpleeg de koppelingen in dit artikel. Bovendien kunt u meer over:  

* [Algemene metrische gegevens voor automatisch schalen](insights-autoscale-common-metrics.md)
* [Het maken van regels voor waarschuwingen](insights-alerts-portal.md)
* [Logboeken van de Azure-opslag met logboekanalyse analyseren](../log-analytics/log-analytics-azure-storage.md)
