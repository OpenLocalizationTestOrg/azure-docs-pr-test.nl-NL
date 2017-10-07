---
title: aaaJob schaling mogelijk met Azure Stream Analytics & AzureML functies | Microsoft Docs
description: Meer informatie over hoe tooproperly schalen Stream Analytics-taken (partitioneren, SU hoeveelheid en meer) bij gebruik van Azure Machine Learning-functies.
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 47ce7c5e-1de1-41ca-9a26-b5ecce814743
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3fbdfaf7e8e86896c56f1d18bbde3a10bd3dca04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-stream-analytics-job-with-azure-machine-learning-functions"></a>Schalen van uw Stream Analytics-taak met Azure Machine Learning-functies
Het is vaak vrij eenvoudig tooset van een Stream Analytics-taak en voorbeeldgegevens doorlopen. Wat moet er doen als we toorun moeten dezelfde job met hogere gegevensvolume Hallo? Hiervoor moeten ons toounderstand hoe tooconfigure Hallo Stream Analytics taak zodat deze kunnen worden geschaald. In dit document gaan we in op Hallo bijzondere aspecten van vergroten/verkleinen Stream Analytics jobs met Machine Learning-functies. Voor informatie over hoe tooscale Stream Analytics-taken in het algemeen Hallo artikel zien [taken schalen](stream-analytics-scale-jobs.md).

