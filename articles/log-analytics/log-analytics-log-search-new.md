---
title: aaaLog zoekopdrachten in OMS Log Analytics | Microsoft Docs
description: U vereisen een zoekopdracht logboek tooretrieve geen gegevens van logboekanalyse.  Dit artikel wordt beschreven hoe nieuwe logboek zoekopdrachten worden gebruikt in Log Analytics en concepten, moet u toounderstand voordat deze is gemaakt.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 08fda1d9eb9e6ab824ffb9e12af09832c3e3fad2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a>Understanding logboek zoekt in Log Analytics

> [!NOTE]
> Dit artikel wordt beschreven logboek van zoekopdrachten in Azure-logboekanalyse Hallo nieuwe query language gebruiken.  U kunt meer informatie over de nieuwe taal Hallo en uw werkruimte op Hallo procedure tooupgrade ophalen [Upgrade van uw Azure-logboekanalyse werkruimte toonew logboek zoekopdracht](log-analytics-log-search-upgrade.md).  
>
> Als uw werkruimte niet bijgewerkte toohello nieuwe querytaal is, raadpleegt u te[vinden van gegevens met behulp van logboek zoekopdrachten in logboekanalyse](log-analytics-log-searches.md).

U vereisen een zoekopdracht logboek tooretrieve geen gegevens van logboekanalyse.  Of u bent analyseren van gegevens in de portal hello, configureren van een waarschuwingsregel toobe gewaarschuwd voor een bepaalde voorwaarde of de gegevens op te halen met behulp van Hallo Log Analytics-API, gaat u een zoekopdracht toospecify Hallo logboekgegevens gewenste.  Dit artikel wordt beschreven hoe logboek zoekopdrachten worden gebruikt in Log Analytics en concepten die u begrijpen moet voordat deze is gemaakt. Zie Hallo [Vervolgstappen](#next-steps) sectie voor meer informatie over het maken en bewerken van logboek zoekopdrachten en voor verwijzingen op Hallo querytaal.

## <a name="where-log-searches-are-used"></a>Waar logboek zoekopdrachten worden gebruikt

Hallo verschillende manieren die u logboek zoekopdrachten in logboekanalyse gebruikt zijn Hallo volgende:

- **Portals.** U interactieve analyses van gegevens kunt uitvoeren in Hallo-opslagplaats met Hallo [logboek zoeken portal](log-analytics-log-search-log-search-portal.md) of Hallo [Advanced Analytics-portal](https://go.microsoft.com/fwlink/?linkid=856587).  Hiermee kunt u tooedit uw vragen en te analyseren Hallo resulteert in verschillende indelingen en visualisaties.  De meeste query's die u maakt in een van de portals hello wordt gestart en vervolgens gekopieerd zodra u controleren of deze werkt zoals verwacht.
- **Regels voor waarschuwingen.** [Waarschuwing regels](log-analytics-alerts.md) proactief problemen van gegevens in uw werkruimte.  Elke waarschuwingsregel is gebaseerd op een logboek zoekopdracht die automatisch wordt uitgevoerd met regelmatige tussenpozen.  Hallo resultaten zijn domeinen toodetermine als een waarschuwing moet worden gemaakt.
- **Weergaven.**  U kunt visualisaties van gegevens toobe opgenomen in Gebruikersdashboards met maken [ontwerper](log-analytics-view-designer.md).  Logboek zoekopdrachten Hallo-gegevens die worden gebruikt door bieden [tegels](log-analytics-view-designer-tiles.md) en [visualisatie delen](log-analytics-view-designer-parts.md) in elke weergave.  U kunt inzoomen op uit visualisatie delen Hallo logboek zoeken portal tooperform verdere analyse op Hallo-gegevens.
- **Exporteren.**  Wanneer u gegevens uit Hallo Log Analytics-werkruimte tooExcel exporteren of [Power BI](log-analytics-powerbi.md), hebt u een logboek zoeken toodefine Hallo gegevens tooexport.
- **PowerShell.** U kunt een PowerShell-script uitvoeren vanaf een opdrachtregel of een Azure Automation-runbook die gebruikmaakt van [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) tooretrieve gegevens van logboekanalyse.  Deze cmdlet is een query toodetermine Hallo gegevens tooretrieve vereist.
- **Log Analytics-API.**  Hallo [Log Analytics-API van zoekservice Meld](log-analytics-log-search-api.md) kan een REST-API-client tooretrieve gegevens van Hallo-werkruimte.  Hallo-API-aanvraag bevat een query die wordt uitgevoerd op logboekanalyse toodetermine Hallo gegevens tooretrieve.

![Logboek zoekopdrachten](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a>De structuur van Log Analytics-gegevens
Als u een query bouwen, begint u met het bepalen van welke tabellen Hallo gegevens hebt die u zoekt. Elke [gegevensbron](log-analytics-data-sources.md) en [oplossing](../operations-management-suite/operations-management-suite-solutions.md) gegevens opslaat in de speciale tabellen in de werkruimte voor logboekanalyse Hallo.  Documentatie voor elke gegevensbron en de oplossing bevat Hallo-naam van Hallo-gegevenstype dat wordt gemaakt en een beschrijving van elk van de eigenschappen ervan.     Groot aantal query's moet alleen gegevens uit een enkele tabellen, maar anderen tal van opties tooinclude gegevens uit meerdere tabellen kunnen gebruiken.

![Tabellen](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a>Een query schrijven
Hallo-kern van logboek zoekopdrachten in logboekanalyse is [een uitgebreide querytaal](https://docs.loganalytics.io/) waarmee u ophalen en analyseren van gegevens uit de opslagplaats Hallo in tal van manieren.  Deze zelfde querytaal wordt gebruikt voor [Application Insights](../application-insights/app-insights-analytics.md).  Leren hoe toowrite een query kritieke toocreating logboek zoekopdrachten in logboekanalyse is.  U doorgaans beginnen met een eenvoudige query's en vervolgens uitgevoerd toouse meer geavanceerde functies zoals steeds ingewikkelder worden uw vereisten.

Hallo basisstructuur van een query is een brontabel gevolgd door een reeks operators gescheiden door een sluisteken `|`.  U kunt een keten van meerdere operators toorefine Hallo gegevens en geavanceerde functies uitvoeren.

Stel bijvoorbeeld dat u deze wilde toofind Hallo top tien computers Hello meeste foutgebeurtenissen via Hallo afgelopen dag.

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

Of misschien wilt u toofind dat computers die nog niet als een heartbeat in Hallo laatste dag hebben.

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

Hoe zit een lijndiagram met Hallo processorgebruik voor elke computer in de afgelopen week?

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

U kunt zien van deze snelle voorbeelden die ongeacht Hallo soort gegevens die u werkt met, Hallo structuur van Hallo-query is vergelijkbaar.  U kunt opsplitsen in afzonderlijke stappen waarbij Hallo resulterende gegevens van een opdracht wordt verzonden via de volgende opdracht voor toohello Hallo-pijplijn.

Zie voor volledige documentatie over hello Azure Log Analytics-querytaal inclusief zelfstudies en taalreferentie Hallo [Azure Log Analytics query language-documentatie](https://docs.loganalytics.io/).

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over Hallo [portals toocreate te gebruiken en bewerken van logboek zoekopdrachten](log-analytics-log-search-portals.md).
- Bekijk een [zelfstudie over het schrijven van query's](https://go.microsoft.com/fwlink/?linkid=856078) Hallo nieuwe query language gebruiken.
