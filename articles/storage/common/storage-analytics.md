---
title: aaaUse logboeken en metrische gegevens van Azure Storage Analytics toocollect | Microsoft Docs
description: Storage Analytics kunt u tootrack metrische gegevens voor alle storage-services en toocollect logboeken voor de opslag van Blob, wachtrijen en tabellen.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7894993b-ca42-4125-8f17-8f6dfe3dca76
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: aba1a236cb69fa2e60bcb8fda5d34841e36e379a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storage-analytics"></a>Storage Analytics

Met Azure Storage Analytics wordt logboekregistratie uitgevoerd en kunnen metrische gegevens voor een opslagaccount worden geleverd. U kunt deze gegevensaanvragen tootrace gebruiken, trends in gebruik analyseren en vaststellen van problemen met uw opslagaccount.

toouse Storage Analytics, moet u deze inschakelen voor elke service wilt u afzonderlijk toomonitor. U kunt deze inschakelen via Hallo [Azure Portal](https://portal.azure.com). Zie voor meer informatie [bewaken van een opslagaccount in Azure Portal Hallo](storage-monitor-storage-account.md). U kunt ook Opslaganalyse programmatisch via Hallo REST-API of clientbibliotheek Hallo inschakelen. Gebruik Hallo [Blob-Service-eigenschappen ophalen](https://msdn.microsoft.com/library/hh452239.aspx), [wachtrij Service-eigenschappen ophalen](https://msdn.microsoft.com/library/hh452243.aspx), [tabel Service-eigenschappen ophalen](https://msdn.microsoft.com/library/hh452238.aspx), en [ophalen File Service Properties](https://msdn.microsoft.com/library/mt427369.aspx) operations tooenable Storage Analytics voor elke service.

Hallo wordt geaggregeerde gegevens opgeslagen in een bekende blob (voor logboekregistratie) en in een bekende tabellen (voor metrische gegevens) waartoe toegang kunnen worden verkregen met behulp van Hallo Blob-service en service API's van de tabel.

Storage Analytics heeft een limiet van 20 TB op Hallo en de hoeveelheid opgeslagen gegevens die onafhankelijk is van de totale Hallo-limiet voor uw opslagaccount. Zie voor meer informatie over facturering en bewaarbeleid voor gegevens [Storage Analytics en facturering](https://msdn.microsoft.com/library/hh360997.aspx). Zie voor meer informatie over opslagaccountlimieten [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).

Voor een gedetailleerde richtlijnen voor het gebruik van Storage Analytics en andere hulpprogramma's voor tooidentify, diagnose, en problemen met Azure Storage, Zie [Monitor, vaststellen en oplossen van Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="about-storage-analytics-logging"></a>Over Opslaganalyse logboekregistratie
Storage Analytics registreert gedetailleerde informatie over geslaagde en mislukte aanvragen tooa storage-service. Deze informatie kan worden gebruikt toomonitor afzonderlijke aanvragen en toodiagnose problemen met de storage-service. Aanvragen worden geregistreerd op basis van best-effort.

Logboekvermeldingen worden alleen gemaakt als opslag service-activiteit is. Bijvoorbeeld, als een opslagaccount activiteit in de Blob-service, maar niet in de tabel- of -services heeft, wordt alleen de logboeken die betrekking hebben toohello Blob-service gemaakt.

Storage Analytics logboekregistratie is niet beschikbaar voor Azure File storage.

### <a name="logging-authenticated-requests"></a>Geverifieerde logboekregistratieaanvragen
Hallo volgende typen geverifieerde aanvragen worden geregistreerd:

* Geslaagde aanvragen.
* Mislukte aanvragen, met inbegrip van de time-outperiode, beperking, netwerk, autorisatie en andere fouten.
* -Aanvragen via een Shared Access Signature (SAS), met inbegrip van mislukte en geslaagde aanvragen.
* Aanvragen tooanalytics gegevens.

Aanvragen door Storage Analytics zelf, zoals logboekbestanden worden gemaakt of verwijderd, worden niet geregistreerd. Een volledige lijst met Hallo geregistreerd gegevens wordt beschreven in Hallo [Storage Analytics geregistreerde bewerkingen en statusberichten](https://msdn.microsoft.com/library/hh343260.aspx) en [Storage Analytics logboekindeling](https://msdn.microsoft.com/library/hh343259.aspx) onderwerpen.

### <a name="logging-anonymous-requests"></a>Logboekregistratie anonieme aanvragen
Hallo volgende typen anonieme aanvragen worden geregistreerd:

* Geslaagde aanvragen.
* Serverfouten.
* Time-outfouten voor zowel client als server.
* Mislukte aanvragen ophalen met foutcode 304 (niet gewijzigd).

Alle andere mislukte anonieme aanvragen worden niet geregistreerd. Een volledige lijst met Hallo geregistreerd gegevens wordt beschreven in Hallo [Storage Analytics geregistreerde bewerkingen en statusberichten](https://msdn.microsoft.com/library/hh343260.aspx) en [Storage Analytics logboekindeling](https://msdn.microsoft.com/library/hh343259.aspx) onderwerpen.

### <a name="how-logs-are-stored"></a>Hoe logboeken worden opgeslagen
Alle logboeken worden opgeslagen in een blok-blobs in een container met de naam $logs die automatisch wordt gemaakt wanneer Opslaganalyse is ingeschakeld voor een opslagaccount. Hallo $logs container bevindt zich in Hallo blob-naamruimte van Hallo storage-account, bijvoorbeeld: `http://<accountname>.blob.core.windows.net/$logs`. Deze container kan niet worden verwijderd zodra Opslaganalyse is ingeschakeld, maar de inhoud ervan kunnen worden verwijderd.

> [!NOTE]
> Hallo $logs container wordt niet weergegeven wanneer een container met de bewerking wordt uitgevoerd, zoals Hallo [ListContainers](https://msdn.microsoft.com/library/azure/dd179352.aspx) methode. Deze moet rechtstreeks worden geopend. Bijvoorbeeld, kunt u Hallo [ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx) methode tooaccess Hallo blobs in Hallo `$logs` container.
> Als aanvragen worden geregistreerd, gaat u Storage Analytics tussenliggende resultaten als blokken uploaden. Storage Analytics wordt regelmatig deze blokken doorvoeren en zodat ze beschikbaar zijn als een blob.
> 
> 

Dubbele records kunnen bestaan voor logboeken gemaakt in Hallo hetzelfde uur. U kunt bepalen of een record een duplicaat is door het controleren van Hallo **RequestId** en **bewerking** getal.

### <a name="log-naming-conventions"></a>Meld u naamgevingsregels
Elk logboek wordt geschreven in de volgende indeling Hallo.

    <service-name>/YYYY/MM/DD/hhmm/<counter>.log

Hallo bevat onderstaande tabel alle kenmerken in Hallo logboeknaam.

| Kenmerk | Beschrijving |
| --- | --- |
| < Servicenaam > |Hallo-naam van Hallo storage-service. Bijvoorbeeld: blob, table of wachtrij. |
| JJJJ |jaar van vier cijfers Hallo voor Hallo logboek. Bijvoorbeeld: 2011. |
| MM |Hallo jaartallen met twee maand voor Hallo logboek. Bijvoorbeeld: 07. |
| DD |Hallo jaartallen met twee maand voor Hallo logboek. Bijvoorbeeld: 07. |
| hh |Hallo jaartallen met twee uur die aangeeft vanaf uur voor Hallo Hallo zich aanmeldt, in 24-uurs UTC-notatie. Bijvoorbeeld: 18. |
| mm |Hallo jaartallen met twee getal dat aangeeft Hallo minuut voor Hallo Logboeken wordt gestart. Deze waarde wordt niet ondersteund in de huidige versie Hallo van Storage Analytics wordt, waarbij de waarde altijd 00. |
| <counter> |Een op nul gebaseerde item met zes cijfers die Hallo aantal logboek BLOB's gegenereerd voor de opslagservice Hallo in een uur periode aangeeft. Deze teller begint bij 000000. Bijvoorbeeld: 000001. |

Hallo Hieronder volgt een compleet codevoorbeeld logboeknaam die de eerdere voorbeelden Hallo combineert.

    blob/2011/07/31/1800/000001.log

Hallo Hieronder volgt een voorbeeld van een URI die gebruikt tooaccess Hallo vorige logboek worden kan.

    https://<accountname>.blob.core.windows.net/$logs/blob/2011/07/31/1800/000001.log

Wanneer een aanvraag van de opslag is geregistreerd, correleert Hallo resulterende logboeknaam toohello uur waarop Hallo aangevraagd bewerking is voltooid. Bijvoorbeeld, als een GetBlob-aanvraag is voltooid op 18:30 uur op 7/31/2011 zouden Hallo logboek worden geschreven met Hallo voorvoegsel te volgen:`blob/2011/07/31/1800/`

### <a name="log-metadata"></a>Metagegevens van het logboek
Alle logboekbestanden blobs worden opgeslagen met metagegevens dat gebruikte tooidentify kan worden welke logboekregistratie gegevens Hallo blob bevat. Hallo volgende tabel beschrijft elke metagegevenskenmerk.

| Kenmerk | Beschrijving |
| --- | --- |
| LogType |Hierin wordt beschreven of Hallo logboek bevat informatie over tooread, schrijven of delete-bewerkingen. Deze waarde kan een type of een combinatie van alle drie, gescheiden door komma's bevatten. Voorbeeld 1: schrijven; Voorbeeld 2: lezen, schrijven; Voorbeeld 3: lezen, schrijven, verwijderen. |
| StartTime |Hallo vroegste tijdstip van een vermelding in het Hallo-logboek in de vorm Hallo van jjjj-MM-ssZ. Bijvoorbeeld: 2011-07-31T18:21:46Z. |
| Eindtijd |Hallo laatste tijd van een vermelding in het Hallo-logboek in de vorm Hallo van jjjj-MM-ssZ. Bijvoorbeeld: 2011-07-31T18:22:09Z. |
| LogVersion |Hallo-versie van Hallo-logboekindeling. Hallo alleen ondersteunde waarde is momenteel 1.0. |

Hallo volgende lijst worden weergegeven met behulp van de eerdere voorbeelden Hallo compleet codevoorbeeld-metagegevens.

* LogType = schrijven
* StartTime = 2011-07-31T18:21:46Z
* EndTime = 2011-07-31T18:22:09Z
* LogVersion = 1.0

### <a name="accessing-logging-data"></a>Toegang tot gegevens voor logboekregistratie
Alle gegevens in Hallo `$logs` container toegankelijk via API's voor Hallo Blob-service, inclusief Hallo .NET API's geleverd door hello Azure bibliotheek beheerd. Hallo beheerder opslagaccount kunt lezen en verwijderen van Logboeken, maar niet maken of bijwerken van deze. Zowel de Hallo-logboek metagegevens en de naam van het logboek kunnen worden gebruikt bij het opvragen van een logboek. Het is mogelijk voor een bepaalde tijd logboeken tooappear volgorde, maar Hallo metagegevens bevat altijd Hallo timespan van logboekvermeldingen in een logboek. Daarom kunt u een combinatie van logboeknamen en metagegevens bij het zoeken naar een bepaald logboek.

## <a name="about-storage-analytics-metrics"></a>Over Opslaganalyse metrische gegevens
Storage Analytics metrische gegevens die samengevoegde statistieken en capaciteit transactiegegevens over aanvragen tooa storage-service zijn kunnen worden opgeslagen. Transacties worden gerapporteerd zowel niveau van de bewerking Hallo API, evenals op niveau van de opslag van Hallo en capaciteit op Hallo opslag serviceniveau wordt gerapporteerd. Metrische gegevens kunt gebruikte tooanalyze service opslaggebruik, vaststellen van problemen met aanvragen tegen Hallo storage-service en tooimprove Hallo prestaties van toepassingen die gebruikmaken van een service.

toouse Storage Analytics, moet u deze inschakelen voor elke service wilt u afzonderlijk toomonitor. U kunt deze inschakelen via Hallo [Azure Portal](https://portal.azure.com). Zie voor meer informatie [bewaken van een opslagaccount in Azure Portal Hallo](storage-monitor-storage-account.md). U kunt ook Opslaganalyse programmatisch via Hallo REST-API of clientbibliotheek Hallo inschakelen. Gebruik Hallo **Service-eigenschappen ophalen** operations tooenable Storage Analytics voor elke service.

### <a name="transaction-metrics"></a>Transactie metrische gegevens
Een set krachtige gegevens wordt vastgelegd bij per uur of minuut intervallen voor elke service-opslag en API heeft bewerking aangevraagd, met inbegrip van inkomend en uitgaand, beschikbaarheid, fouten, en gecategoriseerd percentages van de aanvraag. Ziet u een volledige lijst met Hallo transactiedetails Hallo [Storage Analytics metrische gegevens tabelschema](https://msdn.microsoft.com/library/hh343264.aspx) onderwerp.

Transactiegegevens wordt vastgelegd op twee niveaus – Hallo serviceniveau en Hallo API bewerking. Op Hallo van serviceniveau aangevraagd statistieken samenvatten alle API-bewerkingen worden geschreven tooa Tabelentiteit elk uur zelfs als er geen aanvragen toohello service zijn aangebracht. Statistieken worden alleen geschreven tooan entiteit op Hallo API bewerking niveau als Hallo-bewerking is aangevraagd binnen dat uur.

Als u bijvoorbeeld een **GetBlob** bewerking in de Blob-service, metrische gegevens Storage Analytics wordt Hallo aanvraag melden en deze opnemen in Hallo geaggregeerd gegevens voor beide Blob-service, evenals Hallo Hallo **GetBlob** bewerking. Echter, als er geen **GetBlob** bewerking wordt aangevraagd tijdens Hallo uur, een entiteit wordt niet geschreven toohello `$MetricsTransactionsBlob` voor de bewerking.

Transactie metrische gegevens worden geregistreerd voor aanvragen van gebruikers en aanvragen door Opslaganalyse zelf. Bijvoorbeeld worden aanvragen door Opslaganalyse toowrite logboeken en tabelentiteiten geregistreerd. Zie voor meer informatie over hoe deze aanvragen worden gefactureerd [Storage Analytics en facturering](https://msdn.microsoft.com/library/hh360997.aspx).

### <a name="capacity-metrics"></a>Capaciteit metrische gegevens
> [!NOTE]
> Capaciteitsmetrieken zijn momenteel alleen beschikbaar voor Hallo Blob-service. Capaciteit metrische gegevens voor Hallo tabel-service en Queue-service zijn beschikbaar in toekomstige versies van Storage Analytics.
> 
> 

Capaciteit gegevens worden dagelijks geregistreerd voor een opslagaccount Blob-service en twee tabelentiteiten worden geschreven. Één entiteit voorziet in statistieken voor gebruikersgegevens en andere Hallo voorziet in statistieken over Hallo `$logs` blob-container door Storage Analytics gebruikt. Hallo `$MetricsCapacityBlob` tabel bevat Hallo statistieken te volgen:

* **Capaciteit**: Hallo en de hoeveelheid opslagruimte die wordt gebruikt door Hallo storage-account van Blob-service, in bytes.
* **ContainerCount**: Hallo aantal blobcontainers in Hallo storage-account van Blob-service.
* **ObjectCount**: Hallo aantal toegewezen en niet-doorgevoerde blok of pagina blobs in de Blob-service Hallo van het opslagaccount.

Zie voor meer informatie over Hallo capaciteitsmetrieken [Storage Analytics metrische gegevens tabelschema](https://msdn.microsoft.com/library/hh343264.aspx).

### <a name="how-metrics-are-stored"></a>Hoe metrische gegevens worden opgeslagen
Alle metrische gegevens voor elk van de opslagservices hello wordt opgeslagen in drie tabellen die zijn gereserveerd voor de service: één tabel voor transactie-informatie, één tabel voor de minuut transactie-informatie en een andere tabel voor informatie over capaciteit. Transactie en minuut transactie-informatie bestaat uit gegevens aanvraag en -antwoord en capaciteitsgegevens van gebruiksgegevens van de opslag bestaat. Metrische gegevens uur, minuut meetgegevens en capaciteit voor een opslagaccount Blob-service kunnen worden benaderd in tabellen die worden genoemd, zoals beschreven in de volgende tabel Hallo.

| Niveau van de metrische gegevens | Namen van tabellen | Ondersteunde versies |
| --- | --- | --- |
| Elk uur maatstaven voor primaire locatie |$MetricsTransactionsBlob <br/>$MetricsTransactionsTable <br/> $MetricsTransactionsQueue |Versies voorafgaande too2013-08-15 alleen. Deze namen worden wel nog steeds ondersteund, het raadzaam dat u overschakelt naar toousing Hallo tabellen die hieronder worden vermeld. |
| Elk uur maatstaven voor primaire locatie |$MetricsHourPrimaryTransactionsBlob <br/>$MetricsHourPrimaryTransactionsTable <br/>$MetricsHourPrimaryTransactionsQueue |Alle versies, inclusief 2013-08-15. |
| Minuut maatstaven voor primaire locatie |$MetricsMinutePrimaryTransactionsBlob <br/>$MetricsMinutePrimaryTransactionsTable <br/>$MetricsMinutePrimaryTransactionsQueue |Alle versies, inclusief 2013-08-15. |
| Elk uur maatstaven voor secundaire locatie |$MetricsHourSecondaryTransactionsBlob <br/>$MetricsHourSecondaryTransactionsTable <br/>$MetricsHourSecondaryTransactionsQueue |Alle versies, inclusief 2013-08-15. Leestoegang geografisch redundante replicatie moet zijn ingeschakeld. |
| Minuut maatstaven voor secundaire locatie |$MetricsMinuteSecondaryTransactionsBlob <br/>$MetricsMinuteSecondaryTransactionsTable <br/>$MetricsMinuteSecondaryTransactionsQueue |Alle versies, inclusief 2013-08-15. Leestoegang geografisch redundante replicatie moet zijn ingeschakeld. |
| Capaciteit (alleen voor Blob-service) |$MetricsCapacityBlob |Alle versies, inclusief 2013-08-15. |

Deze tabellen worden automatisch gemaakt wanneer Opslaganalyse is ingeschakeld voor een opslagaccount. Ze toegankelijk zijn via het Hallo-naamruimte van Hallo storage-account, bijvoorbeeld:`https://<accountname>.table.core.windows.net/Tables("$MetricsTransactionsBlob")`

### <a name="accessing-metrics-data"></a>Toegang tot metrische gegevens
Alle gegevens in Hallo metrische gegevens tabellen zijn toegankelijk via API's voor Hallo tabel-service, inclusief Hallo .NET API's geleverd door hello Azure bibliotheek beheerd. Hallo beheerder opslagaccount kunt lezen en verwijderen van de tabelentiteiten, maar niet maken of bijwerken ze.

## <a name="billing-for-storage-analytics"></a>Facturering voor Storage Analytics
Alle gegevens van de metrische gegevens worden geschreven door Hallo services van een opslagaccount. Elke schrijfbewerking uitgevoerd door Opslaganalyse is als gevolg hiervan factureerbare. Hallo en de hoeveelheid opslagruimte die wordt gebruikt door metrische gegevens is bovendien ook factureerbare.

Hallo van de volgende activiteiten uitgevoerd door Storage Analytics zijn factureerbare:

* Aanvragen toocreate blobs voor logboekregistratie. 
* Aanvragen toocreate tabelentiteiten voor de metrische gegevens.

Als u een bewaarbeleid voor gegevens hebt geconfigureerd, u worden niet in rekening gebracht voor verwijdertransacties wanneer Opslaganalyse oude logboekregistratie en metrische gegevens worden verwijderd. Er zijn echter verwijdertransacties van een client factureerbare. Zie voor meer informatie over het bewaarbeleid [instellen van een bewaarbeleid voor gegevens van Storage Analytics](https://msdn.microsoft.com/library/azure/hh343263.aspx).

### <a name="understanding-billable-requests"></a>Understanding factureerbare aanvragen
Elk verzoek opslagservice tooan-account is factureerbare of niet-factureerbaar. Storage Analytics registreert elke afzonderlijke aanvraag tooa-service, inclusief een statusbericht dat aangeeft hoe Hallo-aanvraag is verwerkt. Storage Analytics worden op dezelfde manier metrische gegevens voor een service- en het Hallo-API-bewerkingen van die service, inclusief Hallo percentages en de telling van bepaalde statusberichten die zijn opgeslagen. Samen kunt deze functies u uw factureerbare aanvragen analyseren, verbeteringen op uw toepassing maken en analyseren van problemen met aanvragen tooyour services. Zie voor meer informatie over facturering [wat Azure Storage facturering - bandbreedte, transacties en capaciteit](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx).

Wanneer u Opslaganalyse gegevens bekijkt, kunt u Hallo tabellen in Hallo [Storage Analytics geregistreerde bewerkingen en statusberichten](https://msdn.microsoft.com/library/azure/hh343260.aspx) onderwerp toodetermine wat aanvragen factureerbare zijn. Vervolgens kunt u uw logboeken en metrische gegevens toohello status berichten toosee vergelijken als in rekening voor een bepaald verzoek gebracht zijn. U kunt ook Hallo tabellen in Hallo vorige onderwerp tooinvestigate beschikbaarheid gebruiken voor een service-opslag of afzonderlijke API-bewerking.

## <a name="next-steps"></a>Volgende stappen
### <a name="setting-up-storage-analytics"></a>Instellen van Storage Analytics
* [Een opslagaccount in hello Azure Portal controleren](storage-monitor-storage-account.md)
* [Inschakelen en configureren van opslag Analytics](https://msdn.microsoft.com/library/hh360996.aspx)

### <a name="storage-analytics-logging"></a>Storage Analytics logboekregistratie
* [Over Storage Analytics logboekregistratie](https://msdn.microsoft.com/library/hh343262.aspx)
* [Storage Analytics logboekindeling](https://msdn.microsoft.com/library/hh343259.aspx)
* [Storage Analytics geregistreerde bewerkingen en statusberichten](https://msdn.microsoft.com/library/hh343260.aspx)

### <a name="storage-analytics-metrics"></a>Metrische gegevens Storage Analytics
* [Over metrische gegevens Storage Analytics](https://msdn.microsoft.com/library/hh343258.aspx)
* [Storage Analytics metrische gegevens tabelschema](https://msdn.microsoft.com/library/hh343264.aspx)
* [Storage Analytics geregistreerde bewerkingen en statusberichten](https://msdn.microsoft.com/library/hh343260.aspx)  

