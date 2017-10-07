---
title: aaaLoad gegevens uit SQL Server in Azure SQL Data Warehouse (bcp) | Microsoft Docs
description: Voor kleine gegevenssets gebruikt bcp tooexport gegevens uit SQL Server tooflat bestanden en importeren Hallo rechtstreeks in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a>Gegevens uit SQL Server laden in Azure SQL Data Warehouse (platte bestanden)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

U kunt voor kleine gegevenssets Hallo bcp opdrachtregelprogramma tooexport gegevens uit SQL Server gebruiken en deze direct tooAzure SQL Data Warehouse laden.

In deze zelfstudie gebruikt u BCP voor het volgende:

* Een tabel uit exporteren uit SQL Server met behulp van Hallo opdracht out in bcp (of een eenvoudig voorbeeldbestand maken)
* Hallo tabel importeren uit een plat bestand-tooSQL Data Warehouse.
* Statistieken maken voor Hallo geladen gegevens.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a>Voordat u begint
### <a name="prerequisites"></a>Vereisten
toostep voor deze zelfstudie hebt u nodig:

* Een SQL Data Warehouse-database
* Hallo opdrachtregelprogramma bcp geïnstalleerd
* Hallo sqlcmd-opdrachtregelprogramma geïnstalleerd

U kunt hulpprogramma's voor Hallo bcp en sqlcmd downloaden van Hallo [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Gegevens in ASCII- of UTF-16-indeling
Als u deze zelfstudie met uw eigen gegevens probeert, moet uw gegevens toouse Hallo ASCII- of UTF-16 omdat bcp biedt geen ondersteuning voor UTF-8-codering. 

UTF-8 wordt wel ondersteund in PolyBase, maar UTF-16 nog niet. Houd er rekening mee dat als u wilt dat toocombine bcp met PolyBase u tootransform Hallo gegevens tooUTF-8 moet na het exporteren uit SQL Server. 

## <a name="1-create-a-destination-table"></a>1. Een doeltabel maken
Definieer een tabel in SQL Data Warehouse die Hallo doeltabel voor Hallo belasting. Hallo-kolommen in tabel Hallo moeten overeenkomen met toohello gegevens in elke rij van het gegevensbestand.

toocreate een tabel, open een opdrachtprompt en sqlcmd.exe toorun Hallo volgende opdracht gebruiken:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```


## <a name="2-create-a-source-data-file"></a>2. Een brongegevensbestand maken
Open Kladblok en kopieer Hallo volgende regels van gegevens naar een nieuw tekstbestand en sla dit bestand tooyour lokale tijdelijke map C:\Temp\DimDate2.txt. Dit zijn gegevens in ASCII-indeling.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

(Optioneel) tooexport uw eigen gegevens uit een SQL Server-database, open een opdrachtprompt en Voer Hallo opdracht te volgen. Vervang TableName, ServerName, DatabaseName, Username en Password door uw eigen waarden.

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a>3. Hallo gegevens laden
tooload hello gegevens, open een opdrachtprompt en Voer Hallo de volgende opdracht, Hallo waarden voor de servernaam, Database-naam, gebruikersnaam en wachtwoord worden vervangen door uw eigen gegevens.

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

Gebruik die deze opdracht tooverify Hallo gegevens correct zijn geladen

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Hallo resultaten er als volgt uit:

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

## <a name="4-create-statistics"></a>4. Statistieken maken
SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken. tooget hello beste prestaties van query's, is belangrijk toocreate statistieken voor alle kolommen van alle tabellen na Hallo eerst zijn geladen of nadat belangrijke wijzigingen in Hallo-gegevens plaatsvinden. Zie voor een gedetailleerde uitleg van statistieken [statistieken][Statistics]. 

Voer Hallo opdracht toocreate statistieken op uw zojuist geladen tabel te volgen.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a>5. Gegevens uit SQL Data Warehouse exporteren
U kunt desgewenst Hallo-gegevens die u zojuist hebt geladen, weer uit SQL Data Warehouse exporteren.  Hallo opdracht tooexport is precies hetzelfde als het exporteren uit SQL Server Hallo.

Er is echter een verschil in Hallo resultaten. Aangezien het Hallo-gegevens worden opgeslagen op gedistribueerde locaties in SQL Data Warehouse, wanneer u gegevens exporteren schrijft deze elk rekenknooppunt gegevens toohello-uitvoerbestand. Hallo-volgorde van Hallo-gegevens in het Hallo-uitvoerbestand is waarschijnlijk anders dan de volgorde van gegevens in het invoerbestand Hallo HALLO hallo toobe.

### <a name="export-a-table-and-compare-exported-results"></a>Een tabel exporteren en exportresultaten vergelijken
toosee Hallo geëxporteerde gegevens, open een opdrachtprompt en voer deze opdracht met uw eigen parameters. ServerName is Hallo-naam van uw logische Azure SQL-Server.

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
U kunt controleren of Hallo gegevens correct zijn geëxporteerd door nieuwe Hallo-bestand te openen. Hallo-gegevens in Hallo-bestand moet overeenkomen met de onderstaande Hallo tekst, maar waarschijnlijk in een andere volgorde worden gesorteerd:

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="export-hello-results-of-a-query"></a>Hallo-resultaten van een query exporteren
U kunt Hallo **queryout** functie van bcp tooexport Hallo resultaten van een query in plaats van de gehele tabel Hallo exporteren. 

## <a name="next-steps"></a>Volgende stappen
Zie [Gegevens laden in SQL Data Warehouse][Load data into SQL Data Warehouse] voor een overzicht van het laden.
Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.
Zie [tabel overzicht] [ Table Overview] of [syntaxis voor CREATE TABLE] [ CREATE TABLE syntax] voor meer informatie over het maken van een tabel in SQL Data Warehouse.

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
