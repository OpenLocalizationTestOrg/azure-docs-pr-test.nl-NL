---
title: Monitor metrieken - ondersteunde metrische gegevens per resourcetype aaaAzure | Microsoft Docs
description: Lijst met metrische gegevens beschikbaar zijn voor elk resourcetype met Azure-Monitor.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/05/2017
ms.author: johnkem
ms.openlocfilehash: 66834238a1a4fcd7db1464cc023c18ee2563517a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="supported-metrics-with-azure-monitor"></a>Ondersteunde metrische gegevens met Azure-Monitor
Azure biedt verschillende manieren toointeract met metrische gegevens, inclusief voor deze grafieken in Hallo-portal, toegang hebben tot deze via Hallo REST-API of uitvoeren van deze query's met PowerShell of CLI. Hieronder volgt een volledige lijst met alle metrische gegevens op dit moment met metrische gegevens van de Monitor van het Azure-pipeline.

> [!NOTE]
> Het is mogelijk dat andere metrische gegevens beschikbaar in het Hallo-portal of met oudere API's. Deze lijst bevat alleen openbare preview metrische gegevens beschikbaar via Hallo openbare preview van metrische pijplijn van geconsolideerd hello Azure bewaken.
>
>

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|qpu_metric|QPU|Count|Gemiddelde|QPU. Bereik 0-100 voor S1, 0-200 voor S2 en 0-400 voor S4|
|memory_metric|Geheugen|Bytes|Gemiddelde|Geheugen. Bereik van 0-25 GB voor S1, 0-50 GB voor S2 en 0-100 GB voor S4|
|TotalConnectionRequests|Totaal aantal verbindingsaanvragen|Count|Gemiddelde|Totaal aantal verbindingsaanvragen. Dit zijn ontvangsten.|
|SuccessfullConnectionsPerSec|Geslaagde verbindingen Per seconde|CountPerSecond|Gemiddelde|Verhouding van geslaagde verbinding voltooiingen.|
|TotalConnectionFailures|Totaal aantal verbindingsfouten|Count|Gemiddelde|Totaal aantal mislukte verbindingspogingen.|
|CurrentUserSessions|Huidige gebruikerssessies|Count|Gemiddelde|Huidige aantal gebruikerssessies.|
|QueryPoolBusyThreads|Query groepen bezet Threads|Count|Gemiddelde|Het aantal bezet threads in Hallo query thread-groep.|
|CommandPoolJobQueueLength|Opdracht taak wachtrijlengte|Count|Gemiddelde|Het aantal taken in de wachtrij Hallo van Hallo opdracht thread-groep.|
|ProcessingPoolJobQueueLength|Wachtrijlengte taak verwerken|Count|Gemiddelde|Aantal niet-I/O-taken in de wachtrij Hallo Hallo verwerken thread-groep.|
|CurrentConnections|Verbinding: Actieve verbindingen|Count|Gemiddelde|Huidig aantal verbindingen van clients tot stand gebracht.|
|CleanerCurrentPrice|Geheugen: Schonere huidige prijs|Count|Gemiddelde|Huidige prijs van geheugen, byte-$/ tijd, genormaliseerde too1000.|
|CleanerMemoryShrinkable|Geheugen: Schonere geheugen verkleining|Bytes|Gemiddelde|De hoeveelheid geheugen in bytes, onderwerp toopurging door Hallo achtergrond schonere.|
|CleanerMemoryNonshrinkable|Geheugen: Schonere geheugen nonshrinkable|Bytes|Gemiddelde|De hoeveelheid geheugen in bytes, niet onderwerp toopurging door Hallo achtergrond schonere.|
|MemoryUsage|: Geheugengebruik geheugen|Bytes|Gemiddelde|Het geheugengebruik van Hallo serverproces zoals gebruikt bij het berekenen van de prijs van schonere geheugen. Gelijk toocounter Process\PrivateBytes plus Hallo grootte van de geheugentoewijzing gegevens, die is toegewezen of door Hallo xVelocity in het geheugen analyse-engine (VertiPaq) boven Hallo xVelocity engine geheugenlimiet toegewezen geheugen wordt genegeerd.|
|MemoryLimitHard|Geheugen: Geheugenlimiet harde|Bytes|Gemiddelde|Vaste geheugenlimiet uit het configuratiebestand.|
|MemoryLimitHigh|Geheugen: Geheugen beperken hoog|Bytes|Gemiddelde|Maximale geheugenlimiet van configuratiebestand.|
|MemoryLimitLow|Geheugen: Geheugen limiet laag|Bytes|Gemiddelde|Lage geheugenlimiet uit het configuratiebestand.|
|MemoryLimitVertiPaq|Geheugen: Geheugen limiet VertiPaq|Bytes|Gemiddelde|In het geheugen limiet uit het configuratiebestand.|
|Quota|Geheugen: quotum|Bytes|Gemiddelde|Huidige geheugenquotum, in bytes. Geheugenquotum wordt ook wel een grant of geheugen reservering voor geheugen.|
|QuotaBlocked|: Geheugenquotum geblokkeerd|Count|Gemiddelde|Huidig aantal quotum aanvragen die worden geblokkeerd totdat het andere Geheugenquota zijn vrijgegeven.|
|VertiPaqNonpaged|Geheugen: VertiPaq-wisselbaar geheugen:|Bytes|Gemiddelde|Bytes aan geheugen vergrendeld in de werkset Hallo voor gebruik door de engine in geheugen Hallo.|
|VertiPaqPaged|Geheugen: VertiPaq wisselbaar geheugen:|Bytes|Gemiddelde|Bytes wisselbaar geheugen in gebruik voor gegevens in het geheugen.|
|RowsReadPerSec|Verwerking: Rijen lezen per seconde|CountPerSecond|Gemiddelde|Het aantal rijen van alle relationele databases worden gelezen.|
|RowsConvertedPerSec|Verwerking: Rijen geconverteerd per seconde|CountPerSecond|Gemiddelde|Het aantal rijen wordt geconverteerd tijdens de verwerking.|
|RowsWrittenPerSec|Verwerking: Rijen geschreven per seconde|CountPerSecond|Gemiddelde|De frequentie van geschreven tijdens het verwerken van rijen.|
|CommandPoolBusyThreads|Threads: Opdracht groepen bezet threads|Count|Gemiddelde|Het aantal bezet threads in Hallo opdracht thread-groep.|
|CommandPoolIdleThreads|Threads: Opdracht groep niet-actieve threads|Count|Gemiddelde|Het aantal niet-actieve threads in Hallo opdracht thread-groep.|
|LongParsingBusyThreads|Threads: Long bezet threads parseren|Count|Gemiddelde|Het aantal bezet threads in Hallo lang bij het parseren van thread-groep.|
|LongParsingIdleThreads|Threads: Long bij het parseren van niet-actieve threads|Count|Gemiddelde|Het aantal niet-actieve threads in Hallo lang bij het parseren van thread-groep.|
|LongParsingJobQueueLength|Threads: Parseren lang taak wachtrijlengte|Count|Gemiddelde|Het aantal taken in de wachtrij Hallo Hallo lang bij het parseren van thread-groep.|
|ProcessingPoolBusyIOJobThreads|Threads: Groepen bezet i/o-taak threads verwerken|Count|Gemiddelde|Aantal actieve threads i/o-taken in Hallo verwerken thread-groep.|
|ProcessingPoolBusyNonIOThreads|Threads: Groep bezet niet-I/O-threads verwerkt|Count|Gemiddelde|Het aantal threads worden uitgevoerd van niet-I/O-taken in Hallo verwerken thread-groep.|
|ProcessingPoolIOJobQueueLength|Threads: Verwerken i/o-taak wachtrijlengte van toepassingen|Count|Gemiddelde|Het aantal i/o-taken in de wachtrij Hallo Hallo verwerken thread-groep.|
|ProcessingPoolIdleIOJobThreads|Threads: Groep niet-actieve i/o-taak threads verwerken|Count|Gemiddelde|Het aantal niet-actieve threads voor i/o-taken in Hallo verwerken thread-groep.|
|ProcessingPoolIdleNonIOThreads|Threads: Groep niet-actieve niet-I/O-threads verwerken|Count|Gemiddelde|Aantal niet-actieve threads in de verwerking van de threadgroep Hallo speciale toonon-I/O-taken.|
|QueryPoolIdleThreads|Threads: Query groep niet-actieve threads|Count|Gemiddelde|Het aantal niet-actieve threads voor i/o-taken in Hallo verwerken thread-groep.|
|QueryPoolJobQueueLength|Threads: Query groep taak wachtrij lengt|Count|Gemiddelde|Het aantal taken in de wachtrij Hallo van Hallo query thread-groep.|
|ShortParsingBusyThreads|Threads: Korte bezet threads parseren|Count|Gemiddelde|Het aantal bezet threads in Hallo korte bij het parseren van thread-groep.|
|ShortParsingIdleThreads|Threads: Korte bij het parseren van niet-actieve threads|Count|Gemiddelde|Het aantal niet-actieve threads in Hallo korte bij het parseren van thread-groep.|
|ShortParsingJobQueueLength|Threads: Korte wachtrijlengte taak parseren|Count|Gemiddelde|Het aantal taken in de wachtrij Hallo Hallo korte bij het parseren van thread-groep.|
|memory_thrashing_metric|Geheugen voorkomen|Procent|Gemiddelde|Gemiddelde geheugen thrashing.|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|TotalRequests|Totaal aantal Gateway aanvragen|Count|Totaal|Het aantal aanvragen van de gateway|
|SuccessfulRequests|De Gateway aanvragen|Count|Totaal|Aantal geslaagde gateway aanvragen|
|UnauthorizedRequests|Niet-geautoriseerde Gateway aanvragen|Count|Totaal|Het aantal niet-geautoriseerde gateway aanvragen|
|FailedRequests|Mislukte Gateway aanvragen|Count|Totaal|Aantal fouten in gateway aanvragen|
|OtherRequests|Andere Gateway aanvragen|Count|Totaal|Aantal andere gateway aanvragen|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|CoreCount|Speciale Core-telling|Count|Totaal|Totale aantal toegewezen kernen in Hallo batch-account|
|TotalNodeCount|Aantal toegewezen knooppunten|Count|Totaal|Totale aantal toegewezen knooppunten in Hallo batch-account|
|LowPriorityCoreCount|Core-telling LowPriority|Count|Totaal|Totaal aantal kernen in batch-account Hallo lage prioriteit|
|TotalLowPriorityNodeCount|Aantal knooppunten met lage prioriteit|Count|Totaal|Totale aantal knooppunten in de batch-account Hallo lage prioriteit|
|CreatingNodeCount|Aantal knooppunten maken|Count|Totaal|Het aantal knooppunten dat wordt gemaakt|
|StartingNodeCount|Aantal knooppunten wordt gestart|Count|Totaal|Het aantal knooppunten starten|
|WaitingForStartTaskNodeCount|Wachttijd voor begin taak aantal knooppunten|Count|Totaal|Het aantal knooppunten die wachten op Hallo taak starten toocomplete|
|StartTaskFailedNodeCount|Begintaak aantal knooppunten is mislukt|Count|Totaal|Het aantal knooppunten waar Hallo taak starten is mislukt|
|IdleNodeCount|Aantal niet-actieve knooppunten|Count|Totaal|Aantal niet-actieve knooppunten|
|OfflineNodeCount|Aantal offline knooppunten|Count|Totaal|Aantal knooppunten dat offline|
|RebootingNodeCount|Aantal knooppunten aan het opstarten|Count|Totaal|Het aantal knooppunten aan het opstarten|
|ReimagingNodeCount|Aantal knooppunten teruggezet|Count|Totaal|Het aantal knooppunten teruggezet|
|RunningNodeCount|Aantal actieve knooppunten|Count|Totaal|Aantal actieve knooppunten|
|LeavingPoolNodeCount|Aantal van de knooppunten groep verlaten|Count|Totaal|Het aantal knooppunten Hallo groep verlaten|
|UnusableNodeCount|Aantal onbruikbaar knooppunten|Count|Totaal|Aantal onbruikbaar knooppunten|
|PreemptedNodeCount|Aantal knooppunten afgebroken|Count|Totaal|Aantal afgebroken knooppunten|
|TaskStartEvent|Taak Start gebeurtenissen|Count|Totaal|Totaal aantal taken die zijn gestart|
|TaskCompleteEvent|Taak Complete-gebeurtenissen|Count|Totaal|Totale aantal taken die zijn voltooid|
|TaskFailEvent|Gebeurtenissen van taak mislukt|Count|Totaal|Totaal aantal taken die in een foutstatus voltooid|
|PoolCreateEvent|Gebeurtenissen van toepassingen maken|Count|Totaal|Totale aantal groepen die zijn gemaakt|
|PoolResizeStartEvent|Groep van toepassingen starten formaatwijzigingen|Count|Totaal|Totaal aantal toepassingen Hiermee wordt de grootte die zijn gestart|
|PoolResizeCompleteEvent|Groep formaat Complete-gebeurtenissen|Count|Totaal|Totaal aantal toepassingen Hiermee wordt de grootte die zijn voltooid|
|PoolDeleteStartEvent|Gebeurtenissen van toepassingen starten|Count|Totaal|Totaal aantal toepassingen verwijderen die zijn gestart|
|PoolDeleteCompleteEvent|Toepassingen verwijderen Complete-gebeurtenissen|Count|Totaal|Totaal aantal toepassingen verwijderen die zijn voltooid|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|connectedclients|Verbonden Clients|Count|Maximum||
|totalcommandsprocessed|Totaal aantal bewerkingen|Count|Totaal||
|cachehits|Treffers in cache|Count|Totaal||
|cachemisses|Cachemissers|Count|Totaal||
|getcommands|Opgehaald|Count|Totaal||
|setcommands|Sets|Count|Totaal||
|evictedkeys|Verwijderde sleutels|Count|Totaal||
|totalkeys|Totale aantal sleutels|Count|Maximum||
|expiredkeys|Verlopen sleutels|Count|Totaal||
|usedmemory|Gebruikt geheugen|Bytes|Maximum||
|usedmemoryRss|Gebruikt geheugen RSS|Bytes|Maximum||
|serverLoad|Belasting van de server|Procent|Maximum||
|cacheWrite|Cache schrijven|BytesPerSecond|Maximum||
|cacheRead|Cache lezen|BytesPerSecond|Maximum||
|percentProcessorTime|CPU|Procent|Maximum||
|connectedclients0|Verbonden Clients (Shard 0)|Count|Maximum||
|totalcommandsprocessed0|Totaal aantal bewerkingen (Shard 0)|Count|Totaal||
|cachehits0|Treffers in cache (Shard 0)|Count|Totaal||
|cachemisses0|Cachemissers (Shard 0)|Count|Totaal||
|getcommands0|Opgehaald (Shard 0)|Count|Totaal||
|setcommands0|Sets (Shard 0)|Count|Totaal||
|evictedkeys0|Verwijderde sleutels (Shard 0)|Count|Totaal||
|totalkeys0|Totale aantal sleutels (Shard 0)|Count|Maximum||
|expiredkeys0|Verlopen sleutels (Shard 0)|Count|Totaal||
|usedmemory0|Gebruikt geheugen (Shard 0)|Bytes|Maximum||
|usedmemoryRss0|Gebruikt geheugen RSS (Shard 0)|Bytes|Maximum||
|serverLoad0|Belasting van de server (Shard 0)|Procent|Maximum||
|cacheWrite0|Cache schrijven (Shard 0)|BytesPerSecond|Maximum||
|cacheRead0|Cache lezen (Shard 0)|BytesPerSecond|Maximum||
|percentProcessorTime0|CPU (Shard 0)|Procent|Maximum||
|connectedclients1|Verbonden Clients (Shard 1)|Count|Maximum||
|totalcommandsprocessed1|Totaal aantal bewerkingen (Shard 1)|Count|Totaal||
|cachehits1|Treffers in cache (Shard 1)|Count|Totaal||
|cachemisses1|Cachemissers (Shard 1)|Count|Totaal||
|getcommands1|Opgehaald (Shard 1)|Count|Totaal||
|setcommands1|Sets (Shard 1)|Count|Totaal||
|evictedkeys1|Verwijderde sleutels (Shard 1)|Count|Totaal||
|totalkeys1|Totale aantal sleutels (Shard 1)|Count|Maximum||
|expiredkeys1|Verlopen sleutels (Shard 1)|Count|Totaal||
|usedmemory1|Gebruikt geheugen (Shard 1)|Bytes|Maximum||
|usedmemoryRss1|Gebruikt geheugen RSS (Shard 1)|Bytes|Maximum||
|serverLoad1|Belasting van de server (Shard 1)|Procent|Maximum||
|cacheWrite1|Cache schrijven (Shard 1)|BytesPerSecond|Maximum||
|cacheRead1|Cache lezen (Shard 1)|BytesPerSecond|Maximum||
|percentProcessorTime1|CPU (Shard 1)|Procent|Maximum||
|connectedclients2|Verbonden Clients (Shard 2)|Count|Maximum||
|totalcommandsprocessed2|Totaal aantal bewerkingen (Shard 2)|Count|Totaal||
|cachehits2|Treffers in cache (Shard 2)|Count|Totaal||
|cachemisses2|Cachemissers (Shard 2)|Count|Totaal||
|getcommands2|Opgehaald (Shard 2)|Count|Totaal||
|setcommands2|Sets (Shard 2)|Count|Totaal||
|evictedkeys2|Verwijderde sleutels (Shard 2)|Count|Totaal||
|totalkeys2|Totale aantal sleutels (Shard 2)|Count|Maximum||
|expiredkeys2|Verlopen sleutels (Shard 2)|Count|Totaal||
|usedmemory2|Gebruikt geheugen (Shard 2)|Bytes|Maximum||
|usedmemoryRss2|Gebruikt geheugen RSS (Shard 2)|Bytes|Maximum||
|serverLoad2|Belasting van de server (Shard 2)|Procent|Maximum||
|cacheWrite2|Cache schrijven (Shard 2)|BytesPerSecond|Maximum||
|cacheRead2|Cache lezen (Shard 2)|BytesPerSecond|Maximum||
|percentProcessorTime2|CPU (Shard 2)|Procent|Maximum||
|connectedclients3|Verbonden Clients (Shard 3)|Count|Maximum||
|totalcommandsprocessed3|Totaal aantal bewerkingen (Shard 3)|Count|Totaal||
|cachehits3|Treffers in cache (Shard 3)|Count|Totaal||
|cachemisses3|Cachemissers (Shard 3)|Count|Totaal||
|getcommands3|Opgehaald (Shard 3)|Count|Totaal||
|setcommands3|Sets (Shard 3)|Count|Totaal||
|evictedkeys3|Verwijderde sleutels (Shard 3)|Count|Totaal||
|totalkeys3|Totale aantal sleutels (Shard 3)|Count|Maximum||
|expiredkeys3|Verlopen sleutels (Shard 3)|Count|Totaal||
|usedmemory3|Gebruikt geheugen (Shard 3)|Bytes|Maximum||
|usedmemoryRss3|Gebruikt geheugen RSS (Shard 3)|Bytes|Maximum||
|serverLoad3|Belasting van de server (Shard 3)|Procent|Maximum||
|cacheWrite3|Cache schrijven (Shard 3)|BytesPerSecond|Maximum||
|cacheRead3|Cache lezen (Shard 3)|BytesPerSecond|Maximum||
|percentProcessorTime3|CPU (Shard 3)|Procent|Maximum||
|connectedclients4|Verbonden Clients (Shard 4)|Count|Maximum||
|totalcommandsprocessed4|Totaal aantal bewerkingen (Shard 4)|Count|Totaal||
|cachehits4|Treffers in cache (Shard 4)|Count|Totaal||
|cachemisses4|Cachemissers (Shard 4)|Count|Totaal||
|getcommands4|Opgehaald (Shard 4)|Count|Totaal||
|setcommands4|Sets (Shard 4)|Count|Totaal||
|evictedkeys4|Verwijderde sleutels (Shard 4)|Count|Totaal||
|totalkeys4|Totale aantal sleutels (Shard 4)|Count|Maximum||
|expiredkeys4|Verlopen sleutels (Shard 4)|Count|Totaal||
|usedmemory4|Gebruikt geheugen (Shard 4)|Bytes|Maximum||
|usedmemoryRss4|Gebruikt geheugen RSS (Shard 4)|Bytes|Maximum||
|serverLoad4|Belasting van de server (Shard 4)|Procent|Maximum||
|cacheWrite4|Cache schrijven (Shard 4)|BytesPerSecond|Maximum||
|cacheRead4|Cache lezen (Shard 4)|BytesPerSecond|Maximum||
|percentProcessorTime4|CPU (Shard 4)|Procent|Maximum||
|connectedclients5|Verbonden Clients (Shard 5)|Count|Maximum||
|totalcommandsprocessed5|Totaal aantal bewerkingen (Shard 5)|Count|Totaal||
|cachehits5|Treffers in cache (Shard 5)|Count|Totaal||
|cachemisses5|Cachemissers (Shard 5)|Count|Totaal||
|getcommands5|Opgehaald (Shard 5)|Count|Totaal||
|setcommands5|Sets (Shard 5)|Count|Totaal||
|evictedkeys5|Verwijderde sleutels (Shard 5)|Count|Totaal||
|totalkeys5|Totale aantal sleutels (Shard 5)|Count|Maximum||
|expiredkeys5|Verlopen sleutels (Shard 5)|Count|Totaal||
|usedmemory5|Gebruikt geheugen (Shard 5)|Bytes|Maximum||
|usedmemoryRss5|Gebruikt geheugen RSS (Shard 5)|Bytes|Maximum||
|serverLoad5|Belasting van de server (Shard 5)|Procent|Maximum||
|cacheWrite5|Cache schrijven (Shard 5)|BytesPerSecond|Maximum||
|cacheRead5|Cache lezen (Shard 5)|BytesPerSecond|Maximum||
|percentProcessorTime5|CPU (Shard 5)|Procent|Maximum||
|connectedclients6|Verbonden Clients (Shard 6)|Count|Maximum||
|totalcommandsprocessed6|Totaal aantal bewerkingen (Shard 6)|Count|Totaal||
|cachehits6|Treffers in cache (Shard 6)|Count|Totaal||
|cachemisses6|Cachemissers (Shard 6)|Count|Totaal||
|getcommands6|Opgehaald (Shard 6)|Count|Totaal||
|setcommands6|Sets (Shard 6)|Count|Totaal||
|evictedkeys6|Verwijderde sleutels (Shard 6)|Count|Totaal||
|totalkeys6|Totale aantal sleutels (Shard 6)|Count|Maximum||
|expiredkeys6|Verlopen sleutels (Shard 6)|Count|Totaal||
|usedmemory6|Gebruikt geheugen (Shard 6)|Bytes|Maximum||
|usedmemoryRss6|Gebruikt geheugen RSS (Shard 6)|Bytes|Maximum||
|serverLoad6|Belasting van de server (Shard 6)|Procent|Maximum||
|cacheWrite6|Cache schrijven (Shard 6)|BytesPerSecond|Maximum||
|cacheRead6|Cache lezen (Shard 6)|BytesPerSecond|Maximum||
|percentProcessorTime6|CPU (Shard 6)|Procent|Maximum||
|connectedclients7|Verbonden Clients (Shard 7)|Count|Maximum||
|totalcommandsprocessed7|Totaal aantal bewerkingen (Shard 7)|Count|Totaal||
|cachehits7|Treffers in cache (Shard 7)|Count|Totaal||
|cachemisses7|Cachemissers (Shard 7)|Count|Totaal||
|getcommands7|Opgehaald (Shard 7)|Count|Totaal||
|setcommands7|Sets (Shard 7)|Count|Totaal||
|evictedkeys7|Verwijderde sleutels (Shard 7)|Count|Totaal||
|totalkeys7|Totale aantal sleutels (Shard 7)|Count|Maximum||
|expiredkeys7|Verlopen sleutels (Shard 7)|Count|Totaal||
|usedmemory7|Gebruikt geheugen (Shard 7)|Bytes|Maximum||
|usedmemoryRss7|Gebruikt geheugen RSS (Shard 7)|Bytes|Maximum||
|serverLoad7|Belasting van de server (Shard 7)|Procent|Maximum||
|cacheWrite7|Cache schrijven (Shard 7)|BytesPerSecond|Maximum||
|cacheRead7|Cache lezen (Shard 7)|BytesPerSecond|Maximum||
|percentProcessorTime7|CPU (Shard 7)|Procent|Maximum||
|connectedclients8|Verbonden Clients (Shard 8)|Count|Maximum||
|totalcommandsprocessed8|Totaal aantal bewerkingen (Shard 8)|Count|Totaal||
|cachehits8|Treffers in cache (Shard 8)|Count|Totaal||
|cachemisses8|Cachemissers (Shard 8)|Count|Totaal||
|getcommands8|(Shard 8) opgehaald|Count|Totaal||
|setcommands8|Sets (Shard 8)|Count|Totaal||
|evictedkeys8|Verwijderde sleutels (Shard 8)|Count|Totaal||
|totalkeys8|Totale aantal sleutels (Shard 8)|Count|Maximum||
|expiredkeys8|Verlopen sleutels (Shard 8)|Count|Totaal||
|usedmemory8|Gebruikt geheugen (Shard 8)|Bytes|Maximum||
|usedmemoryRss8|Gebruikt geheugen RSS (Shard 8)|Bytes|Maximum||
|serverLoad8|Belasting van de server (Shard 8)|Procent|Maximum||
|cacheWrite8|Cache schrijven (Shard 8)|BytesPerSecond|Maximum||
|cacheRead8|Cache lezen (Shard 8)|BytesPerSecond|Maximum||
|percentProcessorTime8|CPU (Shard 8)|Procent|Maximum||
|connectedclients9|Verbonden Clients (Shard 9)|Count|Maximum||
|totalcommandsprocessed9|Totaal aantal bewerkingen (Shard 9)|Count|Totaal||
|cachehits9|Treffers in cache (Shard 9)|Count|Totaal||
|cachemisses9|Cachemissers (Shard 9)|Count|Totaal||
|getcommands9|Opgehaald (Shard 9)|Count|Totaal||
|setcommands9|Sets (Shard 9)|Count|Totaal||
|evictedkeys9|Verwijderde sleutels (Shard 9)|Count|Totaal||
|totalkeys9|Totale aantal sleutels (Shard 9)|Count|Maximum||
|expiredkeys9|Verlopen sleutels (Shard 9)|Count|Totaal||
|usedmemory9|Gebruikt geheugen (Shard 9)|Bytes|Maximum||
|usedmemoryRss9|Gebruikt geheugen RSS (Shard 9)|Bytes|Maximum||
|serverLoad9|Belasting van de server (Shard 9)|Procent|Maximum||
|cacheWrite9|Cache schrijven (Shard 9)|BytesPerSecond|Maximum||
|cacheRead9|Cache lezen (Shard 9)|BytesPerSecond|Maximum||
|percentProcessorTime9|CPU (Shard 9)|Procent|Maximum||

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|TotalCalls|Totaal aantal aanroepen|Count|Totaal|Totaal aantal aanroepen.|
|SuccessfulCalls|Geslaagde aanroepen|Count|Totaal|Aantal geslaagde aanroepen.|
|TotalErrors|Totale aantal fouten|Count|Totaal|Totaal aantal aanroepen met foutmelding (HTTP-antwoord code 4xx of 5xx).|
|BlockedCalls|Geblokkeerde aanroepen|Count|Totaal|Het aantal aanroepen dat overschreden snelheid of quotumlimiet.|
|ServerErrors|Server-fouten|Count|Totaal|Het aantal aanroepen met interne servicefout (HTTP-antwoord code 5xx).|
|ClientErrors|Client-fouten|Count|Totaal|Het aantal aanroepen met de fout op de client (HTTP-antwoord code 4xx).|
|DataIn|Gegevens In|Bytes|Totaal|Grootte van binnenkomende gegevens in bytes.|
|DataOut|Gegevens uit|Bytes|Totaal|Grootte van uitgaande gegevens in bytes.|
|Latentie|Latentie|Milliseconden|Gemiddelde|Latentie in milliseconden.|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|CPU-percentage|CPU-percentage|Procent|Gemiddelde|Hallo percentage toegewezen compute-eenheden die zich momenteel in gebruik door Hallo horen|
|Het netwerk|Het netwerk|Bytes|Totaal|Hallo aantal bytes dat is ontvangen op alle netwerkinterfaces door Hallo horen (inkomend verkeer)|
|Uit het netwerk|Uit het netwerk|Bytes|Totaal|Hallo aantal bytes in alle netwerkinterfaces door Hallo horen (uitgaande verkeer)|
|Schijf lezen Bytes|Schijf lezen Bytes|Bytes|Totaal|Totaal aantal bytes lezen van de schijf tijdens de periode bewaking|
|Schijf schrijven Bytes|Schijf schrijven Bytes|Bytes|Totaal|Totaal aantal bytes geschreven toodisk tijdens de periode bewaking|
|Gelezen bewerkingen per seconde|Gelezen bewerkingen per seconde|CountPerSecond|Gemiddelde|Schijf lezen IOP 's|
|Geschreven bewerkingen per seconde|Geschreven bewerkingen per seconde|CountPerSecond|Gemiddelde|Schijf schrijven IOP 's|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|CPU-percentage|CPU-percentage|Procent|Gemiddelde|Hallo percentage toegewezen compute-eenheden die zich momenteel in gebruik door Hallo horen|
|Het netwerk|Het netwerk|Bytes|Totaal|Hallo aantal bytes dat is ontvangen op alle netwerkinterfaces door Hallo horen (inkomend verkeer)|
|Uit het netwerk|Uit het netwerk|Bytes|Totaal|Hallo aantal bytes in alle netwerkinterfaces door Hallo horen (uitgaande verkeer)|
|Schijf lezen Bytes|Schijf lezen Bytes|Bytes|Totaal|Totaal aantal bytes lezen van de schijf tijdens de periode bewaking|
|Schijf schrijven Bytes|Schijf schrijven Bytes|Bytes|Totaal|Totaal aantal bytes geschreven toodisk tijdens de periode bewaking|
|Gelezen bewerkingen per seconde|Gelezen bewerkingen per seconde|CountPerSecond|Gemiddelde|Schijf lezen IOP 's|
|Geschreven bewerkingen per seconde|Geschreven bewerkingen per seconde|CountPerSecond|Gemiddelde|Schijf schrijven IOP 's|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|CPU-percentage|CPU-percentage|Procent|Gemiddelde|Hallo percentage toegewezen compute-eenheden die zich momenteel in gebruik door Hallo horen|
|Het netwerk|Het netwerk|Bytes|Totaal|Hallo aantal bytes dat is ontvangen op alle netwerkinterfaces door Hallo horen (inkomend verkeer)|
|Uit het netwerk|Uit het netwerk|Bytes|Totaal|Hallo aantal bytes in alle netwerkinterfaces door Hallo horen (uitgaande verkeer)|
|Schijf lezen Bytes|Schijf lezen Bytes|Bytes|Totaal|Totaal aantal bytes lezen van de schijf tijdens de periode bewaking|
|Schijf schrijven Bytes|Schijf schrijven Bytes|Bytes|Totaal|Totaal aantal bytes geschreven toodisk tijdens de periode bewaking|
|Gelezen bewerkingen per seconde|Gelezen bewerkingen per seconde|CountPerSecond|Gemiddelde|Schijf lezen IOP 's|
|Geschreven bewerkingen per seconde|Geschreven bewerkingen per seconde|CountPerSecond|Gemiddelde|Schijf schrijven IOP 's|

