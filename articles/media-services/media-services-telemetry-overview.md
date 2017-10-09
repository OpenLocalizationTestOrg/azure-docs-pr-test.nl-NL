---
title: Media Services telemetrie aaaAzure | Microsoft Docs
description: In dit artikel biedt een overzicht van telemetrie van Azure Media Services.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95c20ec4-c782-4063-8042-b79f95741d28
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 659e1c947a77aad0e4acacb541d95714da4775ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-telemetry"></a>Azure Media Services-telemetrie

Azure Media Services (AMS) kunt u tooaccess telemetrie/metrische gegevens voor de services. Hallo huidige versie van AMS kunt u het verzamelen van telemetriegegevens voor live **kanaal**, **StreamingEndpoint**, en live **archief** entiteiten. 

Telemetrie tooa opslag tabel is geschreven in een Azure Storage-account dat u opgeeft (normaal gesproken zou u Hallo storage-account is gekoppeld aan uw AMS-account gebruiken). 

Hallo telemetrie system beheert niet bewaren van gegevens. U kunt Hallo oude telemetrische gegevens verwijderen door Hallo storage-tabellen te verwijderen.

Dit onderwerp wordt beschreven hoe tooconfigure en Hallo AMS telemetrie in beslag nemen.

## <a name="configuring-telemetry"></a>Telemetrie configureren

U kunt telemetrie configureren op een niveau granulatie onderdeel. Er zijn twee detailniveaus 'Standaard' en 'Verbose'. Op dit moment kunnen beide niveaus Hallo retourneren dezelfde informatie. Het verdient aanbeveling toouse 'normaal. 

Hallo van de volgende onderwerpen tonen hoe tooenable telemetrie:

[Inschakelen van telemetrie met .NET](media-services-dotnet-telemetry.md) 

[Telemetrie met REST inschakelen](media-services-rest-telemetry.md)

## <a name="consuming-telemetry-information"></a>Telemetrie-informatie gebruiken

Telemetrie is tooan Azure Storage, Table geschreven in Hallo storage-account die u hebt opgegeven tijdens het configureren van telemetrie voor Hallo Media Services-account. Deze sectie beschrijft Hallo opslagtabellen voor Hallo metrische gegevens.

U kunt telemetrische gegevens in een van de volgende manieren hello gebruiken:

