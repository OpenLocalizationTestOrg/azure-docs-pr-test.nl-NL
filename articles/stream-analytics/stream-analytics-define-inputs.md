---
title: 'Gegevensverbinding: gegevensstroom invoer van een stroom gebeurtenissen | Microsoft Docs'
description: Meer informatie over het instellen van een data verbinding tooStream Analytics 'invoer' genoemd. Invoer bevatten een gegevensstroom van gebeurtenissen en ook verwijzen naar gegevens.
keywords: gegevensstroom, gegevensverbinding, stroom gebeurtenissen
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 8155823c-9dd8-4a6b-8393-34452d299b68
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/05/2017
ms.author: samacha
ms.openlocfilehash: be2008f159061c5c9be9d0314c27fa67193e3269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-connection-learn-about-data-stream-inputs-from-events-toostream-analytics"></a>Gegevensverbinding: meer informatie over gegevens invoer van de stroom van gebeurtenissen tooStream Analytics
Hallo gegevens verbinding tooa Stream Analytics-taak is een stream van gebeurtenissen van een gegevensbron, waarnaar wordt verwezen tooas Hallo taak *invoer*. Stream Analytics is een uitstekende integratie met Azure stream gegevensbronnen, waaronder [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/), en [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/). Deze bronnen kunnen afkomstig zijn uit Hallo invoer hetzelfde Azure-abonnement als analytics-taak of vanuit een ander abonnement.

## <a name="data-input-types-data-stream-and-reference-data"></a>Gegevens invoertypen: de stroom- en referentiegegevens samenvoegt gegevens
Als de gegevensbron tooa wordt doorgeschoven, gegevens, heeft gebruikt door de Stream Analytics-taak Hallo en verwerkt in realtime. Invoer worden onderverdeeld in twee typen: gegevens stream invoer en verwijzen naar gegevens invoer.

### <a name="data-stream-inputs"></a>Gegevensstroom invoer
Een gegevensstroom is een niet-gebonden reeks gebeurtenissen gedurende een bepaalde periode. Stream Analytics-taken moeten ten minste één gegevensstroominvoer bevatten. Event Hubs, IoT-Hub en Blob-opslag worden ondersteund als invoer gegevensbronnen stroom. Event hubs zijn gebruikte toocollect gebeurtenisstromen van meerdere apparaten en services. Deze stromen kunnen sociale media activiteitsfeeds, gegevens over voorraad handel of gegevens van sensoren bevatten. IoT hubs zijn geoptimaliseerde toocollect gegevens van verbonden apparaten in scenario's voor Internet der dingen (IoT).  BLOB-opslag kan worden gebruikt als een invoerbron voor het opnemen van grote hoeveelheden gegevens als een stream, zoals logboekbestanden.  

### <a name="reference-data"></a>Referentiegegevens
Stream Analytics ondersteunt ook bekend als invoer *referentiegegevens*. Dit zijn aanvullende gegevens die statische is of waarmee traag wordt gewijzigd. Dit wordt meestal gebruikt voor het uitvoeren van de correlatie en zoekacties. Bijvoorbeeld, u mogelijk join gegevens Hallo gegevensstroom invoer toodata in referentiegegevens hello, net als u een SQL-join-toolook statische waarden wilt uitvoeren. Azure Blob-opslag bevindt zich momenteel in de invoerbron Hallo alleen ondersteund voor referentiegegevens. Verwijzing naar gegevensbron blobs zijn beperkt too100 MB groot.

hoe toocreate verwijzing gegevens invoer zien toolearn [gebruik referentiegegevens](stream-analytics-use-reference-data.md).  

## <a name="create-data-stream-input-from-event-hubs"></a>Gegevensstroominvoer van Event Hubs maken

Azure Event Hubs is zeer schaalbaar gebeurtenis ingestors publiceren / abonneren. Een event hub kunt miljoenen gebeurtenissen per seconde verzamelen zodat u kunt verwerken en analyseren van Hallo enorme hoeveelheden gegevens die worden geproduceerd door verbonden apparaten en toepassingen. Event Hubs en Stream Analytics samen bieden u een end-to-end-oplossing voor realtime analyses: Event Hubs kunt u gebeurtenissen in Azure-kanaal in realtime en Stream Analytics-taken die gebeurtenissen in realtime kunnen verwerken. U kunt bijvoorbeeld web klikken, sensormetingen of online logboek gebeurtenissen tooEvent Hubs verzenden. Vervolgens kunt u de Stream Analytics-taken toouse Event Hubs maken als Hallo invoergegevens gegevensstromen voor realtime filteren, aggregeren en correlatie.