## <a name="microsoftcustomerinsightshubs"></a>Microsoft.CustomerInsights/hubs

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|DCIApiCalls|Klant Insights API-aanroepen|Count|Totaal||
|DCIMappingImportOperationSuccessfulLines|Geslaagde bewerkingsregels toewijzing importeren|Count|Totaal||
|DCIMappingImportOperationFailedLines|Toewijzing van de importbewerking is mislukt voor regels|Count|Totaal||
|DCIMappingImportOperationTotalLines|Totaal aantal bewerkingsregels toewijzing importeren|Count|Totaal||
|DCIMappingImportOperationRuntimeInSeconds|Toewijzing importeren bewerking Runtime In seconden|Seconden|Totaal||
|DCIOutboundProfileExportSucceeded|Uitgaande profiel exporteren is geslaagd|Count|Totaal||
|DCIOutboundProfileExportFailed|Uitgaande profiel exporteren is mislukt|Count|Totaal||
|DCIOutboundProfileExportDuration|Duur van de uitgaande profiel exporteren|Seconden|Totaal||
|DCIOutboundKpiExportSucceeded|Uitgaande Kpi exporteren is voltooid|Count|Totaal||
|DCIOutboundKpiExportFailed|Uitgaande Kpi exporteren is mislukt|Count|Totaal||
|DCIOutboundKpiExportDuration|Duur van de uitgaande Kpi exporteren|Seconden|Totaal||
|DCIOutboundKpiExportStarted|Uitgaande Kpi Export gestart|Seconden|Totaal||
|DCIOutboundKpiRecordCount|Aantal uitgaande Kpi-records|Seconden|Totaal||
|DCIOutboundProfileExportCount|Telling van uitgaande profiel exporteren|Seconden|Totaal||
|DCIOutboundInitialProfileExportFailed|Uitgaande profiel exporteren is mislukt|Seconden|Totaal||
|DCIOutboundInitialProfileExportSucceeded|Uitgaande profiel exporteren is geslaagd|Seconden|Totaal||
|DCIOutboundInitialKpiExportFailed|Uitgaande initiële Kpi exporteren is mislukt|Seconden|Totaal||
|DCIOutboundInitialKpiExportSucceeded|Uitgaande initiële Kpi exporteren is voltooid|Seconden|Totaal||
|DCIOutboundInitialProfileExportDurationInSeconds|Uitgaande profiel exporteren duur In seconden|Seconden|Totaal||
|AdlaJobForStandardKpiFailed|De taak Adla voor standaard-Kpi is mislukt In seconden|Seconden|Totaal||
|AdlaJobForStandardKpiTimeOut|De taak Adla voor standaard Kpi time-out In seconden|Seconden|Totaal||
|AdlaJobForStandardKpiCompleted|De taak Adla voor standaard-Kpi voltooid In seconden|Seconden|Totaal||
|ImportASAValuesFailed|Importeren ASA waarden aantal is mislukt|Count|Totaal||
|ImportASAValuesSucceeded|Importeren ASA waarden aantal is voltooid|Count|Totaal||

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.DataLakeAnalytics/accounts

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|JobEndedSuccess|Mislukte taken|Count|Totaal|Het aantal mislukte taken.|
|JobEndedFailure|Mislukte taken|Count|Totaal|Het aantal mislukte taken.|
|JobEndedCancelled|Geannuleerde taken|Count|Totaal|Het aantal geannuleerde taken.|
|JobAUEndedSuccess|Geslaagde Australië tijd|Seconden|Totaal|Totale tijd Australië voor mislukte taken.|
|JobAUEndedFailure|Mislukte Australië tijd|Seconden|Totaal|Totale tijd Australië voor mislukte taken.|
|JobAUEndedCancelled|Geannuleerde Australië tijd|Seconden|Totaal|Totale tijd Australië voor geannuleerde taken.|

