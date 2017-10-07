---
title: aaaGuide voor het gebruik van PolyBase in SQL Data Warehouse | Microsoft Docs
description: Richtlijnen en aanbevelingen voor het gebruik van PolyBase in SQL Data Warehouse-scenario's.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a>Handleiding voor het gebruik van PolyBase in SQL Data Warehouse
Deze handleiding biedt praktische informatie voor het gebruik van PolyBase in SQL Data Warehouse.

tooget gestart, Zie Hallo [gegevens laden met PolyBase] [ Load data with PolyBase] zelfstudie.

## <a name="rotating-storage-keys"></a>Opslagsleutels draaien
Van tijd tootime zult u om veiligheidsredenen toochange Hallo toegang sleutel tooyour blob-opslag.

Hallo meest elegante manier tooperform die deze taak een proces genaamd is 'hello sleutels roteren' toofollow. U mogelijk opgevallen dat er twee opslagsleutels voor blob storage-account. Dit is zodat kunt u overstappen

Roteren van uw sleutels van Azure storage-account is een proces eenvoudige drie stappen

1. Tweede-scoped databasereferentie op basis van de toegangssleutel voor Hallo secundaire opslag maken
2. Tweede externe gegevensbron gebaseerd op deze nieuwe referentie maken
3. Verwijderen en Hallo externe tabel(len) toohello nieuwe externe gegevensbron wijzen maken

Wanneer u alle uw externe tabellen toohello nieuwe externe gegevensbron hebt gemigreerd en vervolgens kunt u uitvoeren opschonen Hallo taken:

1. Eerste externe gegevensbron verwijderen
2. Uitgevallen eerste database-scoped referentie op basis van de toegangssleutel voor Hallo primaire opslag
3. Meld u aan bij Azure en opnieuw genereren van Hallo primaire toegangssleutel gereed voor Hallo volgende keer

## <a name="query-azure-blob-storage-data"></a>Query uitvoeren op Azure blob storage-gegevens
Hallo-tabelnaam een query uitgevoerd naar externe tabellen gewoon gebruiken alsof deze een relationele tabel is.

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> Een query op een externe tabel mislukken met fout Hallo *'Query afgebroken--Hallo maximale afwijzen drempelwaarde werd bereikt tijdens het lezen van een externe bron'*. Dit geeft aan dat de externe gegevens bevat *dirty* records. Een record wordt beschouwd als 'vervuild' als Hallo actuele gegevens typen of aantal kolommen komen niet overeen met de kolomdefinities Hallo van de externe tabel Hallo of als Hallo gegevens toohello opgegeven externe bestandsindeling komt niet overeen. toofix, zorg ervoor dat uw externe tabel en het externe bestand indeling definities juist zijn en de externe gegevens conform toothese definities. Als een subset van externe gegevensrecords zijn gewijzigd, kunt u tooreject deze records voor uw query's met Hallo Weiger de opties in externe tabel-DDL maken.
> 
> 

## <a name="load-data-from-azure-blob-storage"></a>Gegevens laden vanuit Azure-blobopslag
In dit voorbeeld worden gegevens geladen uit Azure blob storage tooSQL Data Warehouse-database.

Opslaan van gegevens rechtstreeks verwijdert Hallo gegevens overdrachtstijd voor query's. Opslaan van gegevens met een columnstore-index verbetert de prestaties van query's voor analyse van query's door up too10x.

In dit voorbeeld gebruikt tooload gegevens Hallo CREATE TABLE AS SELECT-instructie. nieuwe tabel Hallo overgenomen Hallo kolommen met de naam in het Hallo-query. Hallo-gegevenstypen van die kolommen van de definitie van de externe tabel Hallo worden overgenomen.

CREATE TABLE AS SELECT is een zeer zodat Transact-SQL-instructie dat wordt geladen Hallo-gegevens in de parallelle tooall Hallo rekenknooppunten van uw SQL Data Warehouse.  Het oorspronkelijk is ontwikkeld voor Hallo massively parallelle processing (MPP)-engine in Analytics Platform System en bevindt zich nu in SQL Data Warehouse.

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

Zie [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].

## <a name="create-statistics-on-newly-loaded-data"></a>Statistieken maken voor zojuist geladen gegevens
Azure SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken.  Het is belangrijk dat u statistieken voor alle kolommen van alle tabellen nadat Hallo eerst zijn geladen maakt of belangrijke wijzigingen plaatsvinden in Hallo gegevens in volgorde tooget Hallo optimale prestaties van uw query.  Zie voor een gedetailleerde uitleg van statistieken Hallo [statistieken] [ Statistics] onderwerp in Hallo groep onderwerpen.  Hieronder volgt een kort voorbeeld van hoe toocreate statistieken op Hallo ingediend in dit voorbeeld geladen.

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a>Exporteren van gegevens tooAzure blob-opslag
Deze sectie wordt beschreven hoe tooexport gegevens uit SQL Data Warehouse tooAzure blob-opslag. In dit voorbeeld maakt gebruik van CREATE externe TABLE AS SELECT die een zeer zodat Transact-SQL-instructie tooexport Hallo gegevens parallel uit alle Hallo rekenknooppunten.

Hallo wordt volgende voorbeeld een externe tabel Weblogs2014 met behulp van de kolomdefinities en gegevens van dbo. Weblogboeken tabel. Hallo externe tabeldefinitie wordt opgeslagen in SQL Data Warehouse en de resultaten Hallo Hallo SELECT-instructie geëxporteerde toohello '/ archiveren/log2014 /' map onder Hallo blob-container door Hallo-gegevensbron opgegeven. Hallo gegevens Hallo opgegeven tekstbestand geëxporteerd.

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a>Het laden van gebruikers isoleren
Er is vaak een toohave moeten meerdere gebruikers die gegevens in een SQL DW laden kunnen. Omdat Hallo [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] vereist machtigingen voor beheer van Hallo-database, verschijnt met meerdere gebruikers met toegangsbeheer via alle schema's. toolimit, kunt u Hallo weigeren CONTROL-instructie.

Voorbeeld: Overweeg database schema's schema_A voor afdeling A en schema_B voor afdeling B laten database gebruikers user_A en user_B worden gebruikers voor PolyBase laden in afdeling A en B, respectievelijk. Ze hebben gekregen BESTURINGSELEMENT databasemachtigingen.
Hallo auteurs van schema A en B vergrendelen nu hun schema's met behulp van weigeren:

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 Met dit user_A en user_B moeten nu worden vergrendeld van Hallo andere afdeling schema.
 


## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over het verplaatsen gegevens tooSQL datawarehouse, Zie Hallo [Migratieoverzicht][data migration overview].

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