## <a name="what-is-an-azure-machine-learning-function-in-stream-analytics"></a>Wat is een Azure Machine Learning-functie in Stream Analytics?
Een Machine Learning-functie in Stream Analytics kan worden gebruikt als een reguliere functieaanroep in Hallo querytaal van Stream Analytics. Hallo-functieaanroepen zijn echter achter Hallo-scènes daadwerkelijk Azure Machine Learning-webservice-aanvragen. Machine Learning-webservices ondersteuning 'batchverwerking' meerdere rijen die Mini batch wordt genoemd, en in Hallo dezelfde service API-aanroep tooimprove totale doorvoer. Zie de volgende artikelen voor meer informatie; Hallo [Azure Machine Learning-functies in Stream Analytics](https://blogs.technet.microsoft.com/machinelearning/2015/12/10/azure-ml-now-available-as-a-function-in-azure-stream-analytics/) en [Azure Machine Learning-webservices](../machine-learning/machine-learning-consume-web-services.md).

## <a name="configure-a-stream-analytics-job-with-machine-learning-functions"></a>Configureren van een Stream Analytics-taak met Machine Learning-functies
Bij het configureren van een Machine Learning-functie voor Stream Analytics-taak, zijn er twee parameters tooconsider, batchgrootte Hallo van Machine Learning-functieaanroepen Hallo en Hallo streaming-eenheden (SUs) ingericht voor Hallo Stream Analytics-taak. toodetermine hello juiste waarden voor deze, eerst een beslissing moet worden gemaakt tussen latentie en doorvoer, dat wil zeggen, latentie van Hallo Stream Analytics-taak en de doorvoer van elke SU. SUs kunnen altijd worden toegevoegd tooa taak tooincrease doorvoer van een goed gepartitioneerde Stream Analytics query, hoewel aanvullende SUs verhoogt Hallo kosten van het actieve Hallo-taak.

Daarom is het belangrijk toodetermine hello *tolerantie* van latentie in een Stream Analytics-taak wordt uitgevoerd. Extra latentie Azure Machine Learning-serviceaanvragen worden uitgevoerd verhoogd met de batchgrootte, die wordt samengesteld Hallo latentie van de Stream Analytics-taak Hallo natuurlijk. Hallo daarentegen vergroten met de batch kan Hallo Stream Analytics-taak tooprocess * meer gebeurtenissen met de Hallo *hetzelfde nummer* van Machine Learning web serviceaanvragen. Vaak Hallo toename van Machine Learning web service latentie is toohello subplan lineaire toename van batchgrootte dus is het belangrijk tooconsider Hallo meest voordelige batch-grootte voor een Machine Learning-webservice in een situatie met opgegeven. Hallo standaardbatchgrootte voor Hallo-webservice-aanvragen is 1000 en kunnen worden gewijzigd met behulp van Hallo [Stream Analytics REST-API](https://msdn.microsoft.com/library/mt653706.aspx "Stream Analytics REST-API") of Hallo [PowerShell-client voor Stream Analytics](stream-analytics-monitor-and-manage-jobs-use-powershell.md "PowerShell-client voor Stream Analytics").

Zodra een batchgrootte is bepaald, Hallo hoeveelheid streaming-eenheden (SUs) kunnen worden bepaald, gebaseerd op Hallo aantal gebeurtenissen dat Hallo-functie tooprocess per seconde moet. Zie voor meer informatie over het streaming-eenheden, [Stream Analytics taken schalen](stream-analytics-scale-jobs.md).

In het algemeen zijn zijn er 20 gelijktijdige verbindingen toohello Machine Learning-webservice voor elke 6 SUs, behalve dat 1 SU-taken en 3 SU taken 20 gelijktijdige verbindingen ook krijgen.  Als Hallo invoergegevens snelheid 200.000 gebeurtenissen per seconde en Hallo batchgrootte blijft is standaard toohello van 1000 Hallo resulterende web service latentie met 1000 gebeurtenissen Mini batch interval van 200. Dit betekent dat elke verbinding kan maken 5 aanvragen toohello Machine Learning-webservice in een tweede. Bij 20 verbindingen verwerken Hallo Stream Analytics-taak 20.000 gebeurtenissen in een interval van 200 en daarom 100.000 gebeurtenissen gedurende een seconde. Dus tooprocess 200.000 gebeurtenissen per seconde, Hallo Stream Analytics-taak moet 40 gelijktijdige verbindingen, die afkomstig uit too12 SUs is. Hallo-diagram hieronder ziet u Hallo aanvragen van Hallo Stream Analytics-taak toohello Machine Learning web service-eindpunt: elke 6 SUs heeft 20 gelijktijdige verbindingen tooMachine Learning-webservice op max.

![Stream Analytics schalen met Machine Learning functies 2 taak voorbeeld](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-00.png "Scale Stream Analytics met Machine Learning functies 2 taak voorbeeld")

In het algemeen ***B*** voor batchgrootte, ***L*** voor Hallo web service latentieperiode batchgrootte B in milliseconden, Hallo doorvoer van een Stream Analytics-taak met ***N*** SUs is:

![Stream Analytics met Machine Learning functies formule schalen](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-02.png "Stream Analytics met Machine Learning functies formule schalen")

Een extra aandacht mogelijk Hallo 'maximumaantal gelijktijdige aanroepen' op Hallo Machine Learning web service aan clientzijde, verdient het aanbeveling tooset deze toohello maximumwaarde (momenteel 200).

Raadpleeg voor meer informatie over deze instelling Hallo [voor Machine Learning-webservices schalen artikel](../machine-learning/machine-learning-scaling-webservice.md).

## <a name="example--sentiment-analysis"></a>Voorbeeld: gevoel analyse
Hallo volgende voorbeeld bevat een Stream Analytics-taak met de Hallo gevoel analysis Machine Learning-functie, zoals beschreven in Hallo [Stream Analytics, Machine Learning-integratie zelfstudie](stream-analytics-machine-learning-integration-tutorial.md).

Hallo-query is een eenvoudige volledig gepartitioneerde query gevolgd door Hallo **gevoel** functioneren, zoals hieronder wordt weergegeven:

    WITH subquery AS (
        SELECT text, sentiment(text) as result from input
    )

    Select text, result.[Score]
    Into output
    From subquery

Houd rekening met Hallo volgen scenario; met een doorvoersnelheid van 10.000 tweets per seconde moet een Stream Analytics-taak tooperform gevoel analyse van Hallo tweets (gebeurtenissen) worden gemaakt. 1 SU gebruikt, kan deze Stream Analytics-taak worden kunnen toohandle Hallo verkeer? Met Hallo standaardbatchgrootte van 1000 Hallo taak moet kunnen tookeep up met Hallo-invoer. Verdere Hallo toegevoegd aan Machine Learning-functie niet meer dan een seconde van latentie, namelijk Hallo algemeen standaard latentie van Hallo gevoel analyse Machine Learning-webservice (met een standaardbatchgrootte 1000) moet worden gegenereerd. Hallo Stream Analytics-taak van **algehele** of latentie end-to-end doorgaans een paar seconden. Meer gedetailleerde verdiepen in deze Stream Analytics-taak *vooral* Hallo Machine Learning-functieaanroepen. Hallo batchgrootte 1000 hebben, duurt een doorvoer van 10.000 gebeurtenissen ongeveer 10 aanvragen tooweb service. Zelfs met 1 SU, er zijn onvoldoende tooaccommodate gelijktijdige verbindingen dit verkeer invoer.

Wat gebeurt er als Hallo invoergebeurtenis tarief wordt verhoogd door 100 x maar Hallo Stream Analytics-taak moet nu tooprocess 1.000.000 tweets per seconde? Er zijn twee opties:

1. Batchgrootte hello, verhogen of
2. Partitie Hallo invoerstroom tooprocess Hallo gebeurtenissen parallel

Met de eerste optie Hallo Hallo taak **latentie** wordt verhoogd.

Met de tweede optie hello, zou meer SUs moet toobe ingericht en daarom genereren meer gelijktijdige aanvragen van Machine Learning web service. Dit betekent dat de taak Hallo **kosten** wordt verhoogd.

Wordt ervan uitgegaan dat Hallo latentie van Hallo gevoel analysis Machine Learning-webservice is interval van 200 voor batches van 1000 gebeurtenissen of hieronder 250ms voor 5.000 gebeurtenis batches, 300ms voor batches van 10.000 gebeurtenissen of 500ms voor batches 25.000-gebeurtenis.

1. Met behulp van de eerste optie hello (**niet** meer SUs inrichting), batchgrootte hello te kan worden verhoogd**25.000**. Op zijn beurt Hierdoor kan Hallo taak tooprocess 1.000.000 gebeurtenissen met 20 gelijktijdige verbindingen toohello Machine Learning-webservice (met een latentie van 500ms per aanroep). Dus Hallo extra latentie van de Stream Analytics-taak Hallo vanwege toohello gevoel functie aanvragen op basis van Machine Learning webserviceaanvragen zou worden verhoogd van Hallo **interval van 200** te**500ms**. Bedenk wel dat batchgrootte **kan niet** oneindig worden verhoogd als hello Machine Learning-webservices vereist Hallo nettolading grootte van een aanvraag worden 4 MB of kleiner web service aanvragen time-out na 100 seconden van bewerking.
2. Met behulp van de tweede optie Hallo Hallo batchgrootte is links op 1000, met een interval van 200 web service latentie, elke webservice van 20 gelijktijdige verbindingen toohello zou kunnen tooprocess 1000 * 20 * 5 gebeurtenissen = 100.000 per seconde. Tooprocess 1.000.000 gebeurtenissen per seconde, Hallo-taak moet dus 60 SUs. Vergeleken toohello eerste optie, Stream Analytics-taak zouden meer op zijn beurt web service batchaanvragen, het genereren van een extra kosten.

Hieronder vindt u een tabel voor Hallo doorvoer van Hallo Stream Analytics-taak voor verschillende SUs en batch grootte (in het aantal gebeurtenissen per seconde).

| Batchgrootte (ML latentie) | 500 (interval van 200) | 1000 (interval van 200) | 5.000 (250ms) | 10.000 (300ms) | 25.000 (500ms) |
| --- | --- | --- | --- | --- | --- |
| **1 SU** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **SUs 3** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **6 SUs** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **SUs 12** |5,000 |10.000 |40,000 |60,000 |100,000 |
| **18 SUs** |7,500 |15,000 |60,000 |90,000 |150,000 |
| **24 SUs** |10.000 |20,000 |80,000 |120,000 |200.000 |
| **…** |… |… |… |… |… |
| **60 SUs** |25,000 |50,000 |200.000 |300,000 |500,000 |

Nu moet u al een goed begrip van de werking van Machine Learning-functies in Stream Analytics hebben. U waarschijnlijk begrijpen ook dat de Stream Analytics-taken 'pull' gegevens van gegevensbronnen en elke 'pull' retourneert een reeks gebeurtenissen voor Stream Analytics-taak tooprocess Hallo. Hoe beïnvloedt dit pullmodel Hallo Machine Learning web serviceaanvragen

Hallo batchgrootte die we ingesteld voor Machine Learning-functies niet normaal gesproken exact worden gedeeld door het aantal gebeurtenissen dat is geretourneerd door elke Stream Analytics-taak 'pull' Hallo. Dit gebeurt wanneer Hallo Machine Learning-webservice wordt aangeroepen met 'gedeeltelijke' batches. Dit wordt gedaan toonot extra taak latentie overhead in samenvoegen gebeurtenissen van pull-toopull rekening worden gebracht.

## <a name="new-function-related-monitoring-metrics"></a>Nieuwe functie-gerelateerde bewaking metrische gegevens
In het gebied van de Monitor van een Stream Analytics-taak hello, zijn drie extra functie-gerelateerde statistieken toegevoegd. Dit zijn de aanvragen van functie, gebeurtenissen voor de functie en MISLUKTE functie aanvragen, zoals wordt weergegeven in onderstaande afbeelding voor Hallo.

![Stream Analytics met Machine Learning functies metrische gegevens schalen](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-01.png "schalen Stream Analytics met Machine Learning functies metrische gegevens")

Hallo zijn als volgt gedefinieerd:

**AANVRAGEN van functie**: het aantal aanvragen van functie Hallo.

**GEBEURTENISSEN voor de functie**: Hallo aantal gebeurtenissen in Hallo werken aanvragen.

**MISLUKTE aanvragen voor de functie**: Hallo aantal mislukte functie aanvragen.

## <a name="key-takeaways"></a>Sleutel Takeaways
toosummarize hello belangrijkste punten in de volgorde tooscale een Stream Analytics-taak met Machine Learning-functies, hello volgende items moeten worden beschouwd:

1. snelheid van de invoer gebeurtenissen Hallo
2. Hallo verdragen latentie voor Hallo Stream Analytics-taak uitgevoerd (en dus batchgrootte Hallo van Hallo Machine Learning-webservice-aanvragen)
3. Hallo ingericht Stream Analytics SUs en Hallo aantal Machine Learning web service-aanvragen (Hallo aanvullende functie-gerelateerde kosten)

Een voorbeeld is een volledig gepartitioneerde Stream Analytics query gebruikt. Wanneer u een complexere query nodig hebt Hallo [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) is een zeer waardevolle resource voor aanvullende hulp vragen aan Hallo Stream Analytics-team.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Stream Analytics, Zie:

* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)