Hallo standaard tijdstempel van gebeurtenissen die afkomstig zijn van Event Hubs in Stream Analytics is Hallo tijdstempel die Hallo gebeurtenis ontvangen in Hallo event hub, namelijk `EventEnqueuedUtcTime`. tooprocess Hallo gegevens als een stream met een tijdstempel in nettolading hello, moet u Hallo [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) sleutelwoord.

### <a name="consumer-groups"></a>Consumergroepen
Een eigen consumergroep, moet u elke Stream Analytics event hub invoer toohave configureren. Wanneer een taak een self-join bevat of wanneer er meerdere invoer, kan sommige invoer worden gelezen door meer dan één lezer downstream. Deze situatie heeft impact op Hallo aantal lezers in een enkel consumergroep. tooavoid van meer dan Hallo Event Hubs limiet van vijf lezers per klantengroep per partitie, is een best practice toodesignate een consumer groep voor elke Stream Analytics-taak. Er is een limiet van 20 consumergroepen per event hub. Zie voor meer informatie [Event Hubs-programmeergids](../event-hubs/event-hubs-programming-guide.md).

### <a name="configure-an-event-hub-as-a-data-stream-input"></a>Een event hub configureren als een gegevensstroom invoer
Hallo volgende tabel bevat uitleg over elke eigenschap in Hallo **nieuwe invoer** blade in hello Azure-portal als u een event hub als invoer configureert.

| Eigenschap | Beschrijving |
| --- | --- |
| **Invoeralias** |Een beschrijvende naam die u in het Hallo-taak query tooreference gebruiken deze invoer. |
| **Service bus-naamruimte** |Een naamruimte Azure Service Bus is een container voor een set berichtentiteiten. Wanneer u een nieuwe event hub maakt, maakt u ook een Service Bus-naamruimte. |
| **Naam Event hub** |Hallo-naam van Hallo event hub toouse als invoer. |
| **Naam Event hub-beleid** |Hallo beleid voor gedeelde toegang waarmee toegang toohello event hub. Elk gedeeld toegangsbeleid heeft een naam, machtigingen die u instelt en toegangssleutels. |
| **Event hub consumergroep** (optioneel) |Hallo groep toouse tooingest consumentgegevens van Hallo event hub. Als geen consumentengroepen is opgegeven, gebruikt Stream Analytics-taak Hallo Hallo standaard consumergroep. Het is raadzaam om gebruik te maken van een afzonderlijke klantengroep voor elke Stream Analytics-taak. |
| **Gebeurtenis serialisatie-indeling** |Hallo serialisatie-indeling (JSON, CSV of Avro) van de inkomende gegevensstroom Hallo. |
| **Codering** | UTF-8 wordt momenteel alleen ondersteund Hallo coderingsindeling. |

Wanneer de gegevens afkomstig zijn van een event hub, hebt u toegang toohello na de metagegevensvelden in de Stream Analytics-query:

| Eigenschap | Beschrijving |
| --- | --- |
| **EventProcessedUtcTime** |Hallo-datum en tijd is die gebeurtenis Hallo verwerkt door Stream Analytics. |
| **EventEnqueuedUtcTime** |Hallo-datum en tijd worden die Hallo-gebeurtenis is ontvangen door de Event Hubs. |
| **PartitionId** |Hallo op nul gebaseerde partitie-ID voor invoer Hallo-adapter. |

Bijvoorbeeld, kunt u deze velden gebruikt, u een query schrijven zoals Hallo voorbeeld te volgen:

````
SELECT
    EventProcessedUtcTime,
    EventEnqueuedUtcTime,
    PartitionId
FROM Input
````

## <a name="create-data-stream-input-from-iot-hub"></a>Gegevensstroominvoer uit IoT Hub maken
Azure Iot Hub is een uiterst schaalbare voor publiceren / abonneren event ingestor is geoptimaliseerd voor IoT-scenario's.

Hallo standaard tijdstempel van gebeurtenissen die afkomstig zijn van een IoT-hub in Stream Analytics is Hallo tijdstempel die Hallo gebeurtenis ontvangen in Hallo IoT-hub is `EventEnqueuedUtcTime`. tooprocess Hallo gegevens als een stream met een tijdstempel in nettolading hello, moet u Hallo [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) sleutelwoord.

> [!NOTE]
> Alleen berichten met een `DeviceClient` eigenschap kan worden verwerkt.
> 
> 

