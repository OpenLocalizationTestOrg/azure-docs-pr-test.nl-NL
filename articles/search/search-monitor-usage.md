---
title: aaaMonitor gebruiks- en statistieken in een Azure Search-service | Microsoft Docs
description: Bijhouden resourcegrootte verbruik en de index voor Azure Search, een gehoste cloud search-service op Microsoft Azure.
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
tags: azure-portal
ms.assetid: 122948de-d29a-426e-88b4-58cbcee4bc23
ms.service: search
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/01/2017
ms.author: betorres
ms.openlocfilehash: f38eabb5d04a410e11eaaff22157da8aba9e4845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-an-azure-search-service"></a>Een Azure Search-service controleren

Azure Search biedt verschillende bronnen voor het bijhouden van gebruik en prestaties van de search-services. Dit biedt u toegang tot toometrics, Logboeken, indexstatistieken en uitgebreide bewakingsmogelijkheden Power BI. Dit artikel wordt beschreven hoe tooenable Hallo verschillende strategieën voor bewaking en hoe toointerpret Hallo resulterende gegevens.

## <a name="azure-search-metrics"></a>Azure Search metrische gegevens
Metrische gegevens bieden u bijna real-time inzicht in uw zoekservice en beschikbaar zijn voor elke service, zonder aanvullende instellingen. Ze kunnen u de prestaties van uw service voor too30 dagen Hallo bijhouden.

Azure Search worden gegevens verzameld voor drie verschillende metrische gegevens:

* Latentie zoeken: tijd Hallo search-service nodig tooprocess zoekopdrachten, geaggregeerd per minuut.
* Zoekquery's per seconde (QPS): het aantal zoekresultaten ontvangen per seconde, query's per minuut geaggregeerd.
* Beperkte zoekopdracht query percentage: Percentage zoekquery's die zijn beperkt, geaggregeerd per minuut.

![Schermopname van QPS activiteit][1]

### <a name="set-up-alerts"></a>waarschuwingen instellen
Hallo metrische detail pagina kunt u waarschuwingen tootrigger een e-mailbericht of een geautomatiseerde actie wanneer een metriek overschrijdt de drempelwaarde die u hebt gedefinieerd.

Controleer voor meer informatie over metrische gegevens Hallo volledige documentatie over Azure-Monitor.  

## <a name="how-tootrack-resource-usage"></a>Hoe tootrack Resourcegebruik
Hallo groei van indexen en de documentgrootte van het bijhouden, kunt u proactief capaciteit aanpassen voordat het roept Hallo bovengrens die u hebt ingesteld voor uw service. U kunt dit doen op Hallo portal of programmatisch met Hallo REST-API.

### <a name="using-hello-portal"></a>Met behulp van Hallo-portal

