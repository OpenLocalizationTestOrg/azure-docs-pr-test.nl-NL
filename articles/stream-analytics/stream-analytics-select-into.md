---
title: aaaDebug Azure Stream Analytics query's met behulp van SELECT INTO | Microsoft Docs
description: Gegevens halverwege voorbeeldquery met behulp van een instructie SELECT INTO in Stream Analytics
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a>Fouten opsporen in query's met behulp van een instructie SELECT INTO

In realtime-gegevensverwerking weten welke gegevens Hallo lijkt erop dat in het midden van Hallo Hallo query handig kan zijn. Omdat de invoer- of stappen van een Azure Stream Analytics-taak kunnen meerdere keren worden gelezen, kunt u extra SELECT INTO-instructies schrijven. In dat geval voert tussenliggende gegevens naar de opslag en kunt u controleren Hallo juistheid van Hallo gegevens, net zoals *bekijken variabelen* doen wanneer u een programma foutopsporing.

## <a name="use-select-into-toocheck-hello-data-stream"></a>SELECT INTO toocheck Hallo gegevensstroom gebruiken

Hallo heeft volgende voorbeeldquery in een Azure Stream Analytics-taak een Stroominvoer, twee verwijzing gegevens invoeren en een uitvoer-tooAzure Table Storage. Hallo query lid wordt van gegevens van Hallo event hub en twee referentie blobs tooget Hallo naam en categorie-informatie:

![Voorbeeld van de SELECT INTO-query](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

Houd er rekening mee dat Hallo-taak wordt uitgevoerd, maar er zijn geen gebeurtenissen zijn in Hallo uitvoer wordt geproduceerd. Op Hallo **bewaking** tegel, die hier worden weergegeven, kunt u zien dat Hallo-invoer is het opstellen van gegevens, maar u niet welke stap van Hallo weet **JOIN** veroorzaakt alle Hallo gebeurtenissen toobe verwijderd.

![Hallo bewaking tegel](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
In dit geval kunt u een paar extra SELECT INTO-instructies te 'melden' hello tussenliggende JOIN-resultaten en Hallo gegevens dat gelezen uit Hallo invoer toevoegen.

In dit voorbeeld toegevoegd twee nieuwe 'tijdelijke uitvoer." Ze kunnen worden alle gewenste sink. We gebruiken hier Azure Storage als een voorbeeld:

![Toevoegen van extra SELECT INTO-instructies](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

U kunt vervolgens herschrijven Hallo query als volgt:

![Herschreven SELECT INTO-query](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

Nu Hallo taak opnieuw starten en laten uitvoeren voor een paar minuten. Vervolgens query temp1 en Tijdelijk2 met Visual Studio Cloud Explorer tooproduce Hallo tabellen te volgen:

**tabel temp1**
![SELECT INTO temp1 tabel](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**tabel Tijdelijk2**
![SELECT INTO Tijdelijk2 tabel](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

Zoals u ziet, temp1 en Tijdelijk2 gegevens hebt en Hallo naamkolom correct in Tijdelijk2 is ingevuld. Echter, omdat er nog geen gegevens in de uitvoer, er is iets mis:

![SELECT INTO output1 tabel zonder gegevens](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

Door middel van steekproeven Hallo gegevens, kunt u zijn bijna zeker weet dat Hallo probleem met de Hallo is tweede JOIN. U kunt downloaden van Hallo referentiegegevens van Hallo-blob en te bekijken:

![SELECT INTO ref-tabel](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

Zoals u ziet, wijkt Hallo-indeling van GUID Hallo in deze referentiegegevens af van Hallo-indeling van Hallo [uit]-kolom in Tijdelijk2. Daarom is Hallo gegevens niet aangekomen in output1 zoals verwacht.

U kunt oplossen gegevensindeling hello, tooreference blob te uploaden en probeer het opnieuw:

![SELECT INTO tijdelijke tabel](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

Deze tijd wordt Hallo-gegevens in de uitvoer van de Hallo geformatteerd en ingevuld zoals verwacht.

![Selecteer in de laatste tabel](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>Help opvragen

Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen

* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