### <a name="consumer-groups"></a>Consumergroepen
Een eigen consumergroep, moet u elke Stream Analytics IoT hub invoer toohave configureren. Wanneer een taak een self-join bevat of wanneer er meerdere invoer, kan sommige invoer worden gelezen door meer dan één lezer downstream. Deze situatie heeft impact op Hallo aantal lezers in een enkel consumergroep. tooavoid van meer dan hello Azure IoT Hub limiet van vijf lezers per klantengroep per partitie, is een best practice toodesignate een consumer groep voor elke Stream Analytics-taak.

### <a name="configure-an-iot-hub-as-a-data-stream-input"></a>Een IoT-hub configureren als een gegevensstroom invoer
Hallo volgende tabel bevat uitleg over elke eigenschap in Hallo **nieuwe invoer** blade in hello Azure-portal als u een IoT-hub als invoer configureert.

| Eigenschap | Beschrijving |
| --- | --- |
| **Invoeralias** |Een beschrijvende naam die u in het Hallo-taak query tooreference gebruiken deze invoer.|
| **IoT-hub** |Hallo-naam van Hallo IoT hub toouse als invoer. |
| **Eindpunt** |Hallo-eindpunt voor Hallo IoT-hub.|
| **Naam van beleid voor gedeelde toegang** |Hallo gedeeld toegangsbeleid waarmee toegang toohello IoT-hub. Elk gedeeld toegangsbeleid heeft een naam, machtigingen die u instelt en toegangssleutels. |
| **Beleid voor gedeelde toegangssleutel** |Hallo gedeelde toegangssleutel gebruikt tooauthorize toegang toohello IoT-hub. |
| **Consumergroep** (optioneel) |Hallo groep toouse tooingest consumentgegevens uit Hallo iothub. Als geen consumentengroepen is opgegeven, wordt een Stream Analytics-taak Hallo standaard consumergroep. Het is raadzaam om gebruik te maken van een andere klantengroep voor elke Stream Analytics-taak. |
| **Gebeurtenis serialisatie-indeling** |Hallo serialisatie-indeling (JSON, CSV of Avro) van de inkomende gegevensstroom Hallo. |
| **Codering** |UTF-8 wordt momenteel alleen ondersteund Hallo coderingsindeling. |

Wanneer de gegevens afkomstig zijn van een iothub, hebt u toegang toohello na de metagegevensvelden in de Stream Analytics-query:

| Eigenschap | Beschrijving |
| --- | --- |
| **EventProcessedUtcTime** |Hallo-datum en tijd is die gebeurtenis Hallo verwerkt. |
| **EventEnqueuedUtcTime** |Hallo-datum en tijd die gebeurtenis Hallo heeft ontvangen Hallo IoT-hub. |
| **PartitionId** |Hallo op nul gebaseerde partitie-ID voor invoer Hallo-adapter. |
| **IoTHub.MessageId** | Een ID die communicatie in twee richtingen toocorrelate in IoT-hub is gebruikt. |
| **IoTHub.CorrelationId** |Een ID die wordt gebruikt voor antwoorden op berichten en feedback van IoT-hub. |
| **IoTHub.ConnectionDeviceId** |Hallo verificatie-ID gebruikt toosend dit bericht. Deze waarde wordt door de IoT-hub Hallo op servicebound berichten vermeld. |
| **IoTHub.ConnectionDeviceGenerationId** |generatie-ID van het Hallo Hallo geverifieerde apparaat dat gebruikt toosend is dit bericht. Deze waarde wordt door de IoT-hub Hallo op servicebound berichten vermeld. |
| **IoTHub.EnqueuedTime** |Hallo-tijd waarop het Hallo-bericht is ontvangen door de Hallo iothub. |
| **IoTHub.StreamId** |Een aangepaste gebeurteniseigenschap toegevoegd door Hallo afzender apparaat. |


## <a name="create-data-stream-input-from-blob-storage"></a>Gegevensstroominvoer van Blob-opslag maken
Azure Blob-opslag biedt een rendabele en schaalbare oplossing voor scenario's met grote hoeveelheden ongestructureerde gegevens toostore in Hallo cloud. Gegevens in Blob storage is meestal beschouwd als gegevens in rust. Maar kan deze worden verwerkt als een gegevensstroom door Stream Analytics. Een typisch scenario voor Blob storage-ingangen met Stream Analytics is de verwerking van logboekbestanden. In dit scenario telemetriegegevens van een systeem is opgenomen en behoeften toobe geparseerd en tooextract betekenisvolle gegevens verwerkt.

