---
title: een beheeroplossing voor in OMS aaaBuild | Microsoft Docs
description: Beheeroplossingen Hallo functionaliteit van Operations Management Suite (OMS) uitbreiden door verpakte beheerscenario dat klanten tootheir OMS-werkruimte kunnen toevoegen.  Dit artikel bevat informatie over hoe u management oplossingen toobe kunt maken in uw eigen omgeving gebruikt of beschikbaar tooyour klanten worden gemaakt.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dea4c0d9e608d9fe4aa41088705958c9fe999372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-build-a-management-solution-in-operations-management-suite-oms-preview"></a>Ontwerpen en bouwen van een beheeroplossing in Operations Management Suite (OMS) (Preview)
> [!NOTE]
> Dit is voorlopige documentatie voor het maken van oplossingen voor het beheer in OMS die zich momenteel in preview. De hieronder beschreven schema is onderwerp toochange.

[Oplossingen voor](operations-management-suite-solutions.md) Hallo functionaliteit van Operations Management Suite (OMS) uitbreiden door te geven verpakte beheerscenario dat klanten tootheir OMS-werkruimte kunnen toevoegen.  In dit artikel biedt een basisproces toodesign en bouwen van een beheersysteem dat geschikt is voor de meest voorkomende vereisten.  Als u nieuwe oplossingen voor het beheer van toobuilding kunt u dit proces als uitgangspunt gebruiken en vervolgens kunnen Hallo concepten voor complexere oplossingen zoals ontwikkelen van uw vereisten.

## <a name="what-is-a-management-solution"></a>Wat is een oplossing voor het beheer?

Beheeroplossingen bevatten OMS en Azure-resources die tooachieve een bepaald scenario bewaking samenwerken.  Ze worden geïmplementeerd als [Resource Management-sjablonen](../azure-resource-manager/resource-manager-template-walkthrough.md) die bevatten gedetailleerde informatie over de tooinstall en hun ingesloten resources configureren als oplossing voor Hallo is geïnstalleerd.

basic-strategie Hallo is toostart uw beheeroplossing op building Hallo afzonderlijke componenten in uw Azure-omgeving.  Wanneer er Hallo functionaliteit correct werkt, klikt u vervolgens kunt u beginnen verpakken in een [management oplossingsbestand](operations-management-suite-solutions-solution-file.md). 


## <a name="design-your-solution"></a>Ontwerp uw oplossing
Hallo meest voorkomende patroon voor een oplossing wordt weergegeven in Hallo volgende diagram.  Hallo verschillende onderdelen in dit patroon worden in Hallo hieronder beschreven.

![Overzicht van de OMS-oplossing](media/operations-management-suite-solutions/solution-overview.png)


### <a name="data-sources"></a>Gegevensbronnen
eerste stap bij het ontwerpen van een oplossing Hallo bepaald Hallo-gegevens die u nodig van Hallo Log Analytics-opslagplaats hebt.  Deze gegevens kan worden verzameld door een [gegevensbron](../log-analytics/log-analytics-data-sources.md) of [een andere oplossing](operations-management-suite-solutions.md), of moet uw oplossing tooprovide Hallo proces toocollect deze.

Er zijn een aantal manieren gegevensbronnen die kunnen worden verzameld in Hallo Log Analytics-opslagplaats, zoals beschreven in [gegevensbronnen in logboekanalyse](../log-analytics/log-analytics-data-sources.md).  Dit omvat de gebeurtenissen in het gebeurtenislogboek van Windows hello of die worden gegenereerd door Syslog bovendien tooperformance prestatiemeteritems voor Windows- en Linux-clients.  U kunt ook gegevens verzamelen van Azure-resources die door Azure Monitor worden verzameld.  

Als u gegevens die niet toegankelijk zijn via een van de beschikbare gegevensbronnen Hallo nodig hebt, dan kunt u Hallo [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) waarmee u toowrite toohello logboekanalyse gegevensopslagplaats vanaf elke client die een REST kunt aanroepen API.  Hallo meest voorkomende betekent aangepaste verzamelen van gegevens in een beheersysteem is toocreate een [runbook in Azure Automation](../automation/automation-runbook-types.md) die Hallo vereiste gegevens verzamelt van Azure of externe bronnen en maakt gebruik van Data Collector API toowrite Hallo toohello-opslagplaats.  

### <a name="log-searches"></a>Logboek zoekopdrachten
[Meld u zoekopdrachten](../log-analytics/log-analytics-log-searches.md) gebruikte tooextract zijn en analyseren in Hallo Log Analytics-opslagplaats.  Ze worden gebruikt door weergaven en waarschuwingen bij toevoeging tooallowing Hallo gebruiker tooperform ad-hoc analyse van gegevens in het Hallo-opslagplaats.  

