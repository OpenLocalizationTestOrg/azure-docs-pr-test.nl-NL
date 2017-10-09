---
title: Capaciteitslimieten aaaSQL Data Warehouse | Microsoft Docs
description: Maximale waarden voor verbindingen, databases, tabellen en query's voor SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: e1eac122-baee-4200-a2ed-f38bfa0f67ce
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 8619cb997f0955d649d447cb8ca15cd742cc70b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-capacity-limits"></a>SQL Data Warehouse Capaciteitslimieten
Hallo bevatten volgende tabellen Hallo maximumwaarden toegestaan voor de verschillende onderdelen van Azure SQL Data Warehouse.

## <a name="workload-management"></a>Werklastbeheer
| Category | Beschrijving | Maximum |
|:--- |:--- |:--- |
| [Datawarehouse Units (DWU)][Data Warehouse Units (DWU)] |Maximale DWU voor een enkele SQL Data Warehouse |6000 |
| [Datawarehouse Units (DWU)][Data Warehouse Units (DWU)] |Maximale DWU voor één SQL server |6000 standaard<br/><br/> Elke SQL-server (bijvoorbeeld myserver.database.windows.net) heeft standaard een DTU-quotum van 45,000 waarmee up too6000 DWU. Dit quotum is gewoon een veiligheidsbeperking. U kunt uw quotum door verhogen [een ondersteuningsticket maken] [ creating a support ticket] en te selecteren *quotum* als Hallo aanvraagtype.  uw DTU moet, Vermenigvuldig toocalculate Hallo 7.5 Hallo totaal DWU die nodig zijn. U kunt uw huidige DTU-verbruik van SQL server-blade Hallo weergeven in Hallo-portal. Onderbroken en voortgezet databases meetellen voor Hallo DTU-quotum. |
| De verbinding met database |Gelijktijdige sessies actief |1024<br/><br/>We bieden ondersteuning voor een maximum van 1024 actieve verbindingen, die elk aanvragen tooa SQL Data Warehouse-database op Hallo kunt indienen hetzelfde moment. Houd er rekening mee dat er gelden beperkingen voor Hallo aantal query's die daadwerkelijk gelijktijdig kan worden uitgevoerd. Wanneer Hallo gelijktijdigheid limiet wordt overschreden, gaat Hallo aanvraag u naar een interne wachtrij waar er toobe verwerkt. |
| De verbinding met database |Maximale hoeveelheid geheugen voor voorbereide instructies |20 MB |
| [Beheer van de werkbelasting][Workload management] |Maximum aantal gelijktijdige query 's |32<br/><br/> SQL Data Warehouse kan standaard maximaal 32 gelijktijdige query's en wachtrijen resterende query's worden uitgevoerd.<br/><br/>Hallo gelijktijdigheid niveau kan afnemen wanneer gebruikers hogere bronklasse tooa worden toegewezen of wanneer de SQL Data Warehouse is geconfigureerd met een lage DWU. Sommige query's, zoals DMV-query's, zijn altijd toorun toegestaan. |
| [TempDB][Tempdb] |Maximale grootte van Tempdb |399 GB per DW100. Is daarom op DWU1000 Tempdb grootte too3.99 TB |

## <a name="database-objects"></a>database-objecten
| Category | Beschrijving | Maximum |
|:--- |:--- |:--- |
| Database |Maximale grootte |240 TB gecomprimeerd op schijf<br/><br/>Deze ruimte is onafhankelijk van tempdb- of logboekbestand ruimte en is daarom deze ruimte toegewezen toopermanent tabellen.  De geclusterde columnstore-compressie schatting op 5 X.  Deze compressie staat Hallo database toogrow tooapproximately 1 PB wanneer alle tabellen de geclusterde columnstore (Hallo standaard tabeltype worden). |
| Tabel |Maximale grootte |60 TB gecomprimeerd op schijf |
| Tabel |Tabellen per database |2 miljard |
| Tabel |Kolommen per tabel |1024 kolommen |
| Tabel |Bytes per kolom |Afhankelijk van de kolom [gegevenstype][data type].  De limiet is 8000 voor de gegevenstypen char, 4000 voor nvarchar of 2 GB voor de gegevenstypen MAX. |
| Tabel |Bytes per rij, gedefinieerde grootte |8060 bytes<br/><br/>Hallo aantal bytes per rij wordt berekend in Hallo dezelfde manier als het is voor SQL Server met pagina compressie. Zoals SQL Server ondersteunt SQL Data Warehouse overloop rij-opslag waarmee **kolommen met variabele lengte** toobe gepusht buiten een rij. Wanneer rijen met variabele lengte buiten de rij gepusht zijn, wordt alleen 24-byte-hoofdmap opgeslagen in de belangrijkste Hallo-record. Zie voor meer informatie, Hallo [overloop rij gegevens van meer dan 8 KB] [ Row-Overflow Data Exceeding 8 KB] MSDN-artikel. |
| Tabel |Partities per tabel |15,000<br/><br/>Voor hoge prestaties raden we aan Hallo nummer voor het minimaliseren van partities moet u terwijl toch op uw zakelijke vereisten. Als Hallo aantal partities in omvang toeneemt, Hallo-overhead voor Data Definition Language (DDL) en gegevens manipulatie taal (DML)-bewerkingen groeit en zorgt ervoor dat de tragere prestaties. |
| Tabel |Tekens per partitie grenswaarde. |4000 |
| Index |Niet-geclusterde indexen per tabel. |999<br/><br/>Geldt alleen voor toorowstore tabellen. |
| Index |Geclusterde indexen per tabel. |1<br><br/>Van toepassing tooboth rowstore en columnstore-tabellen. |
| Index |Indexsleutel. |900 bytes.<br/><br/>Geldt alleen toorowstore indexen.<br/><br/>Indexen voor kolommen met een maximale grootte van meer dan 900 bytes varchar kunnen worden gemaakt als de bestaande gegevens in de kolommen Hallo Hallo niet groter is dan 900 bytes wanneer Hallo index is gemaakt. Echter, later invoegen updatebewerkingen voor Hallo kolommen die Hallo totale grootte tooexceed 900 bytes veroorzaken, anders mislukt. |
| Index |De sleutelkolommen per index. |16<br/><br/>Geldt alleen toorowstore indexen. Geclusterde columnstore-indexen bevatten alle kolommen. |
| statistieken |Grootte van Hallo gecombineerd kolomwaarden. |900 bytes. |
| statistieken |Kolommen per object statistieken. |32 |
| statistieken |Statistieken maken voor kolommen per tabel. |30,000 |
| Opgeslagen procedures |Maximum aantal geneste niveaus. |8 |
| Weergave |Kolommen per weergeven |1,024 |

