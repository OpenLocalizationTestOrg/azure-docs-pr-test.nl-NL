---
title: aaaUnderstanding waarschuwingen in de Azure Log Analytics | Microsoft Docs
description: Waarschuwingen in logboekanalyse belangrijke informatie in de OMS-opslagplaats te identificeren en op de proactief kunnen zullen u informeren over problemen of acties tooattempt toocorrect aanroepen ze.  Dit artikel wordt beschreven Hallo verschillende soorten waarschuwingsregels en hoe ze worden gedefinieerd.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: bfa0a5aaeca81674e79a6d647f36d937efeeb439
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-alerts-in-log-analytics"></a>Informatie over waarschuwingen in Log Analytics

Waarschuwingen in logboekanalyse identificeren belangrijke informatie in de opslagplaats Log Analytics.  In dit artikel vindt u informatie over hoe waarschuwingsregels in logboekanalyse werk en beschrijft Hallo verschillen tussen de verschillende typen regels voor waarschuwingen.

Zie voor Hallo-proces voor het maken van regels voor waarschuwingen, Hallo artikelen te volgen:

- Maken van regels voor waarschuwingen met [Azure-portal](log-analytics-alerts-creating.md)
- Maken van regels voor waarschuwingen met [Resource Manager-sjabloon](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md)
- Maken van regels voor waarschuwingen met [REST-API](log-analytics-api-alerts.md)


## <a name="alert-rules"></a>Regels voor waarschuwingen

Waarschuwingen worden gemaakt door regels voor waarschuwingen die automatisch logboek zoekopdrachten met regelmatige tussenpozen worden uitgevoerd.  Een waarschuwing record wordt gemaakt als Hallo resultaten van Hallo logboek zoekopdracht aan bepaalde criteria voldoen.  Hallo regel kan automatisch voert vervolgens een of meer acties tooproactively zullen u informeren over Hallo waarschuwing of aanroepen van een ander proces.  Verschillende soorten waarschuwingsregels gebruiken verschillende logica tooperform deze analyse.

![Waarschuwingen in Log Analytics](media/log-analytics-alerts/overview.png)

Waarschuwingsregels worden gedefinieerd door Hallo volgende details:

- **Logboek zoeken**.  Hallo-query die wordt uitgevoerd telkens als Hallo waarschuwingsregel wordt geactiveerd.  Hallo-records geretourneerd door deze query is gebruikt toodetermine of een waarschuwing wordt gemaakt.
- **Tijdvenster**.  Hiermee geeft u een tijdsbereik Hallo voor Hallo-query.  Hallo query retourneert alleen de records die zijn gemaakt binnen dit bereik Hallo huidige tijd.  Dit kan een waarde tussen 5 minuten en 24 uur zijn. Als hello tijd ingesteld too60 minuten en Hallo query wordt uitgevoerd om 1:15 uur, wordt bijvoorbeeld alleen de records die zijn gemaakt tussen 12:15 uur en 1:15 PM geretourneerd.
- **Frequentie**.  Hiermee geeft u op hoe vaak hello query moet worden uitgevoerd. Is een waarde tussen 5 minuten en 24 uur. Moet gelijk tooor kleiner is dan Hallo tijdvenster.  Als het Hallo-waarde groter is dan het tijdvenster hello, risico u records wordt overgeslagen.<br>Neem bijvoorbeeld een tijdvenster van 30 minuten en een frequentie van 60 minuten.  Als het Hallo-query wordt uitgevoerd om 1:00 uur, wordt er records tussen 12:30 en 13:00 uur.  Hallo is Hallo query wordt uitgevoerd zodra 2:00 wanneer er records tussen 1:30 en 2:00 zou geretourneerd.  Alle records gemaakt tussen de 1:00 en 1:30 zou nooit worden geëvalueerd.
- **Drempelwaarde**.  Hallo resultaten van Hallo logboek search zijn geëvalueerd toodetermine of een waarschuwing moet worden gemaakt.  Hallo drempelwaarde verschilt voor verschillende soorten waarschuwingsregels Hallo.

