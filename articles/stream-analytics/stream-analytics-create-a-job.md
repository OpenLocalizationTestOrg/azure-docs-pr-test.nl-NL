---
title: aaaHow toocreate een taak analytics verwerking voor Stream Analytics | Microsoft Docs
description: Maken van een taak analytics verwerking voor Stream Analytics | leren padsegment.
keywords: gegevensverwerking analytics
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a>Hoe toocreate een analytics gegevensverwerking taak voor Stream Analytics
Hallo op het hoogste niveau resource in Azure Stream Analytics is een Stream Analytics-taak.  Deze bestaat uit een of meer gegevensbronnen, een query uitdrukken Hallo gegevenstransformatie en een of meer uitvoer-doelen die resultaten zijn geschreven voor invoer. Bij elkaar op die manier kunnen Hallo gebruiker tooperform gegevensanalyse verwerken voor streaminggegevens scenario's.

toostart met Stream Analytics, begint u met het maken van een nieuwe Stream Analytics-taak.  Houd er rekening mee dat deze actie heeft geen gevolgen voor facturering totdat het Hallo-taak is gestart.

1. Meld u aan bij de online Hallo [klassieke Azure-portal](http://manage.windowsazure.com) of Hallo [Azure-portal](https://portal.azure.com/).
2. In de portal Hallo: **op nieuw**, klikt u vervolgens op **Data Services** of **gegevensanalyse** afhankelijk van uw portal en klik vervolgens op **Azure Stream Analytics** of **Stream Analytics** en vervolgens **snelle invoer**.
   
   ![Wizard gegevensverwerking analytics-taak](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Gegevensanalyse taakverwerking maken](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. Hallo gewenste configuratie voor de Stream Analytics-taak Hallo opgeven.
   
   * In Hallo **taaknaam** Voer een naam tooidentify Hallo Stream Analytics-taak. Wanneer Hallo **taaknaam** is gevalideerd, verschijnt een groen vinkje in Hallo taaknaam vak. Hallo **taaknaam** mag alleen alfanumerieke tekens bevatten en Hallo '-' bevatten, en moet tussen 3 en 63 tekens.
   * Gebruik **regio** in hello Azure-portal of **locatie** in hello Azure portal toospecify Hallo geografische locatie waar u toorun Hallo taak.
   * Als u met behulp van hello Azure-portal, selecteer of maak een toouse storage-account als Hallo **Opslagaccount regionale controle**. Dit opslagaccount wordt gebruikt toostore bewakingsgegevens voor alle Stream Analytics-taken die in deze regio worden uitgevoerd.
   * Als u met behulp van Azure-portal hello, geeft u een nieuwe of bestaande **resourcegroep** toohold verwante resources voor uw toepassing.
4. Wanneer u nieuwe opties voor Stream Analytics-taak Hallo zijn geconfigureerd, klikt u op **Stream Analytics-taak maken**. Het kan enkele minuten duren voordat Hallo Stream Analytics-taak toobe gemaakt. toocheck hello status, kunt u voortgang Hallo in Hallo Notification hubs.
   
   ![Gegevens analytics verwerking taak Notification hubs](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure portal gegevensanalyse verwerken taak taak maken](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. Hallo nieuwe taak wordt de status weergegeven **gemaakt**. U ziet dat Hallo **Start** knop is uitgeschakeld. Hallo taak invoer-, query- en uitvoer configureren voordat u begint met Hallo-taak.
   
   ![Gegevensverwerking analytics-taak Status](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure portal gegevensanalyse taakstatus verwerken](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

