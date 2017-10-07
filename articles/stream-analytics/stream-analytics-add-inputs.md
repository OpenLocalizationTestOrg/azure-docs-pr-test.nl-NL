---
title: een data aaaAdd invoer tooyour Stream Analytics-taken | Microsoft Docs
description: Meer informatie over hoe toohook van een data source tooyour Stream Analytics als streaming gegevensinvoer uit Event Hubs of verwijzing gegevens uit Blog van storage taak.
keywords: gegevens invoeren, streamen van gegevens
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a>Een streaming invoer- of gegevens tooa Stream Analytics-taak toevoegen
Meer informatie over hoe toohook van een data source tooyour Stream Analytics taak als streaming gegevensinvoer uit Event Hubs of verwijzing gegevens uit Blob storage.

Azure Stream Analytics-taken kunnen worden verbonden tooone gegevensinvoer of meer, die elk een verbinding tooan bestaande gegevensbron definiëren. Wanneer gegevens worden verzonden toothat gegevensbron, wordt gebruikt door de Stream Analytics-taak Hallo en verwerkt in realtime als het streamen van gegevens. Stream Analytics heeft eerste-klas integratie met [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) en [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) zowel binnen als buiten van de taak van het Hallo-abonnement.

In dit artikel is een stap in Hallo [leertraject voor Stream Analytics](/documentation/learning-paths/stream-analytics/).

## <a name="data-input-streaming-data-and-reference-data"></a>Invoer: Streaming en verwijzingsgegevens
Er zijn twee verschillende soorten invoer in Stream Analytics: gegevensstromen en referentiegegevens.

* **Gegevensstromen**: Stream Analytics-taken moeten ten minste één gegevensstroom invoer toobe verbruikt en getransformeerd door Hallo taak bevatten. Azure Blob storage en Azure Event Hubs worden ondersteund als invoer gegevensbronnen stroom. Azure Event Hubs zijn gebruikte toocollect gebeurtenisstromen van verbonden apparaten, services en toepassingen. Azure Blob-opslag kan worden gebruikt als een invoerbron voor het opnemen van grote hoeveelheden gegevens als een stroom.  
* **Referentiegegevens**: Stream Analytics ondersteunt een tweede gegevenstype reserve invoerverwijzing genoemd.  Als de tegengestelde toodata in beweging zijn deze gegevens statisch of vertraging wijzigen.  Dit wordt meestal gebruikt voor het uitvoeren van de op te zoeken en correlatie met gegevensstromen toocreate een uitgebreidere set van gegevens.  Azure Blob-opslag bevindt zich momenteel in de invoerbron Hallo alleen ondersteund voor referentiegegevens.  

tooadd een invoer tooyour Stream Analytics-taak:

1. Klik in hello Azure-portal op **invoer** en klik vervolgens op **invoer toevoegen** in uw Stream Analytics-taak.
   
    ![Klassieke Azure-portal - invoer toevoegen.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    Klik in hello Azure-portal op Hallo **invoer** -tegel in de Stream Analytics-taak.  
   
    ![Azure-portal - invoer toevoegen.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. Geef Hallo Hallo invoer: beide **gegevensstroom** of **referentiegegevens**.
   
    ![Invoer, gestreamd of verwijst naar de juiste gegevens Hallo toevoegen](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Invoer, gestreamd of verwijst naar de juiste gegevens Hallo toevoegen](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. Als het maken van een gegevensstroom invoer opgeven Hallo brontype voor Hallo-invoer.  Deze stap worden overgeslagen tijdens het maken van referentiegegevens als alleen-Blob-opslag op dit moment wordt ondersteund.
   
    ![Gegevens gegevensstroominvoer toevoegen](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Gegevens gegevensstroominvoer toevoegen](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. Geef een beschrijvende naam voor deze invoer in Hallo Invoeralias vak.  Deze naam wordt gebruikt in uw job query later op toorefer toohello invoer.
   
    Vul de overige Hallo van Hallo vereiste verbinding eigenschappen tooconnect tooyour-gegevensbron. Deze velden verschillen per type van het type invoer- en bron en worden gedefinieerd in detail [hier](stream-analytics-create-a-job.md).  
   
    ![Event hub gegevensinvoer toevoegen](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. Hallo serialisatie instellingen opgeven voor de invoergegevens Hallo:
   
   * controleren of uw query's werken Hallo zoals verwacht toomake Hallo opgeven **gebeurtenis serialisatie-indeling** van binnenkomende gegevens.  Ondersteunde serialisatie-indelingen zijn JSON, CSV en Avro.
   * Controleer of Hallo **codering** voor Hallo-gegevens.  UTF-8 wordt de coderingsindeling Hallo alleen ondersteund op dit moment.
     
     ![Instellingen voor serialisatie van gegevens voor gegevensinvoer Hallo](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Instellingen voor serialisatie van gegevens voor gegevensinvoer Hallo](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. Na het voltooien van de invoer maken Hallo Stream Analytics controleert of dat deze de invoerbron toohello verbinding kan maken.  U kunt Hallo status Hallo testverbinding bewerking bekijken in Hallo Notification hub.
   
    ![De testverbinding Hallo gegevensstromen invoer](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![De testverbinding Hallo gegevensstromen invoer](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a>Hulp bij het streaming-gegevens invoeren
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

