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
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="a0431-103">Richtlijnen voor het definiëren van gegevenstypen voor tabellen in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a0431-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="a0431-104">Gebruik deze aanbevelingen toodefine tabel-gegevenstypen die compatibel met SQL Data Warehouse zijn.</span><span class="sxs-lookup"><span data-stu-id="a0431-104">Use these recommendations toodefine table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="a0431-105">Bovendien verbetert toocompatibility, voor het minimaliseren van Hallo grootte van gegevenstypen met de prestaties van query's.</span><span class="sxs-lookup"><span data-stu-id="a0431-105">In addition toocompatibility, minimizing hello size of data types improves query performance.</span></span>

<span data-ttu-id="a0431-106">SQL Data Warehouse ondersteunt Hallo meest gebruikte gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="a0431-106">SQL Data Warehouse supports hello most commonly used data types.</span></span> <span data-ttu-id="a0431-107">Zie voor een lijst van gegevenstypen Hallo ondersteund [gegevenstypen](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in Hallo CREATE TABLE-instructie.</span><span class="sxs-lookup"><span data-stu-id="a0431-107">For a list of hello supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in hello CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="a0431-108">Rijlengte minimaliseren</span><span class="sxs-lookup"><span data-stu-id="a0431-108">Minimize row length</span></span>
<span data-ttu-id="a0431-109">Grootte van gegevenstypen met Hallo minimaliseren verkort Hallo rijlengte, wat de queryprestaties toobetter leidt.</span><span class="sxs-lookup"><span data-stu-id="a0431-109">Minimizing hello size of data types shortens hello row length, which leads toobetter query performance.</span></span> <span data-ttu-id="a0431-110">Hallo kleinste gegevenstype gebruiken die geschikt is voor uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="a0431-110">Use hello smallest data type that works for your data.</span></span> 

- <span data-ttu-id="a0431-111">Vermijd tekenkolommen met een grote standaardlengte wordt vereist.</span><span class="sxs-lookup"><span data-stu-id="a0431-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="a0431-112">Bijvoorbeeld, als de langste waarde Hallo 25 tekens, vervolgens definiëren de kolom als VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="a0431-112">For example, if hello longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="a0431-113">Vermijd het gebruik van [NVARCHAR] [ NVARCHAR] wanneer hoeft u alleen VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="a0431-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="a0431-114">Gebruik zo mogelijk NVARCHAR(4000) of VARCHAR(8000) in plaats van NVARCHAR(MAX) of VARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="a0431-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="a0431-115">Als u van Polybase tooload uw tabellen gebruikmaakt, Hallo gedefinieerd van Hallo tabelrij kan niet langer zijn dan 1 MB.</span><span class="sxs-lookup"><span data-stu-id="a0431-115">If you are using Polybase tooload your tables, hello defined length of hello table row cannot exceed 1 MB.</span></span> <span data-ttu-id="a0431-116">Wanneer een rij met variabele lengte groter is dan 1 MB, kunt u Hallo rij met BCP, maar niet met PolyBase laden.</span><span class="sxs-lookup"><span data-stu-id="a0431-116">When a row with variable-length data exceeds 1 MB, you can load hello row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="a0431-117">Niet-ondersteunde gegevenstypen identificeren</span><span class="sxs-lookup"><span data-stu-id="a0431-117">Identify unsupported data types</span></span>
<span data-ttu-id="a0431-118">Als u uw database uit een andere SQL-database migreert, kunt u de gegevenstypen die worden niet ondersteund in SQL Data Warehouse kunt tegenkomen.</span><span class="sxs-lookup"><span data-stu-id="a0431-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="a0431-119">Gebruik deze query niet-ondersteunde toodiscover-gegevenstypen in uw bestaande SQL-schema.</span><span class="sxs-lookup"><span data-stu-id="a0431-119">Use this query toodiscover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="a0431-120"><a name="unsupported-data-types"></a>Tijdelijke oplossingen voor niet-ondersteunde gegevenstypen gebruiken</span><span class="sxs-lookup"><span data-stu-id="a0431-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="a0431-121">Hallo hieronder toont Hallo gegevenstypen die biedt geen ondersteuning voor SQL Data Warehouse en biedt alternatieven die u in plaats van Hallo gebruiken kunt niet-ondersteunde gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="a0431-121">hello following list shows hello data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of hello unsupported data types.</span></span>

| <span data-ttu-id="a0431-122">Niet-ondersteund gegevenstype</span><span class="sxs-lookup"><span data-stu-id="a0431-122">Unsupported data type</span></span> | <span data-ttu-id="a0431-123">Tijdelijke oplossing</span><span class="sxs-lookup"><span data-stu-id="a0431-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="a0431-124">[geometrie][geometry]</span><span class="sxs-lookup"><span data-stu-id="a0431-124">[geometry][geometry]</span></span> |<span data-ttu-id="a0431-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="a0431-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="a0431-126">[Geografie][geography]</span><span class="sxs-lookup"><span data-stu-id="a0431-126">[geography][geography]</span></span> |<span data-ttu-id="a0431-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="a0431-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="a0431-128">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="a0431-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="a0431-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="a0431-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="a0431-130">[afbeelding][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="a0431-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="a0431-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="a0431-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="a0431-132">[tekst][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="a0431-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="a0431-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="a0431-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="a0431-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="a0431-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="a0431-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="a0431-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="a0431-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="a0431-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="a0431-137">Kolom splitsen in meerdere sterk getypeerde kolommen.</span><span class="sxs-lookup"><span data-stu-id="a0431-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="a0431-138">[tabel][table]</span><span class="sxs-lookup"><span data-stu-id="a0431-138">[table][table]</span></span> |<span data-ttu-id="a0431-139">Tootemporary tabellen worden geconverteerd.</span><span class="sxs-lookup"><span data-stu-id="a0431-139">Convert tootemporary tables.</span></span> |
| <span data-ttu-id="a0431-140">[tijdstempel][timestamp]</span><span class="sxs-lookup"><span data-stu-id="a0431-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="a0431-141">Bijwerken van code toouse [datetime2] [ datetime2] en `CURRENT_TIMESTAMP` functie.</span><span class="sxs-lookup"><span data-stu-id="a0431-141">Rework code toouse [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="a0431-142">Alleen constanten worden ondersteund als standaardwaarden, daarom current_timestamp kan niet worden gedefinieerd als een default-beperking.</span><span class="sxs-lookup"><span data-stu-id="a0431-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="a0431-143">Als u toomigrate rijwaarden versie van een getypeerde timestamp-kolom moet, gebruik [binaire][BINARY](8) of [VARBINARY][BINARY](8) voor NOT NULL of NULL-waarden van rijen versie.</span><span class="sxs-lookup"><span data-stu-id="a0431-143">If you need toomigrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="a0431-144">[XML][xml]</span><span class="sxs-lookup"><span data-stu-id="a0431-144">[xml][xml]</span></span> |<span data-ttu-id="a0431-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="a0431-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="a0431-146">[de gebruiker gedefinieerd type][user defined types]</span><span class="sxs-lookup"><span data-stu-id="a0431-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="a0431-147">Native gegevenstype back toohello indien mogelijk converteren.</span><span class="sxs-lookup"><span data-stu-id="a0431-147">Convert back toohello native data type when possible.</span></span> |
| <span data-ttu-id="a0431-148">standaardwaarden</span><span class="sxs-lookup"><span data-stu-id="a0431-148">default values</span></span> | <span data-ttu-id="a0431-149">Standaardwaarden ondersteuning literals en alleen constanten.</span><span class="sxs-lookup"><span data-stu-id="a0431-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="a0431-150">Niet-deterministische expressies of functies, zoals `GETDATE()` of `CURRENT_TIMESTAMP`, worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a0431-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="a0431-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0431-151">Next steps</span></span>
<span data-ttu-id="a0431-152">toolearn meer, Zie:</span><span class="sxs-lookup"><span data-stu-id="a0431-152">toolearn more, see:</span></span>

- <span data-ttu-id="a0431-153">[Aanbevolen procedures van SQL datawarehouse][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="a0431-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="a0431-154">[Overzicht van de tabel][Overview]</span><span class="sxs-lookup"><span data-stu-id="a0431-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="a0431-155">[Het distribueren van een tabel][Distribute]</span><span class="sxs-lookup"><span data-stu-id="a0431-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="a0431-156">[Indexeren van een tabel][Index]</span><span class="sxs-lookup"><span data-stu-id="a0431-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="a0431-157">[Partitioneren van een tabel][Partition]</span><span class="sxs-lookup"><span data-stu-id="a0431-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="a0431-158">[Tabelstatistieken onderhouden][Statistics]</span><span class="sxs-lookup"><span data-stu-id="a0431-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="a0431-159">[Tijdelijke tabellen][Temporary]</span><span class="sxs-lookup"><span data-stu-id="a0431-159">[Temporary Tables][Temporary]</span></span>

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