Elke waarschuwingsregel in Log Analytics is een van twee typen.  Elk van deze typen is beschreven in het Hallo-secties die volgen.

- **[Aantal resultaten](#number-of-results-alert-rules)**. Één waarschuwing gemaakt wanneer Hallo aantal records geretourneerd door Hallo logboek zoekopdracht meer dan een opgegeven getal.
- **[Metrische meting](#metric-measurement-alert-rules)**.  De waarschuwing is gemaakt voor elk object in de resultaten Hallo van Hallo logboek zoeken met waarden die groter zijn dan de opgegeven drempelwaarde.

Hallo verschillen tussen waarschuwingsregel typen zijn als volgt.

- **Aantal resultaten** waarschuwingsregel maakt altijd één waarschuwing even **metrische meting** waarschuwingsregel maakt een waarschuwing voor elk object dat Hallo drempelwaarde overschrijdt.
- **Aantal resultaten** waarschuwingsregels genereren een waarschuwing als Hallo drempelwaarde één keer wordt overschreden. **Metrische meting** waarschuwingsregels kunnen genereren een waarschuwing als het Hallo-drempelwaarde is overschreden een bepaald aantal keren gedurende een bepaald tijdsinterval.

## <a name="number-of-results-alert-rules"></a>Aantal resultaten waarschuwingsregels
**Aantal resultaten** waarschuwingsregels maken van één waarschuwing wanneer het aantal records dat wordt geretourneerd door de zoekquery Hallo HALLO hallo opgegeven drempelwaarde overschrijden.

### <a name="threshold"></a>Drempelwaarde
Hallo-drempelwaarde voor een **aantal resultaten** waarschuwingsregel gewoon groter is dan of kleiner is dan een bepaalde waarde.  Als het aantal records dat wordt geretourneerd door de zoekfunctie Hallo Hallo aan deze criteria voldoen, wordt een waarschuwing gemaakt.

### <a name="scenarios"></a>Scenario's

#### <a name="events"></a>Gebeurtenissen
Dit type waarschuwingsregel is ideaal voor het werken met gebeurtenissen, zoals Windows-gebeurtenislogboeken, Syslog, en aangepaste logboeken.  U kunt toocreate een waarschuwing wanneer een bepaalde foutgebeurtenis wordt gemaakt, of wanneer er meerdere foutgebeurtenissen worden gemaakt binnen een bepaalde periode.

tooalert op één gebeurtenis Hallo aantal resultaten toogreater dan 0 en beide Hallo frequentie instellen en tijd van venster too5 minuten.  Die Hallo query wordt uitgevoerd elke 5 minuten en controleren op Hallo exemplaar van een enkelvoudige gebeurtenis die is gemaakt sinds de laatste query waarvoor tijd Hallo Hallo werd uitgevoerd.  Een langer frequentie mogelijk vertraagd Hallo tijd tussen het Hallo-gebeurtenis wordt verzameld en Hallo waarschuwing wordt gemaakt.

Sommige toepassingen kunnen zich aanmelden voor een incidentele fout die mag niet per se een melding kan genereren.  Hallo-toepassing kan bijvoorbeeld probeer Hallo-proces dat Hallo foutgebeurtenis gemaakt en slaagt de Hallo volgende keer.  In dit geval kunt u geen toocreate Hallo waarschuwing tenzij meerdere gebeurtenissen worden gemaakt binnen een bepaalde periode.  

In sommige gevallen kunt u een waarschuwing toocreate Hallo ontbreken van een gebeurtenis.  Bijvoorbeeld, een proces kan zich aanmelden tooindicate reguliere gebeurtenissen die deze correct werkt.  Als deze niet een van deze gebeurtenissen binnen een bepaalde periode, moet een waarschuwing worden gemaakt.  In dit geval stelt u Hallo drempel te**minder dan 1**.

#### <a name="performance-alerts"></a>Waarschuwingen over toepassingsprestaties
[Prestatiegegevens](log-analytics-data-sources-performance-counters.md) als records in de OMS-opslagplaats vergelijkbare tooevents hello wordt opgeslagen.  Als u tooalert wilt wanneer een prestatiemeteritem een bepaalde drempelwaarde overschrijdt, moet deze drempelwaarde worden opgenomen in Hallo-query.

Bijvoorbeeld, als u deze wilde tooalert wanneer hello processor wordt uitgevoerd via 90%, gebruikt u een query zoals Hallo volgen met Hallo drempelwaarde voor de waarschuwingsregel Hallo **groter dan 0**.

    Type=Perf ObjectName=Processor CounterName="% Processor Time" CounterValue>90

Als u deze tooalert wilde wanneer Hallo processor gemiddeld meer dan 90% voor een bepaalde periode, gebruikt u een query met Hallo [opdracht meten](log-analytics-search-reference.md#commands) Hallo volgende Hallo drempelwaarde voor de waarschuwingsregel hello, zoals **groter dan 0** .

    Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer | where AggregatedValue>90

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query's zou Wijzig toohello volgende:`Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" and CounterValue>90`
> `Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" | summarize avg(CounterValue) by Computer | where CounterValue>90`


## <a name="metric-measurement-alert-rules"></a>Waarschuwingsregels metrische meting

>[!NOTE]
> Waarschuwingsregels metrische meting zijn momenteel in de openbare preview.

**Metrische meting** waarschuwingsregels maakt een waarschuwing voor elk object in een query met een waarde die een opgegeven drempelwaarde overschrijdt.  Ze hebben Hallo duidelijke verschillen van volgende **aantal resultaten** waarschuwing regels.

#### <a name="log-search"></a>Zoekopdrachten in logboeken
Tijdens het gebruik van een query voor een **aantal resultaten** waarschuwing sluiten, er zijn specifieke vereisten Hallo query voor een waarschuwingsregel metrische meting.  Het omvat een [opdracht meten](log-analytics-search-reference.md#commands) toogroup Hallo resultaten op een bepaald veld. Met deze opdracht moet Hallo volgende elementen bevatten.

- **Statistische functie**.  Hallo-berekening die wordt uitgevoerd en mogelijk een numeriek veld tooaggregate bepaalt.  Bijvoorbeeld: **count()** Hallo aantal records dat wordt geretourneerd in Hallo query, **avg(CounterValue)** Hallo gemiddelde van Hallo tegenwaarde veld via hello-interval wordt geretourneerd.
- **Veld groeperen**.  Een record met een cumulatieve waarde voor elk exemplaar van dit veld wordt gemaakt en een waarschuwing worden gegenereerd voor elk.  Bijvoorbeeld, als u een waarschuwing toogenerate voor elke computer wilde, gebruikt u **door Computer**.   
- **Interval**.  Hiermee definieert u Hallo tijdsinterval waarover Hallo gegevens worden samengevoegd.  Bijvoorbeeld, als u hebt opgegeven **5minutes**, een record voor elk exemplaar van Hallo groepsveld om de 5 minuten gedurende Hallo tijdvenster opgegeven voor de waarschuwing Hallo geaggregeerd zouden worden gemaakt.

#### <a name="threshold"></a>Drempelwaarde
Hallo-drempelwaarde voor metrische meting waarschuwingsregels is gedefinieerd door een cumulatieve waarde en een aantal schendingen.  Als alle gegevenspunten in Hallo logboek zoeken deze waarde overschrijdt, heeft deze beschouwd als een schending.  Als het aantal schendingen in voor elk object in de resultaten van de Hallo Hallo overschrijdt Hallo opgegeven waarde, wordt een waarschuwing gemaakt voor dat object.

#### <a name="example"></a>Voorbeeld
Overweeg een scenario waarin het gewenste een waarschuwing als een computer processorgebruik van 90% driemaal gedurende 30 minuten overschreden.  U zou een waarschuwingsregel maken met de volgende details Hallo.  

**Query:** Type = Perf ObjectName = Processor CounterName = "% processortijd" | meten avg(CounterValue) per Computer Interval 5 minuten<br>
**Tijdvenster:** 30 minuten<br>
**Waarschuwing frequentie:** 5 minuten<br>
**Cumulatieve waarde:** geweldige dan 90<br>
**Waarschuwing activeren op basis van:** totaal kiezen oplossingen groter is dan 5<br>

Hallo query zou een gemiddelde waarde voor elke computer maken om de 5 minuten.  Deze query worden uitgevoerd om de 5 minuten voor gegevens die zijn verzameld via Hallo vorige 30 minuten.  Voorbeeldgegevens worden hieronder weergegeven voor de drie computers.

![Voorbeeld-queryresultaten](media/log-analytics-alerts/metrics-measurement-sample-graph.png)

In dit voorbeeld zou er afzonderlijke waarschuwingen voor srv02 en srv03 worden gemaakt omdat ze Hallo 90% drempelwaarde 3 maal via Hallo tijdvenster geschonden.  Als hello **Trigger waarschuwing op basis van:** te zijn gewijzigd**opeenvolgend** en vervolgens een waarschuwing alleen voor srv03 zou worden gemaakt omdat het Hallo-drempelwaarde voor 3 opeenvolgende steekproeven geschonden.

## <a name="alert-records"></a>Waarschuwing records
Waarschuwing-records gemaakt door regels voor waarschuwingen in logboekanalyse hebben een **Type** van **waarschuwing** en een **SourceSystem** van **OMS**.  Ze hebben Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Type |*Een waarschuwing* |
| SourceSystem |*OMS* |
| *Object*  | [Metrische maateenheids waarschuwingen](#metric-measurement-alert-rules) heeft een eigenschap voor Hallo groepsveld.  Bijvoorbeeld, als Hallo logboek zoeken groepen op de Computer, hebben Hallo waarschuwing record met een veld van de Computer met de naam van de computer Hallo HALLO hallo-waarde.
| AlertName |Naam van het Hallo-waarschuwing. |
| AlertSeverity |Ernst van waarschuwing Hallo. |
| LinkToSearchResults |Koppeling tooLog Analytics logboek zoekquery waarmee Hallo records in de Hallo-query die Hallo waarschuwing gemaakt. |
| Query’s uitvoeren |Tekst van het Hallo-query die is uitgevoerd. |
| QueryExecutionEndTime |Einde van de Hallo tijdsbereik voor Hallo-query. |
| QueryExecutionStartTime |Begin van Hallo tijdsbereik voor Hallo-query. |
| ThresholdOperator | De operator die werd gebruikt door de waarschuwingsregel Hallo. |
| ThresholdValue | De waarde die is gebruikt door de waarschuwingsregel Hallo. |
| TimeGenerated |Datum en tijd Hallo waarschuwing is gemaakt. |

Er zijn andere soorten waarschuwing records gemaakt door Hallo [waarschuwing beheeroplossing](log-analytics-solution-alert-management.md) en door [Power BI exporteert](log-analytics-powerbi.md).  Deze alle hebben een **Type** van **waarschuwing** maar elkaar worden onderscheiden door hun **SourceSystem**.


## <a name="next-steps"></a>Volgende stappen
* Hallo installeren [waarschuwing beheeroplossing](log-analytics-solution-alert-management.md) tooanalyze waarschuwingen die zijn gemaakt in logboekanalyse samen met waarschuwingen van System Center Operations Manager worden verzameld.
* Lees meer over [Meld zoekopdrachten](log-analytics-log-searches.md) kunnen die waarschuwingen genereren.
* Een stapsgewijze Kennismaking voltooien [configureren van een webook](log-analytics-alerts-webhooks.md) met een waarschuwingsregel.  
* Meer informatie over hoe toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problemen geïdentificeerd met waarschuwingen.
