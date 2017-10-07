---
title: AAA steekproeven invoer in Azure Stream Analytics | Microsoft Docs
description: Speldenpunt problemen bij het oplossen van Stream Analytics-taken.
keywords: invoer, invoer steekproeven oplossen
documentationcenter: 
services: stream-analytics
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
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a>Azure Stream Analytics invoer-stream steekproeven

U kunt steekproef nemen invoer gebeurtenissen die afkomstig zijn van een bestand en het testen van query's in Hallo portal zonder toostart of stoppen van een taak met behulp van Azure Stream Analytics.

## <a name="testing-your-query"></a>Uw query testen

Open in Hallo Stream Analytics-taak detailvenster Hallo **Query-editor** blade door te klikken op de querynaam Hallo onder **Query**. (In ons voorbeeldscenario omdat nog geen query is gemaakt, klikt u op Hallo **combinatie** tijdelijke aanduiding.)

![Hallo Stream Analytics query-editor](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

Net als in de vorige release Hallo Hallo uitgebreide editor blade voor het maken van uw query weergegeven. Nu Hallo blade is bijgewerkt met een nieuwe linkerdeelvenster die toont Hallo in- en uitgangen die worden gebruikt door query Hallo en gedefinieerd voor deze taak.

![Hallo Stream Analytics query-editor invoer en uitvoer van lijsten](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

Ook wordt weergegeven, zijn een extra invoer en uitvoer, die niet zijn gedefinieerd. Ze afkomstig zijn van het nieuwe querysjabloon hello, beginnend met. Ze te wijzigen of zelfs verdwijnen helemaal, zoals u Hallo query bewerken. U kunt deze gewoon negeren nu.

tootest met voorbeeldgegevens voor invoer met de rechtermuisknop op een van uw invoer en selecteer vervolgens **voorbeeldgegevens uit bestand uploaden**.

![Hallo Stream Analytics query-editor uploaden voorbeeldgegevens uit bestandsopdracht](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

Nadat het Hallo uploaden is voltooid, klikt u op **Test** tootest deze query op Hallo voorbeeldgegevens u zojuist hebt opgegeven.

![knop voor Hallo Stream Analytics query-editor testen](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

Als u toosave hello testuitvoer voor later gebruik wilt, worden Hallo resultaten van de query wordt weergegeven in Hallo browser met een koppeling toohello downloadresultaten. U kunt nu eenvoudig en iteratief pas uw query en testen herhaaldelijk toosee hoe Hallo uitvoer verandert.

![Voorbeelduitvoer van stream Analytics query-editor](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

In de Hallo voorafgaand aan de installatiekopie, is een tweede uitvoer toegevoegd, aangeroepen **HighAvgTempOutput**.

Wanneer u meerdere uitgangen in een query gebruikt, kunt u zien Hallo resultaten voor elke uitvoer afzonderlijk en schakelen tussen deze twee.

Nadat u tevreden met Hallo resultaten bent, kunt u uw query opslaan, uw taak starten, terug zitten en bekijkt hello magie van Stream Analytics.

## <a name="get-help"></a>Help opvragen

Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)