## <a name="microsoftdbformysqlservers"></a>Microsoft.DBforMySQL/servers

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|cpu_percent|CPU-percentage|Procent|Gemiddelde|CPU-percentage|
|compute_limit|COMPUTE eenheid limiet|Count|Gemiddelde|COMPUTE eenheid limiet|
|compute_consumption_percent|Percentage van de eenheid berekenen|Procent|Gemiddelde|Percentage van de eenheid berekenen|
|memory_percent|Percentage geheugen|Procent|Gemiddelde|Percentage geheugen|
|io_consumption_percent|I/o-percentage|Procent|Gemiddelde|I/o-percentage|
|storage_percent|Opslagpercentage|Procent|Gemiddelde|Opslagpercentage|
|storage_used|Gebruikte opslag|Bytes|Gemiddelde|Gebruikte opslag|
|storage_limit|Opslaglimiet bereikt|Bytes|Gemiddelde|Opslaglimiet bereikt|
|active_connections|Totaal aantal actieve verbindingen|Count|Gemiddelde|Totaal aantal actieve verbindingen|
|connections_failed|Totaal aantal mislukte verbindingen|Count|Gemiddelde|Totaal aantal mislukte verbindingen|

## <a name="microsoftdbforpostgresqlservers"></a>Microsoft.DBforPostgreSQL/servers

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|cpu_percent|CPU-percentage|Procent|Gemiddelde|CPU-percentage|
|compute_limit|COMPUTE eenheid limiet|Count|Gemiddelde|COMPUTE eenheid limiet|
|compute_consumption_percent|Percentage van de eenheid berekenen|Procent|Gemiddelde|Percentage van de eenheid berekenen|
|memory_percent|Percentage geheugen|Procent|Gemiddelde|Percentage geheugen|
|io_consumption_percent|I/o-percentage|Procent|Gemiddelde|I/o-percentage|
|storage_percent|Opslagpercentage|Procent|Gemiddelde|Opslagpercentage|
|storage_used|Gebruikte opslag|Bytes|Gemiddelde|Gebruikte opslag|
|storage_limit|Opslaglimiet bereikt|Bytes|Gemiddelde|Opslaglimiet bereikt|
|active_connections|Totaal aantal actieve verbindingen|Count|Gemiddelde|Totaal aantal actieve verbindingen|
|connections_failed|Totaal aantal mislukte verbindingen|Count|Gemiddelde|Totaal aantal mislukte verbindingen|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Telemetrie-bericht verzenden pogingen|Count|Totaal|Aantal pogingen tot toobe voor telemetrie voor apparaat-naar-cloud-berichten verzonden tooyour IoT-hub|
|d2c.telemetry.ingress.Success|Telemetrieberichten|Count|Totaal|Aantal voor apparaat-naar-cloud-telemetrieberichten verzonden tooyour IoT-hub|
|c2d.Commands.egress.complete.Success|Opdrachten voltooid|Count|Totaal|Aantal opdrachten voor cloud-naar-apparaat is voltooid door Hallo-apparaat|
|c2d.Commands.egress.Abandon.Success|Opdrachten afgebroken|Count|Totaal|Aantal afgebroken door Hallo apparaat opdrachten voor cloud-naar-apparaat|
|c2d.Commands.egress.Reject.Success|Opdrachten geweigerd|Count|Totaal|Aantal opdrachten voor cloud-naar-apparaat geweigerd door het Hallo-apparaat|
|devices.totalDevices|Totaal aantal apparaten|Count|Totaal|Aantal apparaten geregistreerd tooyour IoT-hub|
|devices.connectedDevices.allProtocol|Verbonden apparaten|Count|Totaal|Het aantal apparaten zijn verbonden tooyour IoT-hub|
|d2c.telemetry.egress.Success|Telemetrieberichten geleverd|Count|Totaal|Aantal keren dat berichten zijn geschreven tooendpoints (totaal)|
|d2c.telemetry.egress.Dropped|Verwijderde berichten|Count|Totaal|Aantal berichten dat is verwijderd omdat Hallo levering eindpunt dode|
|d2c.telemetry.egress.orphaned|Zwevende berichten|Count|Totaal|het aantal berichten die niet voldoen aan alle routes inclusief terugval route Hallo Hallo|
|d2c.telemetry.egress.Invalid|Ongeldige-berichten|Count|Totaal|Hallo aantal berichten niet verzonden vanwege tooincompatibility met Hallo-eindpunt|
|d2c.telemetry.egress.fallback|Berichten die overeenkomt met alternatieve voorwaarde|Count|Totaal|Aantal berichten dat is geschreven toohello terugval eindpunt|
|d2c.endpoints.egress.eventHubs|Berichten bezorgd tooEvent hubeindpunten|Count|Totaal|Aantal keren dat berichten is geschreven tooEvent-hubeindpunten zijn|
|d2c.endpoints.Latency.eventHubs|Bericht latentie voor Event Hub-eindpunten|milliseconden|Gemiddelde|Hallo gemiddelde latentie tussen bericht inkomend toohello iothub en inkomend bericht in een Event Hub-eindpunt, in milliseconden|
|d2c.endpoints.egress.serviceBusQueues|Berichten bezorgd tooService Bus-wachtrij-eindpunten|Count|Totaal|Aantal keren dat berichten is geschreven tooService Bus-wachtrij eindpunten zijn|
|d2c.endpoints.Latency.serviceBusQueues|Bericht latentie voor Service Bus-wachtrij-eindpunten|milliseconden|Gemiddelde|Hallo gemiddelde latentie tussen bericht inkomend toohello iothub en inkomend bericht in een Service Bus-wachtrij eindpunt, in milliseconden|
|d2c.endpoints.egress.serviceBusTopics|Berichten bezorgd tooService Bus-onderwerp eindpunten|Count|Totaal|Aantal keren dat berichten is geschreven tooService Bus-onderwerp eindpunten zijn|
|d2c.endpoints.Latency.serviceBusTopics|Bericht latentie voor Service Bus-onderwerp eindpunten|milliseconden|Gemiddelde|Hallo gemiddelde latentie tussen bericht inkomend toohello iothub en inkomend bericht in een eindpunt Service Bus-onderwerp in milliseconden|
|d2c.endpoints.egress.builtIn.events|Berichten bezorgd toohello ingebouwd eindpunt (berichten/gebeurtenissen)|Count|Totaal|Aantal keren dat berichten met succes geschreven toohello ingebouwd eindpunt (berichten/gebeurtenissen zijn)|
|d2c.endpoints.Latency.builtIn.events|Bericht latentie voor Hallo ingebouwd eindpunt (berichten/gebeurtenissen)|milliseconden|Gemiddelde|Hallo gemiddelde latentie tussen bericht inkomend toohello iothub en inkomend bericht in Hallo ingebouwd eindpunt (berichten/gebeurtenissen), in milliseconden |
|d2c.Twin.Read.Success|Geslaagde twin leesbewerkingen van apparaten|Count|Totaal|Hallo-telling van alle geslaagde apparaat geïnitieerde twin leest.|
|d2c.Twin.Read.failure|Twin leesbewerkingen van apparaten is mislukt|Count|Totaal|Hallo-telling van alle apparaat geïnitieerde twin leesbewerkingen mislukt.|
|d2c.Twin.Read.Size|De grootte van de antwoorden twin leesbewerkingen van apparaten|Bytes|Gemiddelde|Hallo gemiddelde, min en max van alle geslaagde apparaat geïnitieerde twin leest.|
|d2c.Twin.update.Success|Geslaagde twin updates van apparaten|Count|Totaal|Hallo-telling van alle geslaagde apparaat geïnitieerde twin updates.|
|d2c.Twin.update.failure|Twin updates van apparaten is mislukt|Count|Totaal|Hallo-telling van alle apparaat geïnitieerde twin updates mislukt.|
|d2c.Twin.update.Size|Grootte van de updates twin van apparaten|Bytes|Gemiddelde|gemiddelde Hello, minimale en maximale grootte van alle geslaagde apparaat geïnitieerde twin updates.|
|c2d.Methods.Success|Geslaagde directe methode aanroepen|Count|Totaal|Hallo-telling van alle geslaagde directe methodeaanroepen.|
|c2d.Methods.failure|Directe methode aanroepen is mislukt|Count|Totaal|Hallo-telling van alle directe methodeaanroepen mislukt.|
|c2d.Methods.requestSize|Aanvraaggrootte van directe methode aanroepen|Bytes|Gemiddelde|Hallo gemiddelde, min en max van alle geslaagde aanvragen voor directe methode.|
|c2d.Methods.responseSize|Reactiegrootte van directe methode aanroepen|Bytes|Gemiddelde|Hallo gemiddelde, min en max van alle geslaagde directe methode antwoorden.|
|c2d.Twin.Read.Success|Geslaagde twin leest uit back-end|Count|Totaal|Hallo-telling van alle geslaagde back-end-geïnitieerde twin leest.|
|c2d.Twin.Read.failure|Mislukte twin leest uit back-end|Count|Totaal|Hallo-telling van alle back-end-geïnitieerde twin leesbewerkingen mislukt.|
|c2d.Twin.Read.Size|De grootte van de antwoorden twin leesbewerkingen van back-end|Bytes|Gemiddelde|Hallo gemiddelde, min en max van alle geslaagde back-end-geïnitieerde twin leest.|
|c2d.Twin.update.Success|Geslaagde twin updates van de back-end|Count|Totaal|Hallo-telling van alle geslaagde back-end-geïnitieerde twin updates.|
|c2d.Twin.update.failure|Mislukte twin updates van de back-end|Count|Totaal|Hallo-telling van alle back-end-geïnitieerde twin updates mislukt.|
|c2d.Twin.update.Size|Grootte van twin updates van de back-end|Bytes|Gemiddelde|gemiddelde Hello, minimale en maximale grootte van alle geslaagde back-end-geïnitieerde twin updates.|
|twinQueries.success|Geslaagde twin query 's|Count|Totaal|Hallo-telling van alle geslaagde twin query's.|
|twinQueries.failure|Mislukte twin query 's|Count|Totaal|Hallo-telling van alle mislukte twin query's.|
|twinQueries.resultSize|Grootte van query's Twin|Bytes|Gemiddelde|Hallo gemiddelde, min en max van Hallo resultaat grootte van alle geslaagde twin query's.|
|jobs.createTwinUpdateJob.success|Geslaagde bewerkingen voor het maken van twin taken bijwerken|Count|Totaal|Hallo-telling van alle geslaagde twin update taken worden gemaakt.|
|jobs.createTwinUpdateJob.failure|Mislukte bewerkingen voor het maken van twin taken bijwerken|Count|Totaal|Hallo-telling van alle mislukte twin update taken worden gemaakt.|
|jobs.createDirectMethodJob.success|Geslaagde bewerkingen voor het maken van de methode aanroepen van taken|Count|Totaal|Hallo-telling van alle geslaagde directe methode aanroepen taken worden gemaakt.|
|jobs.createDirectMethodJob.failure|Mislukte bewerkingen voor het maken van de methode aanroepen van taken|Count|Totaal|Hallo-telling van alle maken van taken voor directe methode-aanroep is mislukt.|
|jobs.listJobs.success|Geslaagde aanroepen toolist taken|Count|Totaal|Hallo-telling van alle geslaagde aanroepen toolist taken.|
|jobs.listJobs.failure|Mislukte aanroepen toolist taken|Count|Totaal|Hallo-telling van alle mislukte aanroepen toolist taken.|
|jobs.cancelJob.success|Geslaagde taakannuleringen|Count|Totaal|Hallo-telling van alle geslaagde roept toocancel een taak.|
|jobs.cancelJob.failure|Mislukte taakannuleringen|Count|Totaal|Hallo-telling van alle mislukte aanroepen toocancel een taak.|
|jobs.queryJobs.success|Taak query 's|Count|Totaal|Hallo-telling van alle geslaagde aanroepen tooquery taken.|
|jobs.queryJobs.failure|Taak voert een query is mislukt|Count|Totaal|Hallo-telling van alle mislukte aanroepen tooquery taken.|
|jobs.completed|Voltooide taken|Count|Totaal|Hallo-telling van alle voltooide taken.|
|jobs.failed|Mislukte taken|Count|Totaal|Hallo-telling van alle mislukte taken.|
|d2c.telemetry.ingress.sendThrottle|Aantal bandbreedteregeling fouten|Count|Totaal|Aantal bandbreedteregeling fouten vanwege toodevice doorvoer vertragingen|
|dailyMessageQuotaUsed|Totaal aantal berichten dat is gebruikt|Count|Gemiddelde|Nummer van het totaal aantal berichten die op dit moment gebruikt|

## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|INREQS|Binnenkomende verzendaanvragen|Count|Totaal|Totaal aantal binnenkomende aanvragen voor een notification hub verzenden|
|SUCCREQ|Geslaagde aanvragen|Count|Totaal|Totaal aantal geslaagde aanvragen voor een naamruimte|
|FAILREQ|Mislukte aanvragen|Count|Totaal|Totaal aantal mislukte aanvragen voor een naamruimte|
|SVRBSY|Server bezet fouten|Count|Totaal|Totaal aantal server bezet fouten voor een naamruimte|
|INTERR|Interne serverfouten|Count|Totaal|Totaal aantal interne serverfouten voor een naamruimte|
|MISCERR|Andere fouten|Count|Totaal|Totaal aantal mislukte aanvragen voor een naamruimte|
|INMSGS|Binnenkomende berichten|Count|Totaal|Totaal aantal binnenkomende berichten voor een naamruimte|
|OUTMSGS|Uitgaande berichten|Count|Totaal|Totaal aantal uitgaande berichten voor een naamruimte|
|EHINMBS|Binnenkomende bytes|Bytes|Totaal|Event Hub inkomende bericht doorvoer voor een naamruimte|
|EHOUTMBS|Uitgaande bytes|Bytes|Totaal|Totaal aantal uitgaande berichten voor een naamruimte|
|EHABL|Berichten van de achterstand archiveren|Count|Totaal|Berichten van Event Hub archiveren achterstallige voor een naamruimte|
|EHAMSGS|Berichten archiveren|Count|Totaal|Event Hub gearchiveerde berichten in een naamruimte|
|EHAMBS|Archief bericht doorvoer|Bytes|Totaal|Event Hub gearchiveerd bericht doorvoer in een naamruimte|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|RunsStarted|Wordt uitgevoerd die zijn gestart|Count|Totaal|Aantal gestarte werkstroomuitvoeringen.|
|RunsCompleted|Voltooid wordt uitgevoerd|Count|Totaal|Aantal voltooide werkstroomuitvoeringen.|
|RunsSucceeded|Wordt uitgevoerd is voltooid|Count|Totaal|Aantal geslaagde werkstroomuitvoeringen.|
|RunsFailed|Wordt uitgevoerd, is mislukt|Count|Totaal|Aantal mislukte werkstroomuitvoeringen.|
|RunsCancelled|Wordt uitgevoerd, is geannuleerd|Count|Totaal|Aantal geannuleerde werkstroomuitvoeringen.|
|RunLatency|Latentie uitvoeren|Seconden|Gemiddelde|Latentie van voltooide werkstroomuitvoeringen.|
|RunSuccessLatency|Geslaagde latentie uitvoeren|Seconden|Gemiddelde|Latentie van geslaagde werkstroomuitvoeringen.|
|RunThrottledEvents|Beperkte gebeurtenissen uitvoeren|Count|Totaal|Aantal door werkstroomactie of trigger vertraagde gebeurtenissen.|
|RunFailurePercentage|Fout Percentage uitvoeren|Procent|Totaal|Percentage mislukte werkstroomuitvoeringen.|
|ActionsStarted|Acties die zijn gestart |Count|Totaal|Aantal gestarte werkstroomacties.|
|ActionsCompleted|Acties voltooid |Count|Totaal|Aantal voltooide werkstroomacties.|
|ActionsSucceeded|Acties is voltooid |Count|Totaal|Aantal geslaagde werkstroomacties.|
|ActionsFailed|Acties is mislukt|Count|Totaal|Aantal mislukte werkstroomacties.|
|ActionsSkipped|Acties die zijn overgeslagen |Count|Totaal|Aantal overgeslagen werkstroomacties.|
|ActionLatency|Actie latentie |Seconden|Gemiddelde|Latentie van voltooide werkstroomacties.|
|ActionSuccessLatency|Actie geslaagd latentie |Seconden|Gemiddelde|Latentie van geslaagde werkstroomacties.|
|ActionThrottledEvents|Actie beperkt gebeurtenissen|Count|Totaal|Aantal door werkstroomactie vertraagde gebeurtenissen.|
|TriggersStarted|Triggers is gestart |Count|Totaal|Aantal gestarte werkstroomtriggers.|
|TriggersCompleted|Triggers voltooid |Count|Totaal|Aantal voltooide werkstroomtriggers.|
|TriggersSucceeded|Triggers is voltooid |Count|Totaal|Aantal geslaagde werkstroomtriggers.|
|TriggersFailed|Triggers is mislukt |Count|Totaal|Aantal mislukte werkstroomtriggers.|
|TriggersSkipped|Triggers overgeslagen|Count|Totaal|Aantal overgeslagen werkstroomtriggers.|
|TriggersFired|Deze gebeurtenis wordt gestart triggers |Count|Totaal|Aantal geactiveerde werkstroomtriggers.|
|TriggerLatency|Trigger latentie |Seconden|Gemiddelde|Latentie van voltooide werkstroomtriggers.|
|TriggerFireLatency|Trigger Fire latentie |Seconden|Gemiddelde|Latentie van geactiveerde werkstroomtriggers.|
|TriggerSuccessLatency|Trigger geslaagd latentie |Seconden|Gemiddelde|Latentie van geslaagde werkstroomtriggers.|
|TriggerThrottledEvents|Trigger beperkt gebeurtenissen|Count|Totaal|Aantal door werkstroomtrigger vertraagde gebeurtenissen.|
|BillableActionExecutions|Factureerbare actie uitvoeringen|Count|Totaal|Aantal uitvoeringen van werkstroomacties dat wordt gefactureerd.|
|BillableTriggerExecutions|Factureerbare Trigger-uitvoeringen|Count|Totaal|Aantal uitvoeringen van werkstroomactiveringen dat wordt gefactureerd.|
|TotalBillableExecutions|Totale factureerbare uitvoeringen|Count|Totaal|Aantal werkstroomuitvoeringen dat wordt gefactureerd.|

