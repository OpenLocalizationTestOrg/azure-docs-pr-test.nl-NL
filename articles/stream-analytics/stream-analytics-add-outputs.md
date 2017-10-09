---
title: aaaHow tooconfigure gegevens levert voor Stream Analytics-taken | Microsoft Docs
description: Uitvoer voor Stream Analytics-taken configureren | leren padsegment.
keywords: gegevens uitvoer verplaatsing van gegevens
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a>Hoe tooconfigure gegevens levert voor Stream Analytics-taken

Azure Stream Analytics-taken zijn verbonden tooone of meer gegevens uitvoer, die een verbinding tooan bestaande gegevens sink definiëren. Als uw Stream Analytics-taak verwerkt en binnenkomende gegevens transformeert, is een stream met gegevens uitvoergebeurtenissen tooyour taakuitvoer geschreven.

Stream Analytics gegevens uitvoer kunnen worden gebruikt toosource realtime-dashboards of waarschuwingen, trigger data movement werkstromen of gewoon gegevens archiveren voor batch-verwerking later op. Stream Analytics heeft eerste-klas integratie met verschillende Azure-services, die in details hier worden beschreven.

de Stream Analytics-taak van een uitvoer-tooyour tooadd:

1. In Hallo [Azure-portal](https://portal.azure.com), opent u de taak en klikt u op **uitvoer** en klik vervolgens op **toevoegen** Hallo uitvoer blade die wordt weergegeven.
   
    ![Uitvoer toevoegen](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. Geef een beschrijvende naam voor deze uitvoer in Hallo **Uitvoeraliassen** vak. Deze naam kan worden gebruikt in uw job query later op toorefer toohello uitvoer.  
   
    Vul de overige Hallo van Hallo vereist verbinding eigenschappen tooconnect tooyour uitvoer.  Deze velden is afhankelijk van het uitvoertype en hier worden gedefinieerd.  
   
    ![Gegevenstype verplaatsing kiezen](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. Afhankelijk van het type uitvoer Hallo moet u mogelijk toospecify hoe Hallo gegevens is geserialiseerd of geformatteerd. Hallo serialisatie specifieke instellingen voor elk uitvoertype worden hier beschreven.
   
    Vul de overige Hallo van Hallo vereiste verbinding eigenschappen tooconnect tooyour-gegevensbron. Deze velden verschillen per type van het type invoer- en bron en worden gedefinieerd in detail in Hallo [taak maken artikel](stream-analytics-create-a-job.md).  

> [!Note]
>
> Elke uitvoer element toegevoegde toohello-taak moet bestaan voordat Hallo-taak is gestart en gebeurtenissen start stromende. Bijvoorbeeld, als u een Blob-opslag als uitvoer gebruikt, maakt Hallo-taak niet een opslagaccount automatisch. Het moet toobe gemaakt door gebruiker Hallo voordat Hallo ASA-taak is gestart.
> 
 

## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

