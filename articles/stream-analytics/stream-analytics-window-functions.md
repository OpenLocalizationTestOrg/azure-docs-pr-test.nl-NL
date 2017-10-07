---
title: aaaIntroduction tooStream Analytics-vensterfuncties | Microsoft Docs
description: Meer informatie over drie vensterfuncties Hallo in Stream Analytics (tumbling, hopping, Verschuivend).
keywords: venster Verschuivend venster venster hopping tumbling
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a>Inleiding tooStream Analytics-vensterfuncties
In veel realtime streaming-scenario's, is het nodig tooperform bewerkingen alleen op de gegevens in de tijdelijke windows hello. Systeemeigen ondersteuning voor windowing functies is een belangrijke functie van Azure Stream Analytics die Hallo naald op de productiviteit van ontwikkelaars verplaatst in complexe stroom verwerking taken ontwerpen. Stream Analytics biedt ontwikkelaars toouse [ **Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) en [ **schuifregelaar** ](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform tijdelijke bewerkingen op het streamen van gegevens. Hierbij moet worden opgemerkt dat alle [venster](https://msdn.microsoft.com/library/dn835019.aspx) operations uitvoerresultaten op Hallo **end** van Hallo-venster. Hallo-uitvoer van Hallo-venster worden één gebeurtenis op basis van Hallo statistische functie gebruikt. Hallo-gebeurtenis heeft Hallo tijdstempel van Hallo einde van Hallo-venster en alle functies van het venster met een vaste lengte zijn gedefinieerd. Ten slotte het is belangrijk toonote die alle functies van het venster moeten worden gebruikt in een [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) component.

![Stream Analytics venster werkt concepten](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a>Tumblingvenster
Daling vensterfuncties gebruikte toosegment zijn een gegevensstroom in segmenten van verschillende tijd en uitvoeren van een functie hiertegen, zoals Hallo in het volgende voorbeeld. de belangrijkste differentiators Hallo van een tumblingvenster zijn dat ze herhalen, elkaar niet overlappen en een gebeurtenis kan niet toomore dan één tumblingvenster behoren.

![Stream Analytics-vensterfuncties tumbling intro](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a>Hoppingvenster
Hopping venster functies hop doorsturen door een vaste periode. Eenvoudig toothink hiervan als daling vensters die elkaar overlappen kunnen, kan het zijn zodat gebeurtenissen deel van toomore dan Hopping venster resultaat ingesteld uitmaken kunnen. toomake een venster Hopping Hallo dezelfde als een tumblingvenster geeft een eenvoudig hello hop grootte toobe Hallo dezelfde als Hallo venstergrootte. 

![Stream Analytics-vensterfuncties hopping intro](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a>Sliding Window
Verschuivende vensterfuncties, in tegenstelling tot Tumbling of windows, Hopping produceren uitvoer **alleen** wanneer een gebeurtenis zich voordoet. Elk venster zijn ten minste één gebeurtenis en Hallo venster continu verplaatst doorsturen door een € (epsilon). Net als Windows Hopping kunnen gebeurtenissen toomore dan één venster Verschuivend behoren.

![Stream Analytics-vensterfuncties Verschuivend intro](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a>Help opvragen bij vensterfuncties
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