U moet alle query's die u denkt dat handig toohello gebruiker worden zelfs als ze niet worden gebruikt door alle weergaven of waarschuwingen definiëren.  Dit zijn beschikbaar toothem als opgeslagen zoekacties in Hallo-portal en u kunt ook opnemen in een [lijst van query's visualisatie onderdeel](../log-analytics/log-analytics-view-designer-parts.md#list-of-queries-part) in uw aangepaste weergave.

### <a name="alerts"></a>Waarschuwingen
[Waarschuwingen in logboekanalyse](../log-analytics/log-analytics-alerts.md) geven aan welke problemen via [Meld zoekopdrachten](#log-searches) tegen Hallo-gegevens in het Hallo-opslagplaats.  Ze ofwel Hallo gebruiker waarschuwen of automatisch een actie wordt uitgevoerd in het antwoord. U moet verschillende waarschuwing voorwaarden voor uw toepassing te identificeren en bijbehorende waarschuwingsregels opnemen in uw oplossingsbestand.

Als Hallo probleem kan mogelijk worden opgelost met een geautomatiseerd proces, vervolgens maakt doorgaans u een runbook in Azure Automation tooperform dit herstel.  De meeste Azure-services kunnen worden beheerd met [cmdlets](/powershell/azure/overview) welke Hallo runbook zou gebruikmaken van tooperform dergelijke functionaliteit.

Als uw oplossing voor externe functionaliteit in antwoord tooan waarschuwing nodig heeft, dan kunt u een [webhook antwoord](../log-analytics/log-analytics-alerts-actions.md).  Hiermee kunt u toocall een externe webservice die informatie verzenden vanuit Hallo waarschuwing.

### <a name="views"></a>Weergaven
Weergaven in logboekanalyse zijn gebruikte toovisualize gegevens van Hallo Log Analytics-opslagplaats.  Elke oplossing bevatten doorgaans één weergave met een [tegel](../log-analytics/log-analytics-view-designer-tiles.md) die wordt weergegeven op het hoofddashboard Hallo van de gebruiker.  Hallo weergave mag een onbeperkt aantal [visualisatie delen](../log-analytics/log-analytics-view-designer-parts.md) tooprovide verschillende visualisaties van Hallo verzamelde gegevens toohello gebruiker.

U [aangepaste weergaven maken met de Hallo-ontwerper](../log-analytics/log-analytics-view-designer.md) die u kunt later exporteren voor insluiting in uw oplossingsbestand.  


## <a name="create-solution-file"></a>Oplossingsbestand maken
Nadat u hebt geconfigureerd en getest Hallo-onderdelen die deel van uw oplossing uitmaken, kunt u [maken van uw oplossingsbestand](operations-management-suite-solutions-solution-file.md).  U implementeert Hallo oplossingsonderdelen in een [Resource Manager-sjabloon](../azure-resource-manager/resource-group-authoring-templates.md) die bevat een [oplossing resource](operations-management-suite-solutions-solution-file.md#solution-resource) met relaties toohello Hallo andere resources in een bestand.  


## <a name="test-your-solution"></a>Testen van uw oplossing
Terwijl u uw oplossing ontwikkelt, u moet tooinstall en testen in uw werkruimte.  U kunt dit doen met behulp van een van de beschikbare methoden hello te[testen en installeren van Resource Manager-sjablonen](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="publish-your-solution"></a>Publiceren van uw oplossing
Zodra u hebt voltooid en uw oplossing getest, kunt u deze beschikbaar toocustomers via beide Hallo de volgende bronnen.

- **Azure-snelstartsjablonen**.  [Azure-snelstartsjablonen](https://azure.microsoft.com/resources/templates/) is een set van Resource Manager-sjablonen die is bijgedragen door Hallo community via GitHub.  U kunt uw oplossing beschikbaar maken door de volgende informatie in Hallo [bijdrage handleiding](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE).
- **Azure Marketplace**.  Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/) kunt u toodistribute en uw oplossing verkopen tooother ontwikkelaars, onafhankelijke softwareleveranciers, en IT-professionals.  U leert hoe toopublish uw oplossing tooAzure Marketplace op [hoe toopublish en beheren van een aanbieding in hello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).



## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[maken van een oplossingsbestand](operations-management-suite-solutions-solution-file.md) voor uw beheeroplossing.
* Meer details op Hallo van [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).
* Search [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates) voor voorbeelden van andere Resource Manager-sjablonen.