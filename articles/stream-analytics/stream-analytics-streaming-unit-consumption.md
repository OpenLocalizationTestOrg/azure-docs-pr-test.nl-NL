---
title: "Azure Stream Analytics: Uw taak toouse Streaming-eenheden efficiënt optimaliseren | Microsoft Docs"
description: Aanbevolen procedures voor schaalbaarheid en prestaties in Azure Stream Analytics query.
keywords: Streaming-eenheid, de prestaties van query 's
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a>Efficiënt optimaliseren van uw taak toouse Streaming-eenheden

Azure Stream Analytics aggregeert Hallo prestaties 'gewicht' van een taak die worden uitgevoerd in de Streaming-eenheden (SUs). SUs vertegenwoordigen Hallo computerbronnen die verbruikte tooexecute een taak. SUs bieden een manier toodescribe Hallo relatieve gebeurtenisverwerking capaciteit op basis van een gecombineerde meting van CPU, geheugen, en lezen en schrijven tarieven. Met deze capaciteit kunt u zich richten op Hallo query logica en verwijdert u uit prestatieoverwegingen voor tooknow storage-laag, hoeven handmatig geheugen toewijzen voor uw werk en Hallo CPU core-aantal nodig toorun van uw werk tijdig benaderen.

## <a name="how-many-sus-are-required-for-a-job"></a>Hoeveel SUs zijn vereist voor een taak?

Aantal vereiste SUs voor een bepaalde taak Hallo kiezen, is afhankelijk van Hallo partitieconfiguratie voor Hallo invoer en Hallo-query die gedefinieerd binnen het Hallo-taak. Hallo **Scale** blade kunt u tooset Hallo rechts aantal SUs. Het is een best practices tooallocate meer SUs dan nodig. Hallo-verwerkingsengine Stream Analytics geoptimaliseerd voor latentie en doorvoer op Hallo kosten voor het toewijzen van extra geheugen.

Hallo aanbevolen procedure is over het algemeen toostart met 6 SUs voor query's die geen gebruikmaken van *PARTITION BY*. Vervolgens Hallo sweet positie vast door een vallen en opstaan methode waarin u het aantal SUs Hallo wijzigen nadat u representatieve hoeveelheden gegevens doorgeven en hello SU % gebruik metrische gegevens bekijkt.

Azure Stream Analytics houdt gebeurtenissen in een venster Hallo 'opnieuw ordenen buffer' aangeroepen voordat er begonnen wordt met de verwerking. Gebeurtenissen binnen Hallo bestellen venster zijn gesorteerd op basis van tijd en verdere bewerkingen worden uitgevoerd op Hallo ondersteuningsbeheerder gesorteerd gebeurtenissen. Volgorde van gebeurtenissen door de tijd, zorgt u ervoor dat Hallo-operator heeft inzicht in alle gebeurtenissen in Hallo Hallo bepaald tijdsbestek. U kunt hiermee ook Hallo operator Hallo vereiste bewerkingen uitvoeren en uitvoer te produceren. Een neveneffect van deze methode is dat verwerking door de duur Hallo van Hallo bestellen venster wordt vertraagd. Hallo geheugengebruik van Hallo taak (die van invloed op een SU verbruik) is een functie van Hallo grootte van deze opnieuw ordenen venster en Hallo aantal gebeurtenissen die hierin zijn opgenomen.

> [!NOTE]
> Wanneer het aantal lezers Hallo tijdens upgrades van de taak wordt gewijzigd, worden waarschuwingen voor tijdelijke tooaudit Logboeken geschreven. Stream Analytics-taken worden automatisch herstellen van deze problemen van voorbijgaande aard.

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a>Algemene high memory oorzaken voor gebruik van hoge SU voor het uitvoeren van taken

### <a name="high-cardinality-for-group-by"></a>Hoge kardinaliteit voor GROEPEREN op

Hallo kardinaliteit van binnenkomende gebeurtenissen bepaalt geheugengebruik voor Hallo taak.

Bijvoorbeeld in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, dat is gekoppeld aan Hallo **geclusterde** Hallo kardinaliteit van Hallo-query is.

Hallo query toomitigate problemen die worden veroorzaakt door hoge kardinaliteit uitbreiden door te verhogen met partities **PARTITION BY**.

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

aantal Hallo *geclusterde* Hallo kardinaliteit van GROUP BY hier is.

Nadat het Hallo-query is gepartitioneerd, wordt deze zich verdeeld over meerdere knooppunten. Als gevolg hiervan Hallo aantal gebeurtenissen die afkomstig zijn in elk knooppunt verminderd die op zijn beurt verkleint Hallo Hallo bestellen buffer. U moet ook de event hub partities partitioneren door partitionid.

### <a name="high-unmatched-event-count-for-join"></a>Aantal hoge niet-overeenkomende gebeurtenissen voor de JOIN

Hallo aantal niet-overeenkomende gebeurtenissen in een JOIN is van invloed op Hallo geheugengebruik van Hallo-query. Neem bijvoorbeeld een query die toofind Hallo aantal ad hits die klikken genereert is op zoek:

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

In dit scenario is het mogelijk dat veel advertenties worden weergegeven en enkele muisklikken worden gegenereerd. Dergelijke resultaat moet alle Hallo gebeurtenissen binnen tijdvenster Hallo Hallo taak tookeep. Hallo hoeveelheid gebruikt geheugen is evenredig toohello venster grootte en gebeurtenis-snelheid. 

toomitigate partities van deze situatie scale-out Hallo query door te verhogen met behulp van PARTITION BY. 

Nadat het Hallo-query is gepartitioneerd, wordt deze zich verdeeld over meerdere knooppunten van de verwerking. Als gevolg hiervan Hallo aantal gebeurtenissen die afkomstig zijn in elk knooppunt verminderd die op zijn beurt verkleint Hallo Hallo bestellen buffer.

### <a name="large-number-of-out-of-order-events"></a>Groot aantal gebeurtenissen in andere volgorde 

Een groot aantal gebeurtenissen in andere volgorde binnen een grote tijdvenster zorgt ervoor dat Hallo grootte van Hallo 'rangschikken buffer' toobe groter. toomitigate partities van deze situatie scale Hallo query door te verhogen met behulp van PARTITION BY. Nadat het Hallo-query is gepartitioneerd, wordt deze zich verdeeld over meerdere knooppunten. Als gevolg hiervan Hallo aantal gebeurtenissen die afkomstig zijn in elk knooppunt verminderd die op zijn beurt verkleint Hallo Hallo bestellen buffer. 


## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Naslaginformatie over Azure Stream Analytics Management REST-API](https://msdn.microsoft.com/library/azure/dn835031.aspx)