Hallo standaard tijdstempel van Blob storage-gebeurtenissen in de Stream Analytics is Hallo tijdstempel die Hallo blob het laatst is gewijzigd, namelijk `BlobLastModifiedUtcTime`. tooprocess Hallo gegevens als een stream met een tijdstempel in nettolading hello, moet u Hallo [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) sleutelwoord.

CSV-indeling invoer *vereisen* een header rij toodefine velden voor Hallo-gegevensset. Alle koptekstvelden rij moeten bovendien uniek zijn.

> [!NOTE]
> Stream Analytics biedt geen ondersteuning voor het toevoegen van inhoud tooan bestaande blob. Stream Analytics wordt slechts één keer een blob weergeven en wijzigingen die in Hallo blob plaatsvinden nadat Hallo taak Hallo gegevens leesrechten niet zijn verwerkt. Een aanbevolen procedure is tooupload alle Hallo gegevens eenmaal en voeg vervolgens niet gebeurtenissen toothat bloblarchief.
> 

### <a name="configure-blob-storage-as-a-data-stream-input"></a>Blob-opslag configureren als een gegevensstroom invoer

Hallo volgende tabel bevat uitleg over elke eigenschap in Hallo **nieuwe invoer** blade in hello Azure-portal als u een Blob-opslag als invoer configureert.

| Eigenschap | Beschrijving |
| --- | --- |
| **Invoeralias** | Een beschrijvende naam die u in het Hallo-taak query tooreference gebruiken deze invoer. |
| **Opslagaccount** | Hallo-naam van Hallo storage-account waarin Hallo blob bestanden opgeslagen worden. |
| **De sleutel van opslagaccount** | de geheime sleutel Hallo Hallo storage-account gekoppeld. |
| **Container** | Hallo-container voor Hallo blob-invoer. Containers bieden een logische groepering van blobs die zijn opgeslagen in Hallo Microsoft Azure Blob-service. U moet een container voor blob opgeven tijdens het uploaden van een blob toohello Azure Blob storage-service. |
| **Het pad** (optioneel) | Hallo-bestandspad toolocate Hallo blobs in de opgegeven container Hallo gebruikt. Binnen Hallo pad, kunt u een of meer exemplaren van de volgende drie variabelen Hallo: `{date}`, `{time}`, of`{partition}`<br/><br/>Voorbeeld 1:`cluster1/logs/{date}/{time}/{partition}`<br/><br/>Voorbeeld 2:`cluster1/logs/{date}`<br/><br/>Hallo `*` teken is geen toegestane waarde voor Hallo pad voorvoegsel. Alleen geldige <a HREF="https://msdn.microsoft.com/library/azure/dd135715.aspx">Azure blob-tekens</a> zijn toegestaan. |
| **De datumnotatie** (optioneel) | Als u Hallo datum variabele in pad hello gebruikt, Hallo datumnotatie in welke Hallo bestanden zijn ingedeeld. Voorbeeld:`YYYY/MM/DD` |
| **Tijdnotatie** (optioneel) |  Als u Hallo-tijdvariabele in Hallo pad, Hallo tijdnotatie in welke Hallo bestanden zijn ingedeeld. Op dit moment alleen ondersteund Hallo-waarde is `HH`. |
| **Gebeurtenis serialisatie-indeling** | Hallo serialisatie-indeling (JSON, CSV of Avro) voor inkomende gegevensstromen. |
| **Codering** | Voor de CSV en JSON is UTF-8 momenteel coderingsindeling Hallo alleen ondersteund. |

Wanneer de gegevens afkomstig zijn van een Blob storage-bron, hebt u toegang toohello na de metagegevensvelden in de Stream Analytics-query:

| Eigenschap | Beschrijving |
| --- | --- |
| **BlobName** |Hallo-naam van Hallo blob-invoerbron die gebeurtenis Hallo van afkomstig is. |
| **EventProcessedUtcTime** |Hallo-datum en tijd is die gebeurtenis Hallo verwerkt door Stream Analytics. |
| **BlobLastModifiedUtcTime** |Hallo-datum en tijd Hallo blob laatst is gewijzigd. |
| **PartitionId** |Hallo op nul gebaseerde partitie-ID voor invoer Hallo-adapter. |

Bijvoorbeeld, kunt u deze velden gebruikt, u een query schrijven zoals Hallo voorbeeld te volgen:

````
SELECT
    BlobName,
    EventProcessedUtcTime,
    BlobLastModifiedUtcTime
FROM Input
````

## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen
U hebt geleerd over opties voor gegevensverbinding in Azure voor uw Stream Analytics-taken. toolearn meer informatie over Stream Analytics, Zie:

* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
