---
title: aaaIntroduction tooStream Analytics | Microsoft Docs
description: Meer informatie over Stream Analytics, een beheerde service waarmee u streaminggegevens van Hallo Internet der dingen (IoT) analyseren in realtime.
keywords: analyse als een service, beheerde services, verwerking van streams, analyse van streams, wat is analyse van streams
services: stream-analytics
documentationcenter: 
author: jenniehubbard
manager: jhubbard
editor: cgronlun
ms.assetid: 613c9b01-d103-46e0-b0ca-0839fee94ca8
ms.service: stream-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/08/2017
ms.author: jhubbard
ms.openlocfilehash: 6dd7ea1d358bcc94e927a3e699a2771a25104d72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-stream-analytics"></a>Wat is een Stream Analytics?

Azure Stream Analytics is een volledig beheerde verwerkingsengine voor gebeurtenissen, waarmee u in real time analytische berekeningen kunt uitvoeren op gegevensstromen. Hallo-gegevens kunnen afkomstig zijn van apparaten, sensoren, websites, sociale media feeds, toepassingen, infrastructuursystemen en meer. 

## <a name="what-can-i-do-with-stream-analytics"></a>Wat kan ik doen met Stream Analytics?

Gebruik van Stream Analytics tooexamine grote hoeveelheden gegevens van apparaten of processen, gegevens ophalen uit de gegevensstroom Hallo en zoek naar patronen, trends en relaties. Op basis van wat is er in het Hallo-gegevens, kunt u vervolgens toepassingstaken uitvoeren. U kan bijvoorbeeld waarschuwingen worden gegeven, ere van automation-werkstromen, informatie tooa hulpprogramma zoals Power BI reporting feed of gegevens opslaan voor later onderzoek. 

Voorbeelden:

* Persoonlijke realtimeanalyses van aandelenkoersen en meldingen van financiële dienstverleners.
* Fraudedetectie in real time op basis van transactiegegevens. 
* Services ter beveiliging van gegevens en identiteit.
* Analyse van gegevens die zijn gegenereerd door sensoren en actuators in fysieke objecten (het Internet of Things, IoT).
* Clickstream-analyses op internet.
* CRM-toepassingen (Customer Relationship Management) voor bijvoorbeeld het genereren van waarschuwingen wanneer de klantervaring verslechtert gedurende een bepaalde periode.

## <a name="how-does-stream-analytics-work"></a>Hoe werkt Stream Analytics?

Dit diagram ziet u Hallo Stream Analytics pipeline, die laat zien hoe gegevens wordt ingenomen, geanalyseerd en vervolgens verzonden voor presentatie of actie. 

![Stream Analytics-pijplijn](./media/stream-analytics-introduction/stream_analytics_intro_pipeline.png)

Stream Analytics begint met een gegevensstroom als bron. Hallo-gegevens kunnen worden ingenomen in Azure vanaf een apparaat met een Azure event hub of IoT-hub. Hallo-gegevens kunnen ook worden opgehaald uit een gegevensarchief zoals Azure Blob Storage. 

tooexamine hello stream, maakt u een Stream Analytics *taak* die aangeeft waar Hallo gegevens vandaan komt. Hallo-taak bevat ook een *transformatie*&mdash;hoe toolook van gegevens, patronen of relaties. Voor deze taak ondersteunt Stream Analytics een SQL-achtige querytaal, waarmee u gegevens kunt filteren, sorteren en combineren en gegevensstromen kunt samenvoegen gedurende een bepaalde periode.

Ten slotte geeft Hallo taak een uitvoer toosend Hallo getransformeerd gegevens. Hiermee kunt u bepalen welke toodo in antwoord toohello informatie die u hebt geanalyseerd. In het antwoord tooanalysis kunt u bijvoorbeeld:

* Een opdracht toochange-instellingen van een apparaat verzenden. 
* Verzenden van gegevens tooa wachtrij die wordt bewaakt door een proces dat actie op basis neemt van wat er is gevonden. 
* Verzenden van gegevens tooa Power BI-dashboard voor rapportage.
* Verzenden van gegevens toostorage zoals Data Lake Store, SQL Server-database of Azure Blob of Table storage.

Terwijl een taak wordt uitgevoerd, kunt u die bewaken en instellen hoeveel gebeurtenissen per seconde er moeten worden verwerkt. U kunt ook diagnostische logboeken laten genereren voor het oplossen van problemen.

## <a name="key-capabilities-and-benefits"></a>Belangrijkste mogelijkheden en voordelen

Stream Analytics is ontworpen toobe eenvoudig toouse flexibele, schaalbare tooany taak grootte en voordelige.

### <a name="connectivity-toomany-inputs-and-outputs"></a>Connectiviteit toomany in- en uitgangen