- Gegevens lezen rechtstreeks vanuit Azure Table Storage (bijvoorbeeld via Hallo opslag-SDK). Hallo beschrijving van telemetrie storage-tabellen, Zie Hallo **verbruikt telemetrie informatie** in [dit](https://msdn.microsoft.com/library/mt742089.aspx) onderwerp.

of

- Hallo-ondersteuning gebruiken in Hallo Media Services .NET SDK voor het lezen van gegevens van opslag, zoals beschreven in [dit](media-services-dotnet-telemetry.md) onderwerp. 


Hallo telemetrie schema hieronder beschreven is ontworpen toogive goede prestaties binnen de grenzen Hallo van Azure Table Storage:

- De gegevens zijn gepartitioneerd door account-ID en service-ID tooallow telemetrie van elke service toobe onafhankelijk worden opgevraagd.
- Partities bevatten Hallo datum toogive een redelijke bovengrens op Hallo partitiegrootte.
- Sleutels van de rij in de tijd omgekeerde volgorde tooallow Hallo meest recente telemetrie-items toobe gevraagd voor een bepaalde service.

Op die manier kunnen veel van de algemene query's toobe Hallo efficiënt:

- Parallelle, ongeacht het downloaden van gegevens voor afzonderlijke services.
- Bij het ophalen van alle gegevens voor een bepaalde service in een datumbereik.
- Bij het ophalen van de meest recente gegevens Hallo voor een service.

### <a name="telemetry-table-storage-output-schema"></a>Opslag telemetrie-uitvoer tabelschema

Telemetriegegevens wordt opgeslagen in een statistische functie in een tabel, 'TelemetryMetrics20160321' waar '20160321' datum van de tabel Hallo gemaakt. Telemetriesysteem maakt een afzonderlijke tabel voor elke nieuwe dag gebaseerd op 00:00 UTC. Hallo-tabel wordt gebruikt toostore terugkerende waarden opnemen, zoals bitrate binnen een bepaalde tijd, aantal verzonden bytes, enzovoort. 

Eigenschap|Waarde|Voorbeelden/opmerkingen
---|---|---
PartitionKey|{account-ID} _ {entiteit-ID}|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66 < br /<br/>account-ID is opgenomen in Hallo partitie sleutel toosimplify werkstromen waar meerdere accounts voor Media Services toohello schrijft Hallo hetzelfde opslagaccount.
RowKey|{seconden toomidnight} _ {willekeurige waarde}|01688_00199<br/><br/>Hallo rijsleutel begint met het aantal seconden toomidnight tooallow bovenste n achtige query's binnen een partitie Hallo. Zie voor meer informatie [dit](../cosmos-db/table-storage-design-guide.md#log-tail-pattern) artikel. 
tijdstempel|Datum/tijd|Tijdstempel van hello Azure-tabel 2016 auto-09-09T22:43:42.241Z
Type|Hallo type Hallo entiteit telemetriegegevens bieden|StreamingEndpoint-kanaal-archief<br/><br/>Gebeurtenistype is een string-waarde.
Naam|Hallo-naam van Hallo telemetrie gebeurtenis|ChannelHeartbeat/StreamingEndpointRequestLog
ObservedTime|Hallo tijd Hallo telemetrie gebeurtenis heeft plaatsgevonden (UTC)|2016-09-09T22:42:36.924Z<br/><br/>Hallo waargenomen tijd wordt geleverd door Hallo entiteit Hallo telemetrie te verzenden (bijvoorbeeld een kanaal). Er kunnen zich synchronisatieproblemen met de tussen onderdelen, zodat deze waarde is geschatte tijd
ServiceID|{service ID}|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
Entiteit-specifieke eigenschappen|Zoals gedefinieerd door het Hallo-gebeurtenis|StreamName: stream1, Bitrate 10123...<br/><br/>Hallo overige eigenschappen zijn gedefinieerd voor het betreffende gebeurtenistype Hallo. Azure Table-inhoud is sleutelwaarde-paren.  (dat wil zeggen, hebben verschillende rijen in de tabel Hallo verschillende sets eigenschappen).

### <a name="entity-specific-schema"></a>Entiteit-specifieke schema

Er zijn drie soorten specifieke telemetrische gegevens die elk gepusht Hello volgende frequentie:

- Streaming-eindpunten: elke 30 seconden
- Live kanalen: elke minuut
- Archief Live: elke minuut

**Streaming-eindpunt**

Eigenschap|Waarde|Voorbeelden
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
tijdstempel|tijdstempel|Tijdstempel van Azure Table 2016 auto-09-09T22:43:42.241Z
Type|Type|StreamingEndpoint
Naam|Naam|StreamingEndpointRequestLog
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|Service-ID|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
Hostnaam|Hostnaam van het Hallo-eindpunt|builddemoserver.Origin.mediaservices.Windows.NET
statusCode|Registreert HTTP-status|200
resultCode|Details van resultaat code|S_OK
requestCount|Totaal aantal aanvragen in Hallo aggregatie|3
BytesSent|Cumulatief aantal verzonden bytes|2987358
ServerLatency|Server gemiddelde latentie (inclusief opslag)|129
E2ELatency|Gemiddelde latentie van end-to-end|250

**Live kanaal**

Eigenschap|Waarde|Voorbeelden/opmerkingen
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
tijdstempel|tijdstempel|Tijdstempel van hello Azure-tabel 2016 auto-09-09T22:43:42.241Z
Type|Type|Kanaal
Naam|Naam|ChannelHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|Service-ID|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
TrackType|Type bijhouden audio-video/tekst|video en audio
TrackName|Naam van Hallo bijhouden|video/audio_1
Bitrate|Bitrate bijhouden|785000
CustomAttributes||   
IncomingBitrate|Werkelijke binnenkomende bitrate|784548
OverlapCount|Hallo overlap opnemen|0
DiscontinuityCount|Onderbreking voor bijhouden|0
LastTimestamp|Tijdstempel voor laatste opgenomen gegevens|1800488800
NonincreasingCount|Telling van fragmenten verwijderd vanwege tijdstempel toonon verhogen|2
UnalignedKeyFrames|Of er fragment(s) (in verschillende kwaliteitsniveaus ontvangen) waar sleutel frames niet uitgelijnd |True
UnalignedPresentationTime|Hiermee wordt aangegeven of er ontvangen fragment(s) (alle kwaliteit niveaus/nummers) waar presentatietijd is niet uitgelijnd|True
UnexpectedBitrate|Als berekend/werkelijke bitrate voor audio/video > 40.000 bps en IncomingBitrate bijhouden == True, of IncomingBitrate en actualBitrate met 50 verschillen % 0 |True
In orde|True is, als <br/>overlapCount, <br/>DiscontinuityCount, <br/>NonIncreasingCount, <br/>UnalignedKeyFrames, <br/>UnalignedPresentationTime, <br/>UnexpectedBitrate<br/> alle 0 zijn|True<br/><br/>In orde is een samengestelde functie die resulteert in false wanneer een van de volgende voorwaarden wachtstand Hallo:<br/><br/>-OverlapCount > 0<br/>-DiscontinuityCount > 0<br/>-NonincreasingCount > 0<br/>-UnalignedKeyFrames == True<br/>-UnalignedPresentationTime == True<br/>-UnexpectedBitrate == True

**Live archief**

Eigenschap|Waarde|Voorbeelden/opmerkingen
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
tijdstempel|tijdstempel|Tijdstempel van hello Azure-tabel 2016 auto-09-09T22:43:42.241Z
Type|Type|Archiveren
Naam|Naam|ArchiveHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|Service-ID|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
ManifestName|Programma-url|Asset-eb149703-ed0a-483c-91c4-e4066e72cce3/a0a5cfbf-71ec-4bd2-8c01-a92a2b38c9ba.ISM
TrackName|Naam van Hallo bijhouden|Audio_1
TrackType|Type Hallo bijhouden|Audio-video
CustomAttribute|Hexadecimale tekenreeks die onderscheidt van andere bijhouden met dezelfde naam en bitrate (meerdere camerahoek)|
Bitrate|Bitrate bijhouden|785000
In orde|True is, als FragmentDiscardedCount == 0 & & ArchiveAcquisitionError == False|True (deze twee waarden zijn niet aanwezig in de metriek Hallo maar ze zijn aanwezig in Hallo bron gebeurtenis)<br/><br/>In orde is een samengestelde functie die resulteert in false wanneer een van de volgende voorwaarden wachtstand Hallo:<br/><br/>-FragmentDiscardedCount > 0<br/>-ArchiveAcquisitionError == True

## <a name="general-qa"></a>Algemene Q & A

### <a name="how-tooconsume-metrics-data"></a>Hoe tooconsume metrische gegevens?

Metrische gegevens wordt opgeslagen als een reeks met Azure-tabellen in de storage-account van de klant Hallo. Deze gegevens kan worden gebruikt met Hallo hulpprogramma's te volgen:

- AMS SDK
- Microsoft Azure Storage Explorer (ondersteunt exportindeling toocomma gescheiden waarden en verwerkt in Excel)
- REST API

### <a name="how-toofind-average-bandwidth-consumption"></a>Hoe gemiddelde toofind bandbreedteverbruik?

de gemiddelde bandbreedteverbruik Hallo is Hallo gemiddelde van BytesSent gedurende een bepaalde tijd.

### <a name="how-toodefine-streaming-unit-count"></a>Hoe toodefine streaming-eenheid tellen?

aantal eenheden streaming Hallo kan worden gedefinieerd als Hallo piek doorvoer van streaming Hallo-service-eindpunten gedeeld door Hallo piek doorvoer van een streaming-eindpunt. Hallo piek bruikbare doorvoer van een streaming-eindpunt is 160 Mbps.
Stel bijvoorbeeld dat Hallo piek doorvoer van een klant-service is 40 MBps (Hallo maximumwaarde van BytesSent gedurende een bepaalde tijd). Aantal eenheden streaming Hallo is dan, gelijk too(40 MBps) * (8 bits/byte) /(160 Mbps) = 2 streaming-eenheden.

### <a name="how-toofind-average-requestssecond"></a>Hoe toofind gemiddelde aanvragen/seconde?

toofind hello gemiddelde aantal aanvragen/seconde compute Hallo kunt u het gemiddelde aantal aanvragen (RequestCount) gedurende een bepaalde tijd.

### <a name="how-toodefine-channel-health"></a>Hoe channel toodefine health?

Kanaal health kan worden gedefinieerd als een samengestelde Booleaanse functie die false als alle volgende voorwaarden Hallo houdt:

- OverlapCount > 0
- DiscontinuityCount > 0
- NonincreasingCount > 0
- UnalignedKeyFrames == True 
- UnalignedPresentationTime == True 
- UnexpectedBitrate == True


### <a name="how-toodetect-discontinuities"></a>Hoe wijzigingen toodetect?

toodetect onderbrekingen, alle gegevens van kanaal vinden waar DiscontinuityCount > 0. Hallo bijbehorende ObservedTime tijdstempel geeft Hallo tijden waarop Hallo wijzigingen heeft plaatsgevonden.

### <a name="how-toodetect-timestamp-overlaps"></a>Hoe toodetect tijdstempel overlapt?

toodetect tijdstempel overlappingen, alle gegevens van kanaal vinden waar OverlapCount > 0. Hallo bijbehorende ObservedTime tijdstempel geeft Hallo tijden op welke Hallo tijdstempel overlapt is opgetreden.

### <a name="how-toofind-streaming-request-failures-and-reasons"></a>Hoe toofind streaming aanvragen en de redenen?

mislukte aanvragen streaming van toofind en redenen, zien alle gegevens van Streaming-eindpunt waar ResultCode niet gelijk tooS_OK. Hallo bijbehorende StatusCode veld geeft Hallo waarom Hallo-aanvraag is mislukt.

### <a name="how-tooconsume-data-with-external-tools"></a>Hoe tooconsume gegevens met externe hulpprogramma's?

Telemetrische gegevens kunnen worden verwerkt en die gevisualiseerd Hello hulpprogramma's te volgen:

- PowerBI
- Application Insights
- Monitor voor Azure (voorheen schoenendoos)
- Dashboard voor AMS Live
- Azure-Portal (in behandeling release)

### <a name="how-toomanage-data-retention"></a>Hoe toomanage Gegevensretentie?

Hallo telemetriesysteem biedt geen bewaarperiode gegevensbeheer of automatische verwijdering van de oude records. U moet toomanage en dus oude records handmatig verwijderen uit Hallo opslag tabel. U kunt toostorage SDK raadplegen voor informatie over het toodo deze.

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
