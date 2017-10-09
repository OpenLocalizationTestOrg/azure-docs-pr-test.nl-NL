---
title: aaaAzure Log Analytics query language-referentieoverzicht | Microsoft Docs
description: In dit artikel biedt hulp bij de overgang van nieuwe querytaal toohello voor logboekanalyse als u al bekend met verouderde Hallo-taal bent.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 8b4ee3d0b5e1ec8a9f95a09e0ad9835615ad1342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transitioning-tooazure-log-analytics-new-query-language"></a>Overgang van nieuwe querytaal van tooAzure Log Analytics

> [!NOTE]
> U vindt meer informatie over Hallo nieuwe logboekanalyse querytaal en ophalen van uw werkruimte op Upgrade procedure tooupgrade Hallo uw [Azure Log Analytics werkruimte toonew logboek zoeken](log-analytics-log-search-upgrade.md).

In dit artikel biedt hulp bij de overgang van nieuwe querytaal toohello voor logboekanalyse als u al bekend met verouderde Hallo-taal bent.

## <a name="language-converter"></a>Taal converter

Als u bekend met verouderde Log Analytics-querytaal hello bent, hello toocreate dezelfde query in de nieuwe taal Hallo Hallo gemakkelijkst toouse Hallo Converter taal die geïnstalleerd in Hallo logboek zoeken portal wanneer uw werkruimte is geconverteerd.  Het gebruik van Hallo converter is net zo eenvoudig als een verouderde query in de bovenste tekstvak Hallo typen en vervolgens te klikken op **converteren**.  U kunt klikt u op Hallo knop toorun Hallo zoekquery of kopiëren en plakken toouse deze ergens anders.

![Taal converter](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="cheat-sheet"></a>Overzichtskaart

Hallo volgende tabel bevat een vergelijking tussen een aantal algemene query's tooequivalent opdrachten tussen Hallo nieuwe en bestaande querytaal in Azure-logboekanalyse.

| Beschrijving | Verouderde | Nieuw |
|:--|:--|:--|
| Alle tabellen zoeken      | error | Zoek "error" (niet hoofdlettergevoelig) |
| Gegevens uit tabel selecteren | Type gebeurtenis = |  Gebeurtenis |
|                        | Type = gebeurtenis &#124; Selecteer de bron, EventLog, gebeurtenis-id | Gebeurtenis &#124; Project bron, EventLog, gebeurtenis-id |
|                        | Type = gebeurtenis &#124; Top 100 | Gebeurtenis &#124; 100 duren |
| Vergelijking van tekenreeksen      | Type gebeurtenis Computer=srv01.contoso.com =   | Gebeurtenis &#124; waar Computer == "srv01.contoso.com" |
|                        | Type gebeurtenis Computer=contains("contoso") = | Gebeurtenis &#124; Wanneer de Computer 'contoso' (niet hoofdlettergevoelig) bevat<br>Gebeurtenis &#124; waar Computer contains_cs 'Contoso' (hoofdlettergevoelig) |
|                        | Type gebeurtenis Computer = = RegEx ('@contoso@")  | Gebeurtenis &#124; Computer overeenkomt met de reguliere expressie '. *contoso*' |
| Datumvergelijking        | Type gebeurtenis TimeGenerated = > nu 1DAYS | Gebeurtenis &#124; waar TimeGenerated > ago(1d) |
|                        | Type gebeurtenis TimeGenerated = > 2017-05-01 TimeGenerated < 2017-05-31 | Gebeurtenis &#124; waar TimeGenerated tussen (datetime(2017-05-01)... DATETIME(2017-05-31)) |
| Boole-vergelijking     | Type Heartbeat IsGatewayInstalled = = false  | Heartbeat | waar IsGatewayInstalled == false |
| Sorteren                   | Type = gebeurtenis &#124; Computer asc, EventLog desc, EventLevelName asc sorteren | Gebeurtenis \| sorteren op de Computer asc, EventLog desc, EventLevelName asc |
| Afzonderlijke               | Type = gebeurtenis &#124; Ontdubbeling Computer \| Selecteer de Computer | Gebeurtenis &#124; EventLog-Computer samenvatten |
| Kolommen uitbreiden         | Type = Perf CounterName = "% processortijd" &#124; If(map(CounterValue,0,50,0,1),"HIGH","LOW") uitbreiden als verbruik | Perf &#124; Indien CounterName == '% processortijd' \| Gebruik uitbreiden iff = (tegenwaarde > 50, 'Hoog', 'Laag') |
| Aggregatie            | Type = gebeurtenis &#124; meting count() als tellen per Computer | Gebeurtenis &#124; Aantal samenvatten = count() door Computer |
|                                | Type = Perf ObjectName = Processor CounterName = "% processortijd" &#124; meting avg(CounterValue) door Computer interval van vijf minuten | Perf &#124; waar ObjectName == 'Processor' en CounterName == "% processortijd" &#124; overzicht van avg(CounterValue) door Computer bin (TimeGenerated, 5min) |
| Aggregatie met limiet | Type = gebeurtenis &#124; meting count() door Computer &#124; Top 10 | Gebeurtenis &#124; overzicht van AggregatedValue = count() door Computer &#124; limiet van 10 |
| Union                  | Type gebeurtenis of Type = = Syslog | Union-gebeurtenis Syslog |
| Koppelen                   | Type = NetworkMonitoring &#124; AgentIP inner join (Type = Heartbeat) ComputerIP | NetworkMonitoring &#124; type join interne = (Type Zoek == 'Heartbeat') op $left. AgentIP == $right.ComputerIP |



## <a name="next-steps"></a>Volgende stappen
- Bekijk een [zelfstudie over het schrijven van query's](https://go.microsoft.com/fwlink/?linkid=856078) Hallo nieuwe query language gebruiken.
- Raadpleeg toohello [Query Language Reference](https://go.microsoft.com/fwlink/?linkid=856079) voor meer informatie over alle opdracht, operators en functies voor het nieuwe querytaal Hallo.  