Stream Analytics maakt verbinding rechtstreeks te[Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) en [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) voor streamopname en Hallo [Azure Blob storage-service](https://docs.microsoft.com/azure/storage/storage-introduction#blob-storage-accounts) tooingest historische gegevens. Als u gegevens ontvangt van gebeurtenishubs, kunt u Stream Analytics combineren met andere gegevensbronnen en verwerkingsengines.

De invoer van taken kan ook referentiegegevens (statische of langzaam veranderende gegevens) omvatten. U kunt deelnemen aan streaming gegevens toothis verwijzing gegevens tooperform lookup operations Hallo dezelfde manier als met databasequery's.

U kunt de uitvoer van een Stream Analytics-taak in verschillende richtingen sturen. U kunt toostorage, zoals Azure Storage blobs of tabellen, Azure SQL DB, Azure Data Lake winkels of Azure Cosmos DB schrijven. Hallo-gegevens mogelijk voor batch-analyses van daaruit Ga via Azure HDInsight. U kunt verzenden Hallo uitvoer tooanother voor verbruik door een ander proces, zoals event hubs, Azure Service Bus-onderwerpen of wachtrijen. U kunt Hallo uitvoer tooPower BI voor visualisatie kan verzenden.

### <a name="ease-of-use"></a>Gebruiksgemak

Wanneer u een eenvoudige, declaratieve toodefine transformaties gebruiken [querytaal van Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) waarmee u het maken van geavanceerde analyses met niets te programmeren. Hallo-querytaal duurt streaminggegevens als invoer. U kunt vervolgens Hallo gegevens filteren en sorteren, cumulatieve waarde, berekeningen, koppelt gegevens (binnen een stream of tooreference gegevens) en georuimtelijke functies gebruiken. U kunt query's in het Hallo-portal bewerken met IntelliSense en syntaxiscontrole en u query's met voorbeeldgegevens die kan worden opgehaald uit Hallo live stream kunt testen.

### <a name="extensible-query-language"></a>Uitbreidbare querytaal

U kunt Hallo-mogelijkheden van Hallo querytaal uitbreiden door te definiëren en extra functies aanroepen. U kunt functieaanroepen definiëren in hello Azure Machine Learning service tootake profiteren van Azure Machine Learning-oplossingen. U kunt ook JavaScript gebruiker gedefinieerde functies (UDF's) in de volgorde tooperform complexe berekeningen integreren als onderdeel van een Stream Analytics query.

### <a name="scalability"></a>Schaalbaarheid

Stream Analytics kan up too1 GB van binnenkomende gegevens per seconde verwerken. Integratie met [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) en [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) taken tooingest miljoenen gebeurtenissen per tweede afkomstig van verbonden apparaten, clickstreams en logboekbestanden, tooname kan een paar. Hallo partitie functie van event hubs gebruikt, kunt u berekeningen in logische stappen partitioneren, elk met Hallo mogelijkheid toobe verder tooincrease schaalbaarheid gepartitioneerd.

### <a name="low-cost"></a>Lage kosten

Als een cloudservice is Stream Analytics geoptimaliseerd toolet aan de slag tegen lage kosten. U omslagstelsel op basis van streaming-eenheid gebruiks- en Hallo hoeveelheid gegevens verwerkt door Hallo-systeem. Gebruik wordt berekend op basis van Hallo volume aan verwerkte gebeurtenissen en Hallo hoeveelheid computercapaciteit binnen Hallo cluster toohandle ingericht met Stream Analytics-taken.

### <a name="reliability-quick-recovery-and-repeatability"></a>Betrouwbaarheid, snel herstel en herhaalbaarheid

Als een beheerde service in Hallo cloud, Stream Analytics helpt gegevensverlies voorkomen en biedt bedrijfscontinuïteit. Als er fouten optreden, biedt Hallo service ingebouwde herstelfuncties. Hallo mogelijkheid toointernally status onderhouden, Hallo service herhaalbare resultaten zodat het is mogelijk tooarchive gebeurtenissen en pas verwerking in de toekomst hello wordt altijd dezelfde resultaten ophalen Hallo biedt. Hiermee kunt u toogo terug in tijd en berekeningen onderzoeken terwijl hoofdoorzaak worden geanalyseerd, wat-als-analyse, enzovoort.

## <a name="next-steps"></a>Volgende stappen

* Aan de slag met het [experimenteren met invoer en query’s van IoT-apparaten](stream-analytics-get-started-with-azure-stream-analytics-to-process-data-from-iot-devices.md).
* Bouwen een [Stream Analytics-oplossing voor end-to-end](stream-analytics-real-time-fraud-detection.md) die moet telefoon metagegevens toolook voor frauduleuze aanroepen worden gecontroleerd.
* Meer informatie over Hallo SQL-achtige querytaal voor Stream Analytics en over unieke concepten zoals [vensterfuncties](stream-analytics-window-functions.md).
* Meer informatie over hoe te[Stream Analytics-taken schalen](stream-analytics-scale-jobs.md). 
* Meer informatie over hoe te[Stream Analytics en Azure Machine Learning integreren](stream-analytics-machine-learning-integration-tutorial.md).
* Antwoorden tooyour Stream Analytics vragen vinden in Hallo [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

