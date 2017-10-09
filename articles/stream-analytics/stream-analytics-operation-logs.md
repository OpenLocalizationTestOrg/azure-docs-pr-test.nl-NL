---
title: aaaDebug met bewerking en service-Logboeken in Stream Analytics | Microsoft Docs
description: Hoe toouse Stream Analytics-bewerkingslogboeken
keywords: Service-Logboeken
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a>Fouten opsporen-service en bewerking logboeken met Stream Analytics-taken
Alle Azure-services levering operationele berichten toousers toorecord logboekdetails toomanagement bewerkingen gerelateerd. Deze informatie kan worden gebruikt voor foutopsporing zoals taakstatus, de voortgang van de taak en fout berichten tootrack Hallo voortgang van een taak gedurende een periode van start tooprocessing toooutput weergeven in Azure Stream Analytics.

## <a name="find-operation-logs-in-hello-azure-management-portal"></a>Bewerkingslogboeken op Hallo Azure Management portal zoeken
Bewerkingslogboeken toegankelijk zijn op twee manieren:  

* Dashboard van Hallo Stream Analytics-taak  
* Management-Services in de klassieke Azure-portal Hallo  

## <a name="dashboard-of-hello-stream-analytics-job"></a>Dashboard van Hallo Stream Analytics-taak
Een koppeling toohello overeenkomt logboeken van een Stream Analytics-taak wordt weergegeven op het tabblad van de taak van het Hallo-Dashboard. Als u op de koppeling klikt, wordt ingesteld Hallo filters zodanig dat het meest recente logboeken voor die specifieke taak bevat.

  ![Selecteer beheerservices Logboeken](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a>Management-Services
toomanually Navigeer toohello Bewerkingslogboeken voor Stream Analytics en andere services in de klassieke Azure-portal Hallo:

1. Klik op **beheerservices** in Hallo [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer **Stream Analytics** voor **Type** en Hallo-naam van de taak Hallo voor **servicenaam**.  
   
   ![Selecteer de Stream Analytics](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a>Controlelogboeken niet vinden in hello Azure-portal
toofind operationele logboeken voor de Stream Analytics-taak in hello Azure-portal, klikt u op **Bladeren** en selecteer vervolgens **controlelogboeken**.

  ![Azure-portal Stream Analytics selecteren](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

Hiermee opent u een blade met gebeurtenissen van Hallo afgelopen 7 dagen voor alle resources in uw abonnement.  U kunt toosee gebeurtenissen van een type opgeven of het tijdsbestek filteren door te klikken op Hallo **Filter** opdracht.

  ![Azure-portal Stream Analytics selecteren](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a>Logboekdetails van het ophalen
U kunt filteren op Status tooview Hallo logboeken en tijdsbereik voor uw project.

Hello Azure-beheerportal, klik op Hallo **Details** knop onderaan Hallo Hallo venster tooview meer informatie over een geselecteerde gebeurtenis. 

  ![Details van selecteren](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

Azure-portal, klik op een vermelding logboek toosee Hallo in Hallo gedetailleerde gebeurtenissen in het.

  ![Azure-portal Details selecteren](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

Daar kunt u Hallo openen **Detail** blade door te klikken op Hallo-gebeurtenis.

  ![Azure-portal Details selecteren](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a>Fouten opsporen in een mislukte taak
Klik op het zoekpictogram Hallo in hello Azure-beheerportal, en typ 'mislukt'. Hiermee geeft u een resultaat van alle logboeken met fouten. 

  ![Foutopsporing van een taak die is mislukt](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

In hello Azure-portal, kunt u filteren op niveau van het bericht tooview **Kritiek** gebeurtenissen.

  ![Azure portal foutopsporing](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

Selecteer een van de Hallo fouten en klik op Hallo **Details** voor meer informatie over Hallo-fout.  Bepaalde foutberichten bevatten ook informatie over hoe toomitigate Hallo probleem. 

  ![Details van bewerking](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

Geval u toocontact moet [ondersteuning](https://azure.microsoft.com/support/options/) of geef informatie toohello team via Hallo [MSDN-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), houd er rekening mee Hallo operationele Details, speciaal Hallo **correlatie-ID**. 

## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

