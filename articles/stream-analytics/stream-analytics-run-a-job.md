---
title: aaaHow toostart streaming-taken in de Stream Analytics | Microsoft Docs
description: Hoe een streaming-taak uitgevoerd in Azure Stream Analytics | leren padsegment.
keywords: Streaming-taken
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a>Hoe toorun een streaming-taak in Azure Stream Analytics
Wanneer een taak invoer, query's en uitvoer, zijn alle opgegeven dat kunt u Hallo Stream Analytics-taak starten.

toostart uw taak:

1. Klik in de klassieke Azure-portal Hallo van Hallo taak dashboard op **Start** Hallo Hallo pagina onderaan in.
   
   ![Taak knop starten](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   Klik in hello Azure-portal, op **Start** Hallo boven aan de pagina van de taak.
   
   ![Azure portal starttaak knop](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. Geef een **Start uitvoer** waarde toodetermine wanneer deze taak zal starten uitvoer te produceren. Hallo standaardinstelling voor taken die eerder niet is gestart is **begintijd taak**, wat betekent dat deze taak Hallo begint onmiddellijk verwerken van gegevens. U kunt ook opgeven een **aangepaste** tijd in Hallo in het verleden (voor het gebruiken van historische gegevens) of Hallo toekomstige (toodelay verwerken tot een toekomstig tijdstip). Voor gevallen wanneer een taak is eerder gestart en gestopt, optie Hallo **laatste tijd geëindigd** is beschikbaar in de volgorde tooresume Hallo taak in de tijd van laatste uitvoer Hallo en voorkomen dat gegevens verloren gaan.  
   
   ![Streaming-taak tijd starten](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure portal Start streaming-taak tijd](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. Bevestig uw selectie. Hallo taakstatus verandert te*starten* en zal spoedig te verplaatsen*met* eenmaal Hallo-taak is gestart. U kunt Hallo voortgang Hallo **Start** Hallo-bewerking **Notification Hub**:
   
   ![Streaming-taak uitgevoerd](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Azure-portal streaming-taak uitgevoerd](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