toomonitor Resourcegebruik, Hallo tellingen en statistieken voor uw service weergeven in Hallo [portal](https://portal.azure.com).

1. Meld u aan toohello [portal](https://portal.azure.com).
2. Open het servicedashboard Hallo van uw Azure Search-service. Tegels voor Hallo-service vindt u op de startpagina Hallo of kunt u toohello-service van bladeren op Hallo Snelbalk bladeren.

Hallo gebruik sectie bevat een meter die aangeeft welk gedeelte van de beschikbare resources zijn momenteel in gebruik. Zie voor informatie over de beperkingen van de per-service voor indexen, documenten en opslag, [Servicelimieten](search-limits-quotas-capacity.md).

  ![Tegel gebruik][2]

> [!NOTE]
> Hallo bovenstaande is voor de gratis service hello, die is maximaal één replica en elke partitie en kan alleen host 3 indexen, 10.000 documenten of 50 MB aan gegevens, afhankelijk van wat zich het eerste voordoet. Services die zijn gemaakt op een Basic- of Standard-laag een veel grotere Servicelimieten. Zie voor meer informatie over het kiezen van een laag [kiest u een laag of SKU](search-sku-tier.md).
>
>

### <a name="using-hello-rest-api"></a>Met behulp van Hallo REST-API
Bieden toegang op programmeerniveau tooservice metrische gegevens zowel hello Azure Search REST-API en Hallo .NET SDK.  Als u [indexeerfuncties](https://msdn.microsoft.com/library/azure/dn946891.aspx) tooload een index van Azure SQL Database- of Azure Cosmos DB een extra API is beschikbaar tooget Hallo cijfers die u nodig hebt.

* [Indexstatistieken opvragen](/rest/api/searchservice/get-index-statistics)
* [Aantal documenten](/rest/api/searchservice/count-documents)
* [Status van de indexeerfunctie ophalen](/rest/api/searchservice/get-indexer-status)

## <a name="how-tooexport-logs-and-metrics"></a>Hoe tooexport registreert en metrische gegevens

U kunt Hallo bewerkingslogboeken voor uw service en Hallo onbewerkte gegevens van Hallo metrische gegevens die zijn beschreven in voorgaande sectie Hallo exporteren. Bewerkingslogboeken laten u weten hoe Hallo-service wordt gebruikt en kan worden gebruikt vanuit Power BI als gegevens gekopieerd tooa storage-account. Azure search biedt een controle Power BI-inhoudspakket voor dit doel.


### <a name="enabling-monitoring"></a>Controle inschakelen
Open uw Azure Search-service in Hallo [Azure-portal](http://portal.azure.com) onder Hallo optie bewaking inschakelen.

Hallo-gegevens te selecteren die u wilt dat tooexport: Logboeken, metrische gegevens of beide. U kunt kopiëren tooa storage-account, deze tooan event hub te verzenden of exporteren tooLog Analytics.

![Hoe tooenable bewaking in Hallo-portal][3]

met PowerShell of Azure CLI Hallo tooenable Zie Hallo documentatie [hier](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs).

### <a name="logs-and-metrics-schemas"></a>Schema's voor logboeken en metrische gegevens
Wanneer gegevens Hallo gekopieerde tooa opslag is account, hello gegevens zijn opgemaakt als JSON en de plaats in twee containers:

* Insights-logboeken-operationlogs: voor verkeerslogboeken zoeken
* Insights-metrics-pt1m: van metrische gegevens

Er is een blob, per uur, per container.

Voorbeeldpad:`resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`

#### <a name="log-schema"></a>Logboek schema
Hallo logboeken blobs bevatten uw verkeerslogboeken search-service.
Elke blob heeft een basis-object aangeroepen **records** die een matrix van logboek-objecten bevat.
Elke blob heeft records op alle Hallo-bewerking die plaatsgevonden tijdens het Hallo heeft hetzelfde uur.

| Naam | Type | Voorbeeld | Opmerkingen |
| --- | --- | --- | --- |
| tijd |Datum/tijd |' 2015-12-07T00:00:43.6872559Z ' |Tijdstempel van Hallo-bewerking |
| resourceId |Tekenreeks |"/ SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111 /<br/>STANDAARD-RESOURCEGROUPS-PROVIDERS /<br/> MICROSOFT CORPORATION. SEARCHSERVICES-ZOEKOPDRACHT/SEARCHSERVICE' |Uw ResourceId |
| operationName |Tekenreeks |'Query.Search' |Hallo-naam van Hallo-bewerking |
| operationVersion |Tekenreeks |"2015-02-28" |Hallo-api-versie die wordt gebruikt |
| category |Tekenreeks |'OperationLogs' |constante |
| resultType |Tekenreeks |'Geslaagd' |Mogelijke waarden: geslaagd of mislukt |
| resultSignature |int |200 |HTTP-resultaatcode |
| durationMS |int |50 |Duur van de bewerking Hallo in milliseconden |
| properties |object |Zie tabel Hallo |Object met de bewerking-specifieke gegevens |

**Eigenschappen schema**
| Naam | Type | Voorbeeld | Opmerkingen |
| --- | --- | --- | --- |
| Beschrijving |Tekenreeks |'/Indexes('content')/docs ophalen' |eindpunt van de bewerking Hallo |
| Query’s uitvoeren |Tekenreeks |'? zoeken = AzureSearch & in $count = true & api-version = 2015-02-28 ' |Hallo queryparameters |
| Documenten |int |42 |Aantal verwerkte documenten |
| NaamCommunity |Tekenreeks |'testindex' |Naam van Hallo-index die is gekoppeld aan het Hallo-bewerking |

#### <a name="metrics-schema"></a>Schema van de metrische gegevens
| Naam | Type | Voorbeeld | Opmerkingen |
| --- | --- | --- | --- |
| resourceId |Tekenreeks |"/ SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111 /<br/>STANDAARD-RESOURCEGROUPS-PROVIDERS /<br/>MICROSOFT CORPORATION. SEARCHSERVICES-ZOEKOPDRACHT/SEARCHSERVICE' |de resource-id |
| metricName |Tekenreeks |'Latentie' |Hallo-naam van Hallo metrische gegevens |
| tijd |Datum/tijd |' 2015-12-07T00:00:43.6872559Z ' |de tijdstempel van Hallo bewerking |
| Gemiddelde |int |64 |Hallo gemiddelde waarde van onbewerkte Hallo-voorbeelden in Hallo metrisch tijdsinterval |
| minimale |int |37 |de minimumwaarde Hallo van onbewerkte Hallo-voorbeelden in Hallo metrisch tijdsinterval |
| Maximum |int |78 |Hallo maximumwaarde van onbewerkte Hallo-voorbeelden in Hallo metrisch tijdsinterval |
| Totaal |int |258 |Hallo totaalwaarde van onbewerkte Hallo-voorbeelden in Hallo metrisch tijdsinterval |
| Aantal |int |4 |het aantal steekproeven dat onbewerkte Hallo toogenerate Hallo metriek gebruikt |
| timegrain |Tekenreeks |'PT1M' |Hallo tijdgranulariteit Hallo metrische gegevens in de ISO 8601 |

Alle metrische gegevens worden gerapporteerd in intervallen van één minuut. Elke metriek wordt de minimum, maximum en gemiddelde waarden per minuut.

Voor Hallo SearchQueriesPerSecond metriek is minimaal de laagste waarde Hallo voor zoekquery's per seconde dat is geregistreerd in die minuut. Hallo geldt toohello maximumwaarde. Gemiddelde, is cumulatieve Hallo voor Hallo gehele minuut.
Denk aan dit scenario in één minuut: één seconde van hoge belasting hello maximum zijn voor SearchQueriesPerSecond, gevolgd door 58 seconden gemiddelde belasting, en ten slotte één seconde met slechts één query die Hallo minimale.

ThrottledSearchQueriesPercentage, minimum, maximum, gemiddelde en totaal, een hebben Hallo dezelfde waarde: percentage van de zoekquery's die zijn beperkt van totaal aantal zoekopdrachten in één minuut Hallo Hallo.

## <a name="analyzing-your-data-with-power-bi"></a>Analyseren van uw gegevens met Power BI

Wordt u aangeraden [Power BI](https://powerbi.microsoft.com) tooexplore en uw gegevens te visualiseren. U kunt gemakkelijk verbinding maken tooyour Azure Storage-Account en snel starten analyseren van uw gegevens.

Azure Search biedt een [Power BI-inhoudspakket](https://app.powerbi.com/getdata/services/azure-search) kunt u toomonitor en inzicht in uw search-verkeer met vooraf gedefinieerde grafieken en tabellen. Het bevat een set van Power BI-rapporten die automatisch verbinding maken met tooyour gegevens en visuele inzicht bieden over uw search-service. Zie voor meer informatie, Hallo [inhoudspakket help-pagina](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/).

![Power BI-dashboard voor Azure Search][4]

## <a name="next-steps"></a>Volgende stappen
Bekijk [schalen van replica's en partities](search-limits-quotas-capacity.md) voor instructies over hoe toobalance Hallo toewijzing van partities en replica's voor een bestaande service.

Ga naar [beheren van uw zoekservice in Microsoft Azure](search-manage.md) voor meer informatie over servicebeheer of [prestaties en optimalisatie](search-performance-optimization.md) voor afstemming richtlijnen.

Meer informatie over het maken van fantastische rapporten. Zie [aan de slag met Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/) voor meer informatie

<!--Image references-->
[1]: ./media/search-monitor-usage/AzSearch-Monitor-BarChart.PNG
[2]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG
[3]: ./media/search-monitor-usage/AzureSearch-Enable-Monitoring.PNG
[4]: ./media/search-monitor-usage/AzureSearch-PowerBI-Dashboard.png