## <a name="microsoftnetworkapplicationgateways"></a>Microsoft.Network/applicationGateways

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|Doorvoer|Doorvoer|BytesPerSecond|Gemiddelde||

## <a name="microsoftnetworkexpressroutecircuits"></a>Microsoft.Network/expressRouteCircuits

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|BytesIn|BytesIn|Count|Totaal||
|BytesOut|BytesOut|Count|Totaal||

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|Registration.all|Bewerking voor de registratie|Count|Totaal|Hallo-telling van alle bewerkingen van succesvolle registratie (query's aangemaakte-updates en verwijderingen). |
|Registration.Create|Registratie van de bewerkingen maken|Count|Totaal|Hallo-telling van alle succesvolle registratie aangemaakte.|
|Registration.update|Updatebewerkingen voor registratie|Count|Totaal|Hallo-telling van alle updates van succesvolle registratie.|
|Registration.Get|Registratie-leesbewerkingen|Count|Totaal|Hallo-telling van alle query's van succesvolle registratie.|
|Registration.Delete|Registratie-Delete-bewerkingen|Count|Totaal|Hallo-telling van alle succesvolle registratie verwijderingen.|
|binnenkomende|Binnenkomende berichten|Count|Totaal|Hallo-telling van alle geslaagde verzenden API-aanroepen. |
|Incoming.Scheduled|Geplande Pushmeldingen verzonden|Count|Totaal|Geplande Pushmeldingen geannuleerd|
|Incoming.Scheduled.Cancel|Geplande Pushmeldingen geannuleerd|Count|Totaal|Geplande Pushmeldingen geannuleerd|
|Scheduled.Pending|In behandeling zijnde geplande meldingen|Count|Totaal|In behandeling zijnde geplande meldingen|
|Installation.all|Beheerbewerkingen voor installatie|Count|Totaal|Beheerbewerkingen voor installatie|
|Installation.Get|Installatiebewerkingen ophalen|Count|Totaal|Installatiebewerkingen ophalen|
|Installation.upsert|Installatiebewerkingen maken of bijwerken|Count|Totaal|Installatiebewerkingen maken of bijwerken|
|Installation.patch|Installatiebewerkingen patch|Count|Totaal|Installatiebewerkingen patch|
|Installation.Delete|Verwijderen van installatiebewerkingen|Count|Totaal|Verwijderen van installatiebewerkingen|
|Outgoing.allpns.Success|Geslaagde meldingen|Count|Totaal|Hallo-telling van alle geslaagde meldingen.|
|Outgoing.allpns.invalidpayload|De nettolading van fouten|Count|Totaal|Hallo aantal pushes die is mislukt omdat hello PNS Ongeldige nettolading heeft een fout geretourneerd.|
|Outgoing.allpns.pnserror|Externe meldingen systeemfouten|Count|Totaal|Hallo aantal pushes die is mislukt omdat er een probleem bij het communiceren met de Hallo PNS (met uitzondering van verificatieproblemen).|
|Outgoing.allpns.channelerror|Kanaal-fouten|Count|Totaal|Hallo aantal pushes die is mislukt, omdat Hallo kanaal ongeldig niet is gekoppeld aan Hallo juist app beperkt of verlopen.|
|Outgoing.allpns.badorexpiredchannel|Fouten met slecht of verlopen kanaal|Count|Totaal|Hallo aantal pushes die is mislukt omdat Hallo kanaal/token/registratie-id in Hallo-registratie verlopen of ongeldig is.|
|Outgoing.WNS.Success|Geslaagde WNS-meldingen|Count|Totaal|Hallo-telling van alle geslaagde meldingen.|
|Outgoing.WNS.invalidcredentials|WNS autorisatie fouten (ongeldige aanmeldingsgegevens)|Count|Totaal|Hallo aantal pushes die is mislukt omdat Hallo PNS niet heeft geaccepteerd Hallo opgegeven referenties of referenties van Hallo worden geblokkeerd. (Windows Live wordt niet herkend Hallo referenties).|
|Outgoing.WNS.badchannel|Fout in het WNS onjuiste kanaal|Count|Totaal|Hallo aantal pushes die is mislukt omdat Hallo ChannelURI Hallo-registratie is niet herkend (WNS-status: 404 niet gevonden).|
|Outgoing.WNS.expiredchannel|WNS verlopen kanaal fout|Count|Totaal|Hallo aantal pushes die is mislukt omdat hello ChannelURI is verlopen (WNS-status: 410 Gone).|
|Outgoing.WNS.throttled|WNS beperkt meldingen|Count|Totaal|Hallo aantal pushes die is mislukt, omdat deze app is beperking van WNS (WNS-status: 406 niet geaccepteerd).|
|Outgoing.WNS.tokenproviderunreachable|WNS autorisatie fouten (onbereikbaar)|Count|Totaal|Windows Live is niet bereikbaar.|
|Outgoing.WNS.invalidtoken|WNS autorisatie fouten (ongeldige Token)|Count|Totaal|Hallo token opgegeven tooWNS is niet geldig (WNS-status: niet-gemachtigd 401).|
|Outgoing.WNS.wrongtoken|WNS autorisatie fouten (verkeerd Token)|Count|Totaal|Hallo token opgegeven tooWNS geldig is, maar voor een andere toepassing (WNS-status: 403-verboden). Dit kan gebeuren als Hallo ChannelURI Hallo-registratie gekoppeld aan een andere app is. Controleer dat Hallo client-app is gekoppeld aan Hallo dezelfde app met de referenties die zich op Hallo notification hub.|
|Outgoing.WNS.invalidnotificationformat|WNS ongeldig Meldingsresultaat indeling|Count|Totaal|Hallo-indeling van het Hallo-bericht is ongeldig (WNS-status: 400). Houd er rekening mee dat WNS alle ongeldige nettoladingen komt niet afwijzen.|
|Outgoing.WNS.invalidnotificationsize|Fout met ongeldige grootte van de WNS-melding|Count|Totaal|de nettolading van de meldingen Hallo is te groot (WNS-status: 413).|
|Outgoing.WNS.channelthrottled|WNS-kanaal beperkt|Count|Totaal|Hallo-bericht is verwijderd omdat Hallo ChannelURI Hallo-registratie is beperkt (WNS antwoordheader: X-WNS-NotificationStatus:channelThrottled).|
|Outgoing.WNS.channeldisconnected|WNS-kanaal is verbroken|Count|Totaal|Hallo-bericht is verwijderd omdat Hallo ChannelURI Hallo-registratie is beperkt (WNS antwoordheader: X-WNS-DeviceConnectionStatus: verbroken).|
|Outgoing.WNS.Dropped|WNS verwijderd meldingen|Count|Totaal|Hallo-bericht is verwijderd omdat Hallo ChannelURI Hallo-registratie is beperkt (X-WNS-NotificationStatus: uitgevallen, maar niet X-WNS-DeviceConnectionStatus: verbroken).|
|Outgoing.WNS.pnserror|WNS-fouten|Count|Totaal|De melding is niet bezorgd vanwege fouten bij het communiceren met WNS.|
|Outgoing.WNS.authenticationerror|WNS verificatiefouten|Count|Totaal|De melding niet worden bezorgd omdat er fouten zijn communicatie met Windows Live ongeldige referenties of verkeerd token.|
|Outgoing.apns.Success|Geslaagde meldingen APNS|Count|Totaal|Hallo-telling van alle geslaagde meldingen.|
|Outgoing.apns.invalidcredentials|APNS-autorisatie-fouten|Count|Totaal|Hallo aantal pushes die is mislukt omdat Hallo PNS niet heeft geaccepteerd Hallo opgegeven referenties of referenties van Hallo worden geblokkeerd.|
|Outgoing.apns.badchannel|Fout in het APNS onjuiste kanaal|Count|Totaal|Hallo aantal pushes die is mislukt omdat het Hallo-token is ongeldig (APNS-statuscode: 8).|
|Outgoing.apns.expiredchannel|APNS verlopen kanaal fout|Count|Totaal|Hallo aantal token die ongeldig zijn gemaakt door Hallo APNS feedback kanaal.|
|Outgoing.apns.invalidnotificationsize|Fout met ongeldige grootte van APNS-melding|Count|Totaal|Hallo aantal pushes die is mislukt omdat het Hallo-nettolading was te groot (APNS-statuscode: 7).|
|Outgoing.apns.pnserror|APNS-fouten|Count|Totaal|Hallo aantal pushes die is mislukt wegens fouten bij het communiceren met APNS.|
|Outgoing.GCM.Success|Geslaagde GCM-meldingen|Count|Totaal|Hallo-telling van alle geslaagde meldingen.|
|Outgoing.GCM.invalidcredentials|GCM autorisatie fouten (ongeldige aanmeldingsgegevens)|Count|Totaal|Hallo aantal pushes die is mislukt omdat Hallo PNS niet heeft geaccepteerd Hallo opgegeven referenties of referenties van Hallo worden geblokkeerd.|
|Outgoing.GCM.badchannel|Fout bij GCM onjuiste kanaal|Count|Totaal|Hallo aantal pushes die is mislukt omdat het Hallo-registratie in Hallo registratie-id is niet herkend (GCM resultaat: ongeldige registratie).|
|Outgoing.GCM.expiredchannel|GCM verlopen kanaal fout|Count|Totaal|Hallo aantal pushes die is mislukt omdat Hallo registrationId Hallo-registratie is verlopen (GCM resultaat: NotRegistered).|
|Outgoing.GCM.throttled|GCM beperkt meldingen|Count|Totaal|aantal pushes die is mislukt, omdat GCM deze app beperkt Hallo (GCM-statuscode: 501-599 ligt of resultaat: niet beschikbaar).|
|Outgoing.GCM.invalidnotificationformat|GCM ongeldig Meldingsresultaat indeling|Count|Totaal|aantal pushes die is mislukt omdat het Hallo-nettolading is niet juist geformatteerd Hallo (GCM resultaat: InvalidDataKey of InvalidTtl).|
|Outgoing.GCM.invalidnotificationsize|Fout met ongeldige grootte van GCM-melding|Count|Totaal|Hallo aantal pushes die is mislukt omdat het Hallo-nettolading was te groot (GCM resultaat: MessageTooBig).|
|Outgoing.GCM.wrongchannel|Fout bij GCM onjuiste kanaal|Count|Totaal|Hallo aantal pushes die Hallo registrationId Hallo-registratie is mislukt omdat de huidige app toohello die is gekoppeld (GCM resultaat: InvalidPackageName).|
|Outgoing.GCM.pnserror|GCM-fouten|Count|Totaal|Hallo aantal pushes die is mislukt wegens fouten bij het communiceren met GCM.|
|Outgoing.GCM.authenticationerror|GCM verificatiefouten|Count|Totaal|het aantal pushes die is mislukt omdat Hallo PNS niet heeft geaccepteerd Hallo opgegeven referenties Hallo referenties worden geblokkeerd of Hallo SenderId, is niet correct geconfigureerd in de app Hallo Hallo (GCM resultaat: MismatchedSenderId).|
|Outgoing.mpns.Success|Geslaagde MPNS-meldingen|Count|Totaal|Hallo-telling van alle geslaagde meldingen.|
|Outgoing.mpns.invalidcredentials|Ongeldige referenties MPNS|Count|Totaal|Hallo aantal pushes die is mislukt omdat Hallo PNS niet heeft geaccepteerd Hallo opgegeven referenties of referenties van Hallo worden geblokkeerd.|
|Outgoing.mpns.badchannel|Fout in het MPNS onjuiste kanaal|Count|Totaal|Hallo aantal pushes die is mislukt omdat Hallo ChannelURI Hallo-registratie is niet herkend (MPNS-status: 404 niet gevonden).|
|Outgoing.mpns.throttled|MPNS beperkt meldingen|Count|Totaal|het aantal pushes die is mislukt, omdat deze app is beperking van MPNS Hallo (WNS MPNS: 406 niet geaccepteerd).|
|Outgoing.mpns.invalidnotificationformat|MPNS ongeldig Meldingsresultaat indeling|Count|Totaal|Hallo aantal pushes die is mislukt omdat het Hallo-nettolading van het Hallo-bericht is te groot.|
|Outgoing.mpns.channeldisconnected|MPNS kanaal verbroken|Count|Totaal|Hallo aantal pushes die is mislukt omdat Hallo ChannelURI Hallo registratie van de verbinding is verbroken (MPNS-status: 412 niet gevonden).|
|Outgoing.mpns.Dropped|MPNS verwijderd meldingen|Count|Totaal|Hallo aantal pushes dat is verwijderd door de MPNS (MPNS antwoordheader: X NotificationStatus: QueueFull of Suppressed).|
|Outgoing.mpns.pnserror|MPNS-fouten|Count|Totaal|Hallo aantal pushes die is mislukt wegens fouten bij het communiceren met MPNS.|
|Outgoing.mpns.authenticationerror|Verificatiefouten MPNS|Count|Totaal|Hallo aantal pushes die is mislukt omdat Hallo PNS niet heeft geaccepteerd Hallo opgegeven referenties of referenties van Hallo worden geblokkeerd.|
|notificationhub.pushes|Alle uitgaande meldingen|Count|Totaal|Alle uitgaande meldingen van Hallo notification hub|
|Incoming.all.Requests|Alle inkomende aanvragen|Count|Totaal|Totaal aantal binnenkomende aanvragen voor een notification hub|
|Incoming.all.failedrequests|Alle binnenkomende mislukte aanvragen|Count|Totaal|Totaal aantal binnenkomende mislukte aanvragen voor een notification hub|

## <a name="microsoftpowerbidedicatedcapacities"></a>Microsoft.PowerBIDedicated/capacities

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|qpu_metric|QPU|Count|Gemiddelde|QPU. Bereik 0-100 voor S1, 0-200 voor S2 en 0-400 voor S4|
|memory_metric|Geheugen|Bytes|Gemiddelde|Geheugen. Bereik van 0-25 GB voor S1, 0-50 GB voor S2 en 0-100 GB voor S4|
|TotalConnectionRequests|Totaal aantal verbindingsaanvragen|Count|Gemiddelde|Totaal aantal verbindingsaanvragen. Dit zijn ontvangsten.|
|SuccessfullConnectionsPerSec|Geslaagde verbindingen Per seconde|CountPerSecond|Gemiddelde|Verhouding van geslaagde verbinding voltooiingen.|
|TotalConnectionFailures|Totaal aantal verbindingsfouten|Count|Gemiddelde|Totaal aantal mislukte verbindingspogingen.|
|CurrentUserSessions|Huidige gebruikerssessies|Count|Gemiddelde|Huidige aantal gebruikerssessies.|
|QueryPoolBusyThreads|Query groepen bezet Threads|Count|Gemiddelde|Het aantal bezet threads in Hallo query thread-groep.|
|CommandPoolJobQueueLength|Opdracht taak wachtrijlengte|Count|Gemiddelde|Het aantal taken in de wachtrij Hallo van Hallo opdracht thread-groep.|
|ProcessingPoolJobQueueLength|Wachtrijlengte taak verwerken|Count|Gemiddelde|Aantal niet-I/O-taken in de wachtrij Hallo Hallo verwerken thread-groep.|
|CurrentConnections|Verbinding: Actieve verbindingen|Count|Gemiddelde|Huidig aantal verbindingen van clients tot stand gebracht.|
|CleanerCurrentPrice|Geheugen: Schonere huidige prijs|Count|Gemiddelde|Huidige prijs van geheugen, byte-$/ tijd, genormaliseerde too1000.|
|CleanerMemoryShrinkable|Geheugen: Schonere geheugen verkleining|Bytes|Gemiddelde|De hoeveelheid geheugen in bytes, onderwerp toopurging door Hallo achtergrond schonere.|
|CleanerMemoryNonshrinkable|Geheugen: Schonere geheugen nonshrinkable|Bytes|Gemiddelde|De hoeveelheid geheugen in bytes, niet onderwerp toopurging door Hallo achtergrond schonere.|
|MemoryUsage|: Geheugengebruik geheugen|Bytes|Gemiddelde|Het geheugengebruik van Hallo serverproces zoals gebruikt bij het berekenen van de prijs van schonere geheugen. Gelijk toocounter Process\PrivateBytes plus Hallo grootte van de geheugentoewijzing gegevens, die is toegewezen of door Hallo xVelocity in het geheugen analyse-engine (VertiPaq) boven Hallo xVelocity engine geheugenlimiet toegewezen geheugen wordt genegeerd.|
|MemoryLimitHard|Geheugen: Geheugenlimiet harde|Bytes|Gemiddelde|Vaste geheugenlimiet uit het configuratiebestand.|
|MemoryLimitHigh|Geheugen: Geheugen beperken hoog|Bytes|Gemiddelde|Maximale geheugenlimiet van configuratiebestand.|
|MemoryLimitLow|Geheugen: Geheugen limiet laag|Bytes|Gemiddelde|Lage geheugenlimiet uit het configuratiebestand.|
|MemoryLimitVertiPaq|Geheugen: Geheugen limiet VertiPaq|Bytes|Gemiddelde|In het geheugen limiet uit het configuratiebestand.|
|Quota|Geheugen: quotum|Bytes|Gemiddelde|Huidige geheugenquotum, in bytes. Geheugenquotum wordt ook wel een grant of geheugen reservering voor geheugen.|
|QuotaBlocked|: Geheugenquotum geblokkeerd|Count|Gemiddelde|Huidig aantal quotum aanvragen die worden geblokkeerd totdat het andere Geheugenquota zijn vrijgegeven.|
|VertiPaqNonpaged|Geheugen: VertiPaq-wisselbaar geheugen:|Bytes|Gemiddelde|Bytes aan geheugen vergrendeld in de werkset Hallo voor gebruik door de engine in geheugen Hallo.|
|VertiPaqPaged|Geheugen: VertiPaq wisselbaar geheugen:|Bytes|Gemiddelde|Bytes wisselbaar geheugen in gebruik voor gegevens in het geheugen.|
|RowsReadPerSec|Verwerking: Rijen lezen per seconde|CountPerSecond|Gemiddelde|Het aantal rijen van alle relationele databases worden gelezen.|
|RowsConvertedPerSec|Verwerking: Rijen geconverteerd per seconde|CountPerSecond|Gemiddelde|Het aantal rijen wordt geconverteerd tijdens de verwerking.|
|RowsWrittenPerSec|Verwerking: Rijen geschreven per seconde|CountPerSecond|Gemiddelde|De frequentie van geschreven tijdens het verwerken van rijen.|
|CommandPoolBusyThreads|Threads: Opdracht groepen bezet threads|Count|Gemiddelde|Het aantal bezet threads in Hallo opdracht thread-groep.|
|CommandPoolIdleThreads|Threads: Opdracht groep niet-actieve threads|Count|Gemiddelde|Het aantal niet-actieve threads in Hallo opdracht thread-groep.|
|LongParsingBusyThreads|Threads: Long bezet threads parseren|Count|Gemiddelde|Het aantal bezet threads in Hallo lang bij het parseren van thread-groep.|
|LongParsingIdleThreads|Threads: Long bij het parseren van niet-actieve threads|Count|Gemiddelde|Het aantal niet-actieve threads in Hallo lang bij het parseren van thread-groep.|
|LongParsingJobQueueLength|Threads: Parseren lang taak wachtrijlengte|Count|Gemiddelde|Het aantal taken in de wachtrij Hallo Hallo lang bij het parseren van thread-groep.|
|ProcessingPoolBusyIOJobThreads|Threads: Groepen bezet i/o-taak threads verwerken|Count|Gemiddelde|Aantal actieve threads i/o-taken in Hallo verwerken thread-groep.|
|ProcessingPoolBusyNonIOThreads|Threads: Groep bezet niet-I/O-threads verwerkt|Count|Gemiddelde|Het aantal threads worden uitgevoerd van niet-I/O-taken in Hallo verwerken thread-groep.|
|ProcessingPoolIOJobQueueLength|Threads: Verwerken i/o-taak wachtrijlengte van toepassingen|Count|Gemiddelde|Het aantal i/o-taken in de wachtrij Hallo Hallo verwerken thread-groep.|
|ProcessingPoolIdleIOJobThreads|Threads: Groep niet-actieve i/o-taak threads verwerken|Count|Gemiddelde|Het aantal niet-actieve threads voor i/o-taken in Hallo verwerken thread-groep.|
|ProcessingPoolIdleNonIOThreads|Threads: Groep niet-actieve niet-I/O-threads verwerken|Count|Gemiddelde|Aantal niet-actieve threads in de verwerking van de threadgroep Hallo speciale toonon-I/O-taken.|
|QueryPoolIdleThreads|Threads: Query groep niet-actieve threads|Count|Gemiddelde|Het aantal niet-actieve threads voor i/o-taken in Hallo verwerken thread-groep.|
|QueryPoolJobQueueLength|Threads: Query groep taak wachtrij lengt|Count|Gemiddelde|Het aantal taken in de wachtrij Hallo van Hallo query thread-groep.|
|ShortParsingBusyThreads|Threads: Korte bezet threads parseren|Count|Gemiddelde|Het aantal bezet threads in Hallo korte bij het parseren van thread-groep.|
|ShortParsingIdleThreads|Threads: Korte bij het parseren van niet-actieve threads|Count|Gemiddelde|Het aantal niet-actieve threads in Hallo korte bij het parseren van thread-groep.|
|ShortParsingJobQueueLength|Threads: Korte wachtrijlengte taak parseren|Count|Gemiddelde|Het aantal taken in de wachtrij Hallo Hallo korte bij het parseren van thread-groep.|
|memory_thrashing_metric|Geheugen voorkomen|Procent|Gemiddelde|Gemiddelde geheugen thrashing.|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|SearchLatency|Latentie zoeken|Seconden|Gemiddelde|Gemiddelde zoeken latentie voor Hallo search-service|
|SearchQueriesPerSecond|Zoekquery's per seconde|CountPerSecond|Gemiddelde|Zoekquery's per seconde voor Hallo search-service|
|ThrottledSearchQueriesPercentage|Percentage van beperkte zoeken query 's|Procent|Gemiddelde|Percentage van de zoekquery's die zijn beperkt voor Hallo search-service|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|CPUXNS|CPU-gebruik per naamruimte|Procent|Maximum|Service bus premium naamruimte CPU-gebruik metrische gegevens|
|WSXNS|Geheugengebruik per naamruimte|Procent|Maximum|Service bus premium naamruimte geheugen gebruik metrische gegevens|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|cpu_percent|CPU-percentage|Procent|Gemiddelde|CPU-percentage|
|physical_data_read_percent|Gegevens-I/O-percentage|Procent|Gemiddelde|Gegevens-I/O-percentage|
|log_write_percent|Percentage van logboek-i/o|Procent|Gemiddelde|Percentage van logboek-i/o|
|dtu_consumption_percent|DTU-percentage|Procent|Gemiddelde|DTU-percentage|
|Opslag|Totale grootte|Bytes|Maximum|Totale grootte|
|connection_successful|Geslaagde verbindingen|Count|Totaal|Geslaagde verbindingen|
|connection_failed|Mislukte verbindingen|Count|Totaal|Mislukte verbindingen|
|blocked_by_firewall|Geblokkeerd door een Firewall|Count|Totaal|Geblokkeerd door een Firewall|
|impasse|Impassen|Count|Totaal|Impassen|
|storage_percent|Databaseomvangpercentage|Procent|Maximum|Databaseomvangpercentage|
|xtp_storage_percent|In het geheugen OLTP opslag procent|Procent|Gemiddelde|In het geheugen OLTP opslag procent|
|workers_percent|Percentage van de werknemers|Procent|Gemiddelde|Percentage van de werknemers|
|sessions_percent|Percentage van sessies|Procent|Gemiddelde|Percentage van sessies|
|dtu_limit|DTU limiet|Count|Gemiddelde|DTU limiet|
|dtu_used|DTU gebruikt|Count|Gemiddelde|DTU gebruikt|
|dwu_limit|DWU-limiet|Count|Maximum|DWU-limiet|
|dwu_consumption_percent|DWU-percentage|Procent|Maximum|DWU-percentage|
|dwu_used|DWU gebruikt|Count|Maximum|DWU gebruikt|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|cpu_percent|CPU-percentage|Procent|Gemiddelde|CPU-percentage|
|database_cpu_percent|CPU-percentage|Procent|Gemiddelde|CPU-percentage|
|physical_data_read_percent|Gegevens-I/O-percentage|Procent|Gemiddelde|Gegevens-I/O-percentage|
|database_physical_data_read_percent|Gegevens-I/O-percentage|Procent|Gemiddelde|Gegevens-I/O-percentage|
|log_write_percent|Percentage van logboek-i/o|Procent|Gemiddelde|Percentage van logboek-i/o|
|database_log_write_percent|Percentage van logboek-i/o|Procent|Gemiddelde|Percentage van logboek-i/o|
|dtu_consumption_percent|DTU-percentage|Procent|Gemiddelde|DTU-percentage|
|database_dtu_consumption_percent|DTU-percentage|Procent|Gemiddelde|DTU-percentage|
|storage_percent|Opslagpercentage|Procent|Gemiddelde|Opslagpercentage|
|workers_percent|Percentage van de werknemers|Procent|Gemiddelde|Percentage van de werknemers|
|database_workers_percent|Percentage van de werknemers|Procent|Gemiddelde|Percentage van de werknemers|
|sessions_percent|Percentage van sessies|Procent|Gemiddelde|Percentage van sessies|
|database_sessions_percent|Percentage van sessies|Procent|Gemiddelde|Percentage van sessies|
|eDTU_limit|limiet voor eDTU|Count|Gemiddelde|limiet voor eDTU|
|storage_limit|Opslaglimiet bereikt|Bytes|Gemiddelde|Opslaglimiet bereikt|
|eDTU_used|eDTU gebruikt|Count|Gemiddelde|eDTU gebruikt|
|storage_used|Gebruikte opslag|Bytes|Gemiddelde|Gebruikte opslag|
|database_storage_used|Gebruikte opslag|Bytes|Gemiddelde|Gebruikte opslag|
|xtp_storage_percent|In het geheugen OLTP opslag procent|Procent|Gemiddelde|In het geheugen OLTP opslag procent|

## <a name="microsoftsqlservers"></a>Microsoft.Sql/servers

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|dtu_consumption_percent|DTU-percentage|Procent|Gemiddelde|DTU-percentage|
|database_dtu_consumption_percent|DTU-percentage|Procent|Gemiddelde|DTU-percentage|
|storage_used|Gebruikte opslag|Bytes|Gemiddelde|Gebruikte opslag|
|database_storage_used|Gebruikte opslag|Bytes|Gemiddelde|Gebruikte opslag|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|ResourceUtilization|SU % gebruik|Procent|Maximum|SU % gebruik|
|InputEvents|Invoervelden|Count|Totaal|Invoervelden|
|InputEventBytes|Invoergebeurtenis Bytes|Bytes|Totaal|Invoergebeurtenis Bytes|
|LateInputEvents|Laat invoervelden|Count|Totaal|Laat invoervelden|
|OutputEvents|Uitvoergebeurtenissen|Count|Totaal|Uitvoergebeurtenissen|
|ConversionErrors|Conversie van fouten|Count|Totaal|Conversie van fouten|
|Fouten|Runtime-fouten|Count|Totaal|Runtime-fouten|
|DroppedOrAdjustedEvents|Gebeurtenissen in andere volgorde|Count|Totaal|Gebeurtenissen in andere volgorde|
|AMLCalloutRequests|Aanvragen van functie|Count|Totaal|Aanvragen van functie|
|AMLCalloutFailedRequests|Mislukte functie aanvragen|Count|Totaal|Mislukte functie aanvragen|
|AMLCalloutInputEvents|Gebeurtenissen voor de functie|Count|Totaal|Gebeurtenissen voor de functie|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|CpuPercentage|CPU-percentage|Procent|Gemiddelde|CPU-percentage|
|MemoryPercentage|Geheugenpercentage|Procent|Gemiddelde|Geheugenpercentage|
|DiskQueueLength|Wachtrijlengte voor schijf|Count|Totaal|Wachtrijlengte voor schijf|
|HttpQueueLength|HTTP-wachtrijlengte|Count|Totaal|HTTP-wachtrijlengte|
|BytesReceived|Gegevens In|Bytes|Totaal|Gegevens In|
|BytesSent|Gegevens uit|Bytes|Totaal|Gegevens uit|

## <a name="microsoftwebsites-excluding-functions"></a>Microsoft.Web/sites (met uitzondering van de functies)

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|CpuTime|CPU-tijd|Seconden|Totaal|CPU-tijd|
|Aanvragen|Aanvragen|Count|Totaal|Aanvragen|
|BytesReceived|Gegevens In|Bytes|Totaal|Gegevens In|
|BytesSent|Gegevens uit|Bytes|Totaal|Gegevens uit|
|Http101|HTTP 101|Count|Totaal|HTTP 101|
|Http2xx|HTTP-2xx|Count|Totaal|HTTP-2xx|
|Http3xx|HTTP-3xx|Count|Totaal|HTTP-3xx|
|Http401|401 HTTP|Count|Totaal|401 HTTP|
|Http403|HTTP-fout 403|Count|Totaal|HTTP-fout 403|
|Http404|HTTP 404|Count|Totaal|HTTP 404|
|Http406|HTTP 406|Count|Totaal|HTTP 406|
|Http4xx|HTTP-4xx|Count|Totaal|HTTP-4xx|
|Http5xx|HTTP-Server-fouten|Count|Totaal|HTTP-Server-fouten|
|MemoryWorkingSet|Geheugen-werkset|Bytes|Gemiddelde|Geheugen-werkset|
|AverageMemoryWorkingSet|Gemiddelde geheugen werkset|Bytes|Gemiddelde|Gemiddelde geheugen werkset|
|AverageResponseTime|Gemiddelde reactietijd|Seconden|Gemiddelde|Gemiddelde reactietijd|

## <a name="microsoftwebsites-functions"></a>Microsoft.Web/sites (functies)

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|BytesReceived|Gegevens In|Bytes|Totaal|Gegevens In|
|BytesSent|Gegevens uit|Bytes|Totaal|Gegevens uit|
|Http5xx|HTTP-Server-fouten|Count|Totaal|HTTP-Server-fouten|
|MemoryWorkingSet|Geheugen-werkset|Bytes|Gemiddelde|Geheugen-werkset|
|AverageMemoryWorkingSet|Gemiddelde geheugen werkset|Bytes|Gemiddelde|Gemiddelde geheugen werkset|
|FunctionExecutionUnits|Eenheden van de functie kan worden uitgevoerd|Count|Gemiddelde|Eenheden van de functie kan worden uitgevoerd|
|FunctionExecutionCount|Aantal keer uitgevoerd voor de functie|Count|Gemiddelde|Aantal keer uitgevoerd voor de functie|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|CpuTime|CPU-tijd|Seconden|Totaal|CPU-tijd|
|Aanvragen|Aanvragen|Count|Totaal|Aanvragen|
|BytesReceived|Gegevens In|Bytes|Totaal|Gegevens In|
|BytesSent|Gegevens uit|Bytes|Totaal|Gegevens uit|
|Http101|HTTP 101|Count|Totaal|HTTP 101|
|Http2xx|HTTP-2xx|Count|Totaal|HTTP-2xx|
|Http3xx|HTTP-3xx|Count|Totaal|HTTP-3xx|
|Http401|401 HTTP|Count|Totaal|401 HTTP|
|Http403|HTTP-fout 403|Count|Totaal|HTTP-fout 403|
|Http404|HTTP 404|Count|Totaal|HTTP 404|
|Http406|HTTP 406|Count|Totaal|HTTP 406|
|Http4xx|HTTP-4xx|Count|Totaal|HTTP-4xx|
|Http5xx|HTTP-Server-fouten|Count|Totaal|HTTP-Server-fouten|
|MemoryWorkingSet|Geheugen-werkset|Bytes|Gemiddelde|Geheugen-werkset|
|AverageMemoryWorkingSet|Gemiddelde geheugen werkset|Bytes|Gemiddelde|Gemiddelde geheugen werkset|
|AverageResponseTime|Gemiddelde reactietijd|Seconden|Gemiddelde|Gemiddelde reactietijd|
|FunctionExecutionUnits|Eenheden van de functie kan worden uitgevoerd|Count|Gemiddelde|Eenheden van de functie kan worden uitgevoerd|
|FunctionExecutionCount|Aantal keer uitgevoerd voor de functie|Count|Gemiddelde|Aantal keer uitgevoerd voor de functie|

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over metrische gegevens in Azure-Monitor](monitoring-overview-metrics.md)
* [Waarschuwingen maken op de metrische gegevens](insights-receive-alert-notifications.md)
* [Metrische gegevens toostorage, Event Hub of Log Analytics exporteren](monitoring-overview-of-diagnostic-logs.md)
