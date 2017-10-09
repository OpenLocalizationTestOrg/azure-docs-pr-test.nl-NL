---
title: aaaData typen richtlijnen - Azure SQL Data Warehouse | Microsoft Docs
description: Aanbevelingen toodefine gegevenstypen die zijn compatibel met SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: a2f7a394feb73d273b25101735b00eb12db2b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a>Richtlijnen voor het definiëren van gegevenstypen voor tabellen in SQL Data Warehouse
Gebruik deze aanbevelingen toodefine tabel-gegevenstypen die compatibel met SQL Data Warehouse zijn. Bovendien verbetert toocompatibility, voor het minimaliseren van Hallo grootte van gegevenstypen met de prestaties van query's.

SQL Data Warehouse ondersteunt Hallo meest gebruikte gegevenstypen. Zie voor een lijst van gegevenstypen Hallo ondersteund [gegevenstypen](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in Hallo CREATE TABLE-instructie. 


## <a name="minimize-row-length"></a>Rijlengte minimaliseren
Grootte van gegevenstypen met Hallo minimaliseren verkort Hallo rijlengte, wat de queryprestaties toobetter leidt. Hallo kleinste gegevenstype gebruiken die geschikt is voor uw gegevens. 

- Vermijd tekenkolommen met een grote standaardlengte wordt vereist. Bijvoorbeeld, als de langste waarde Hallo 25 tekens, vervolgens definiëren de kolom als VARCHAR(25). 
- Vermijd het gebruik van [NVARCHAR] [ NVARCHAR] wanneer hoeft u alleen VARCHAR.
- Gebruik zo mogelijk NVARCHAR(4000) of VARCHAR(8000) in plaats van NVARCHAR(MAX) of VARCHAR(MAX).

Als u van Polybase tooload uw tabellen gebruikmaakt, Hallo gedefinieerd van Hallo tabelrij kan niet langer zijn dan 1 MB. Wanneer een rij met variabele lengte groter is dan 1 MB, kunt u Hallo rij met BCP, maar niet met PolyBase laden.

## <a name="identify-unsupported-data-types"></a>Niet-ondersteunde gegevenstypen identificeren
Als u uw database uit een andere SQL-database migreert, kunt u de gegevenstypen die worden niet ondersteund in SQL Data Warehouse kunt tegenkomen. Gebruik deze query niet-ondersteunde toodiscover-gegevenstypen in uw bestaande SQL-schema.

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <a name="unsupported-data-types"></a>Tijdelijke oplossingen voor niet-ondersteunde gegevenstypen gebruiken

Hallo hieronder toont Hallo gegevenstypen die biedt geen ondersteuning voor SQL Data Warehouse en biedt alternatieven die u in plaats van Hallo gebruiken kunt niet-ondersteunde gegevenstypen.

| Niet-ondersteund gegevenstype | Tijdelijke oplossing |
| --- | --- |
| [geometrie][geometry] |[varbinary][varbinary] |
| [Geografie][geography] |[varbinary][varbinary] |
| [hierarchyid][hierarchyid] |[nvarchar][nvarchar](4000) |
| [afbeelding][ntext,text,image] |[varbinary][varbinary] |
| [tekst][ntext,text,image] |[varchar][varchar] |
| [ntext][ntext,text,image] |[nvarchar][nvarchar] |
| [sql_variant][sql_variant] |Kolom splitsen in meerdere sterk getypeerde kolommen. |
| [tabel][table] |Tootemporary tabellen worden geconverteerd. |
| [tijdstempel][timestamp] |Bijwerken van code toouse [datetime2] [ datetime2] en `CURRENT_TIMESTAMP` functie.  Alleen constanten worden ondersteund als standaardwaarden, daarom current_timestamp kan niet worden gedefinieerd als een default-beperking. Als u toomigrate rijwaarden versie van een getypeerde timestamp-kolom moet, gebruik [binaire][BINARY](8) of [VARBINARY][BINARY](8) voor NOT NULL of NULL-waarden van rijen versie. |
| [XML][xml] |[varchar][varchar] |
| [de gebruiker gedefinieerd type][user defined types] |Native gegevenstype back toohello indien mogelijk converteren. |
| standaardwaarden | Standaardwaarden ondersteuning literals en alleen constanten.  Niet-deterministische expressies of functies, zoals `GETDATE()` of `CURRENT_TIMESTAMP`, worden niet ondersteund. |


## <a name="next-steps"></a>Volgende stappen
toolearn meer, Zie:

- [Aanbevolen procedures van SQL datawarehouse][SQL Data Warehouse Best Practices]
- [Overzicht van de tabel][Overview]
- [Het distribueren van een tabel][Distribute]
- [Indexeren van een tabel][Index]
- [Partitioneren van een tabel][Partition]
- [Tabelstatistieken onderhouden][Statistics]
- [Tijdelijke tabellen][Temporary]

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
