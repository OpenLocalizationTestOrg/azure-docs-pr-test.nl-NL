---
title: aaaWhat is logboekanalyse in Operations Management Suite (OMS)? | Microsoft Docs
description: Log Analytics is een service in Operations Management Suite (OMS) voor het verzamelen en analyseren van operationele gegevens die zijn gegenereerd door resources in uw cloud- en on-premises omgevingen.  Dit artikel bevat een kort overzicht van de verschillende onderdelen Hallo van logboekanalyse en koppelingen toodetailed inhoud.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: bd90b460-bacf-4345-ae31-26e155beac0e
ms.service: log-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: b35da77e3782f7c1fe54cc34142f8cd9f2eb57d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-log-analytics"></a>Wat is Log Analytics?
Log Analytics is een service in [Operations Management Suite \(OMS\) ](../operations-management-suite/operations-management-suite-overview.md) die uw cloud en on-premises omgevingen toomaintain bewaakt de beschikbaarheid en prestaties.  Gegevens die zijn gegenereerd door de resources in uw cloud en on-premises omgevingen en van andere bewaking extra tooprovide analysis over meerdere bronnen worden verzameld.  Dit artikel bevat een korte beschrijving van de waarde Hallo dat Log Analytics, een overzicht van hoe het werkt, en koppelingen toomore gedetailleerde inhoud zodat u kunt verder verdiepen.

## <a name="is-log-analytics-for-you"></a>Is Log Analytics iets voor u?
Als u op dit moment niet beschikt over een bewakingsfunctie voor uw Azure-omgeving, kunt u beginnen met [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md) om bewakingsgegevens voor uw Azure-resources te verzamelen en analyseren.  Log Analytics kunt [verzamelen van gegevens van Azure Monitor](log-analytics-azure-storage.md) toocorrelate met andere gegevens en bieden aanvullende analyse.

Als u uw on-premises omgeving toomonitor wilt of bestaande bewaking met services zoals Azure-Monitor of System Center Operations Manager hebt, kunt Log Analytics aanzienlijke waarde toevoegen.  De service kan namelijk rechtstreeks gegevens opvragen bij verschillende agents en bij deze andere services en verzamelen in één opslagplaats.  Analyseprogramma's in Log Analytics zoals zoeken in logboeken, weergaven en oplossingen worden toegepast op alle verzamelde gegevens zodat u op één plek toegang hebt tot een analyse van de hele omgeving.


## <a name="using-log-analytics"></a>Log Analytics gebruiken
Log Analytics is toegankelijk via Hallo OMS-portal of hello Azure-portal die worden uitgevoerd in een browser en bieden u met instellingen voor tooconfiguration en tooanalyze van meerdere hulpprogramma's en reageren op de verzamelde gegevens.  Vanuit Hallo portal kunt u gebruikmaken van [Meld zoekopdrachten](log-analytics-log-searches.md) waarbij het samenstellen van query's tooanalyze verzamelde gegevens, [dashboards](log-analytics-dashboards.md) die u kunt aanpassen met grafische weergave van uw waardevolste zoekopdrachten, en [oplossingen](log-analytics-add-solutions.md) die aanvullende functionaliteit en analyse hulpprogramma's bieden.