## <a name="loads"></a>Belasting
| Category | Beschrijving | Maximum |
|:--- |:--- |:--- |
| Polybase-belasting |MB per rij |1<br/><br/>Polybase belasting zijn beperkt tooloading rijen, beide kleiner dan 1MB en tooVARCHR(MAX), kan niet worden geladen NVARCHAR(MAX) of VARBINARY(MAX).<br/><br/> |

## <a name="queries"></a>Query's
| Category | Beschrijving | Maximum |
|:--- |:--- |:--- |
| Query’s uitvoeren |In de wachtrij query's voor gebruikerstabellen. |1000 |
| Query’s uitvoeren |Gelijktijdige query's over systeemweergaven. |100 |
| Query’s uitvoeren |In de wachtrij-query's in system-weergaven |1000 |
| Query’s uitvoeren |Maximum aantal parameters |2098 |
| Batch |Maximale grootte |65,536*4096 |
| Selecteer resultaten |Kolommen per rij |4096<br/><br/>U kunt nooit meer dan 4096 kolommen per rij in Hallo Selecteer resultaat hebben. Er is geen garantie dat u kunt altijd 4096 hebben. Als het queryplan Hallo een tijdelijke tabel vereist, Hallo 1024 kolommen per tabel maximale mogelijk van toepassing. |
| SELECTEER |Geneste subquery 's |32<br/><br/>U kunt nooit meer dan 32 geneste subquery's in een SELECT-instructie hebben. Er is geen garantie dat u kunt altijd 32 hebben. Een JOIN kan bijvoorbeeld een subquery in het queryplan Hallo introduceren. Hallo aantal subquery's kan ook worden beperkt door het beschikbare geheugen. |
| SELECTEER |Kolommen per JOIN |1024 kolommen<br/><br/>U kunt nooit meer dan 1024 kolommen hebben in Hallo JOIN. Er is geen garantie dat u kunt altijd 1024 hebben. Als Hallo JOIN plan een tijdelijke tabel met meer kolommen dan Hallo JOIN resultaat vereist, geldt Hallo 1024 limiet voor de tijdelijke tabel toohello. |
| SELECTEER |Aantal bytes per GROEPEREN op kolommen. |8060<br/><br/>Hallo-kolommen in de component GROUP BY Hallo kunnen maximaal 8060 bytes hebben. |
| SELECTEER |Aantal bytes per ORDER BY kolommen |8060 bytes.<br/><br/>Hallo-kolommen in component ORDER BY Hallo kunnen maximaal 8060 bytes hebben. |
| Id's en constanten per instructie |Het aantal waarnaar wordt verwezen id's en constanten. |65,535<br/><br/>SQL Data Warehouse beperkt Hallo aantal id's en constanten die kunnen worden opgenomen in één expressie van een query. Deze limiet is 65.535. Dit nummer resulteert in een SQL Server-fout 8632 overschrijdt. Zie voor meer informatie [interne fout: een expressie services limiet is bereikt][Internal error: An expression services limit has been reached]. |

## <a name="metadata"></a>Metagegevens
| Het systeemweergave | Maximumaantal rijen |
|:--- |:--- |
| sys.dm_pdw_component_health_alerts |10.000 |
| sys.dm_pdw_dms_cores |100 |
| sys.dm_pdw_dms_workers |Totaal aantal DMS werknemers voor de meest recente 1000 Hallo SQL-aanvragen. |
| sys.dm_pdw_errors |10.000 |
| sys.dm_pdw_exec_requests |10.000 |
| sys.dm_pdw_exec_sessions |10.000 |
| sys.dm_pdw_request_steps |Totaal aantal stappen voor het meest recente 1000 Hallo SQL aanvragen die zijn opgeslagen in sys.dm_pdw_exec_requests. |
| sys.dm_pdw_os_event_logs |10.000 |
| sys.dm_pdw_sql_requests |Hallo recentste 1000 SQL-aanvragen die zijn opgeslagen in sys.dm_pdw_exec_requests. |

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, [SQL Data Warehouse verwijzing overzicht][SQL Data Warehouse reference overview].

<!--Image references-->

<!--Article references-->
[Data Warehouse Units (DWU)]: ./sql-data-warehouse-overview-what-is.md
[SQL Data Warehouse reference overview]: ./sql-data-warehouse-overview-reference.md
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Tempdb]: ./sql-data-warehouse-tables-temporary.md
[data type]: ./sql-data-warehouse-tables-data-types.md
[creating a support ticket]: /sql-data-warehouse-get-started-create-support-ticket.md

<!--MSDN references-->
[Row-Overflow Data Exceeding 8 KB]: https://msdn.microsoft.com/library/ms186981.aspx
[Internal error: An expression services limit has been reached]: https://support.microsoft.com/kb/913050
