---
title: aaaHow toowrite query's in de Stream Analytics | Microsoft Docs
description: Query's in de Stream Analytics en querygegevens schrijven | leren padsegment.
keywords: hoe toowrite query's gegevens opvragen, een query schrijven van query's schrijven
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a>Hoe toowrite in Stream Analytics query 's
Schrijven van query's voor stroomverwerkingslogica schrijft in Azure Stream Analytics wordt geïmplementeerd als een 'permanente query' die is gedefinieerd voordat een taak wordt gestart en wordt uitgevoerd op gegevens, zoals het Hallo-taak is bereikt. Hallo gegevenstransformatie wordt uitgedrukt in een SQL-achtige query-taal, die is grotendeels een subset van T-SQL met enkele taal extensies als toegevoegd [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) tooexpress tijdelijke semantiek gebruikt.

## <a name="writing-queries"></a>Schrijven van query's:
1. Klik in de Stream Analytics-taak in hello Azure-beheerportal op **Query**.
   
    ![Query selecteren](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    In Azure Portal hello, klikt u op **Query**.
   
    ![Selecteer de Query-Preview](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. Nieuwe taken hebben een query sjabloon toohelp u op weg. Hallo query sjabloon 'doorgangsschijf' voert query dat projecten alle velden uit de invoervelden in Hallo uitvoer.  
   
   * Als u ten minste één invoer en uitvoer voor uw taak hebt gedefinieerd, kunt u Hallo tijdelijke aanduiding '[YourOutputAlias]' en '[YourInputAlias]' velden vervangen door Hallo aliassen Hallo invoer en uitvoer dat u wenst dat gebruik eerst. U kunt bovendien nog steeds ontwerpen en testen van uw query in de klassieke Azure-Portal Hallo zonder te definiëren in- en uitgangen op Hallo-taak.
   * Als u tooperform meer dan een eenvoudige pass-through-verwerking wenst, kunt u de querydefinitie Hallo kunt bewerken. tooget gestart met het ontwerpen van query verdiepen in enkele algemene query patronen worden vastgelegd [hier](stream-analytics-stream-analytics-query-patterns.md).  
   
   ![Querygegevens venster](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a>querygegevens toovalidate werkt:
U kunt testen dat uw query werkt zoals verwacht in de browser Hallo worden uitgevoerd via een of meer lokale JSON-bestanden met testgegevens. Dit wordt niet Hallo taak starten of hebben invloed op de facturering.

> [!NOTE]
> Testen van query's in de browser is momenteel niet ondersteund in hello Azure-Portal.  
> 
> 

1. Zorg ervoor dat er geen fouten zijn opgetreden in Hallo-query (anders de knop testen hello wordt uitgeschakeld) en klik vervolgens op de knop testen Hallo.  
   
   ![Querygegevens Test](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. U zult na vragen aan gebruiker toospecify bestanden voor elk waarnaar wordt verwezen in de query Hallo Hallo-invoer. In dit voorbeeld Hallo sjabloon query wordt gehandhaafd-is, dus Hallo dialoogvenster gevraagd om voor invoer met de naam 'yourinputalias'.  
   
   ![De query gegevens testen](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. Blader tooa testbestand. Verschillende voorbeeldbestanden zijn beschikbaar op [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) en u kunt ook voorbeeldgegevens ophalen uit de invoer van uw eigen gegevens stream via Hallo voorbeeldgegevens-functie op Hallo invoer tabblad.  
   
   ![Invoer voor de query](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. Na het Hallo-dialoogvenster te sluiten, uw query wilt uitvoeren via de testgegevens Hallo en Hallo resultaten onderaan Hallo Hallo querypagina worden weergegeven.  
   
   ![Samenvatting van de query](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