Hallo in onderstaande afbeelding is van Hallo OMS-portal welke toont Hallo-dashboard dat geeft samenvattingsinformatie weer voor Hallo [oplossingen](#add-functionality-with-management-solutions) die in de werkruimte Hallo worden geïnstalleerd.  U kunt klikken op een tegel toodrill verder in Hallo-gegevens voor deze oplossing.

![OMS-portal](media/log-analytics-overview/portal.png)

Log Analytics omvat een query language tooquickly ophalen en samenvoegen van gegevens in het Hallo-opslagplaats.  U kunt maken en opslaan [logboek zoekopdrachten](log-analytics-log-searches.md) toodirectly gegevens analyseren in de portal Hallo of logboek zoekopdrachten automatisch uitgevoerde diagnosetests toocreate een waarschuwing als Hallo resultaten van Hallo query een belangrijke voorwaarde aangeven.

![Zoekopdrachten in logboeken](media/log-analytics-overview/log-search.png)

een snelle grafische weergave van Hallo status van uw hele omgeving tooget, kunt u met visualisaties voor opgeslagen logboek zoekopdrachten tooyour toevoegen [dashboard](log-analytics-dashboards.md).   

![Dashboard](media/log-analytics-overview/dashboard.png)

Volgorde tooanalyze gegevens buiten Log Analytics, u kunt Hallo gegevens exporteren vanuit Hallo OMS-opslagplaats in hulpprogramma's zoals [Power BI](log-analytics-powerbi.md) of Excel.  U kunt ook gebruikmaken van Hallo [Log-API van zoekservice](log-analytics-log-search-api.md) toobuild aangepaste oplossingen die gebruikmaken van logboekanalyse gegevens of toointegrate met andere systemen.

## <a name="add-functionality-with-management-solutions"></a>Functionaliteit toevoegen met beheeroplossingen
[Oplossingen voor](log-analytics-add-solutions.md) functionaliteit tooOMS, aanvullende gegevens en analyse extra tooLog Analytics toevoegen.  Ze kunnen ook nieuwe recordtypen toobe verzameld die kan worden geanalyseerd met logboek zoekopdrachten of door aanvullende gebruikersinterface van Hallo-oplossing in Hallo dashboard definiëren.  Hallo voorbeeld in onderstaande afbeelding ziet u Hallo [oplossing bijhouden](log-analytics-change-tracking.md)

![Traceringsoplossingen wijzigen](media/log-analytics-overview/change-tracking.png)

Er zijn oplossingen voor allerlei functies en er worden elke dag weer nieuwe oplossingen toegevoegd.  Kunt u eenvoudig beschikbare oplossingen te bladeren en [ze tooyour OMS-werkruimte toevoegen](log-analytics-add-solutions.md) van Hallo oplossingen galerie of Azure Marketplace.  Veel van de oplossing worden automatisch geïmplementeerd en zijn direct bruikbaar, terwijl voor andere oplossingen mogelijk enige configuratie vereist is.

![Galerie van oplossingen](media/log-analytics-overview/solution-gallery.png)

## <a name="log-analytics-components"></a>Onderdelen van Log Analytics
Hallo is center logboekanalyse Hallo OMS-opslagplaats die wordt gehost in hello Azure-cloud.  Gegevens worden verzameld in Hallo opslagplaats van verbonden bronnen door configureren gegevensbronnen en toe te voegen oplossingen tooyour abonnement.  Gegevensbronnen en oplossingen maakt elk verschillende recordtypen die hun eigen set eigenschappen, maar nog steeds in query's toohello opslagplaats samen kunnen worden geanalyseerd.  Hiermee kunt u toouse Hallo dezelfde toowork in hulpprogramma's en -methoden met verschillende soorten gegevens verzameld door verschillende bronnen.

![OMS-opslagplaats](media/log-analytics-overview/overview.png)

Verbonden bronnen zijn Hallo computers en andere bronnen die gegevens verzameld door logboekanalyse genereren.  Dit kunnen agenten zijn die zijn geïnstalleerd op [Windows-](log-analytics-windows-agents.md) en [Linux](log-analytics-linux-agents.md)-computers die rechtstreeks verbinding maken of agenten in een [verbonden beheergroep van System Center Operations Manager](log-analytics-om-agents.md).  In het geval van Azure-resources verzamelt Log Analytics gegevens uit [Azure Monitor en Azure Diagnostics](log-analytics-azure-storage.md).

[Gegevensbronnen](log-analytics-data-sources.md) Hallo verschillende soorten gegevens verzameld van elke bron verbonden zijn.  Dit omvat [gebeurtenissen](log-analytics-data-sources-windows-events.md) en [prestatiegegevens](log-analytics-data-sources-performance-counters.md) van [Windows](log-analytics-data-sources-windows-events.md) en Linux-agents in toevoeging toosources zoals [IIS-logboeken](log-analytics-data-sources-iis-logs.md), en [aangepaste tekstlogboeken](log-analytics-data-sources-custom-logs.md).  U configureren elke gegevensbron dat u wilt dat toocollect en Hallo configuratie automatisch geleverde tooeach verbonden gegevensbron is.

Als u aangepaste vereisten hebt, dan kunt u Hallo [HTTP Data Collector API](log-analytics-data-collector-api.md) toowrite data toohello opslagplaats van een REST-API-client.

## <a name="log-analytics-architecture"></a>Architectuur van Log Analytics
vereisten voor de implementatie van logboekanalyse Hallo zijn minimale omdat Hallo centrale onderdelen worden gehost in hello Azure-cloud.  Dit omvat Hallo-opslagplaats in toevoeging toohello services kunnen u toocorrelate en de verzamelde gegevens te analyseren.  Hallo portal toegankelijk vanuit elke browser zodat er geen vereiste voor clientsoftware is.

U moet agenten installeren op [Windows](log-analytics-windows-agents.md)- en [Linux](log-analytics-linux-agents.md)-computers, maar er is geen aanvullende agent vereist voor computers die al lid van zijn een [verbonden SCOM-beheergroep](log-analytics-om-agents.md).  SCOM-agents blijven toocommunicate met beheerservers die hun gegevens tooLog Analytics doorstuurt.  Sommige oplossingen echter vereisen agents toocommunicate rechtstreeks met logboekanalyse.  Hallo-documentatie voor elke oplossing geeft de vereisten voor clientcommunicatie.

Wanneer u [zich aanmeldt voor Log Analytics](log-analytics-get-started.md), maakt u een OMS-werkruimte.  U kunt Hallo werkruimte beschouwen als een unieke Log Analytics-omgeving met een eigen data-opslagplaats, gegevensbronnen en oplossingen. U kunt meerdere werkruimten maken in uw abonnement toosupport omgevingen met meerdere zoals productie en testen.

![Architectuur van Log Analytics](media/log-analytics-overview/architecture.png)

## <a name="next-steps"></a>Volgende stappen
* [Aanmelden voor een gratis Log Analytics-account](log-analytics-get-started.md) tootest in uw eigen omgeving.
* Weergave Hallo verschillende [gegevensbronnen](log-analytics-data-sources.md) beschikbaar toocollect gegevens in Hallo OMS-opslagplaats.
* [Beschikbare oplossingen in de galerie met oplossingen Hallo Hallo Bladeren](log-analytics-add-solutions.md) tooadd functionaliteit tooLog Analytics.

