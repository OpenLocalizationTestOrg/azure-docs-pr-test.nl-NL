---
title: aaaUse bcp tooload-gegevens in SQL Data Warehouse | Microsoft Docs
description: Meer informatie over welke BCP en hoe toouse voor datawarehousescenario's.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a>Gegevens laden met bcp
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

**[BCP] [ bcp]**  is een opdrachtregelprogramma voor het bulksgewijs laden hulpprogramma waarmee u toocopy gegevens tussen de SQL Server, gegevensbestanden en SQL Data Warehouse. Gebruikt bcp tooimport groot aantal rijen in SQL Data Warehouse-tabellen of tooexport gegevens uit SQL Server-tabellen naar gegevensbestanden. Bcp vereist, behalve wanneer gebruikt de optie queryout hello, zonder enige kennis van Transact-SQL.

BCP is een snelle en gemakkelijke manier toomove kleinere gegevenssets van en naar een SQL Data Warehouse-database. Hallo exacte hoeveelheid gegevens die wordt aanbevolen tooload/extract via bcp hangen af op het netwerk van verbinding toohello Azure-Datacenter.  Over het algemeen kunt u dimensietabellen probleemloos laden en extraheren met BCP. Voor grote hoeveelheden gegevens wordt BCP echter niet aangeraden.  Polybase is Hallo aanbevolen hulpprogramma voor het laden en extraheren van grote hoeveelheden gegevens als er een beter geschikt Hallo uitgebreide parallelle verwerkingsarchitectuur van SQL Data Warehouse.

Met BCP kunt u:

* Gebruik een eenvoudig opdrachtregelprogramma tooload gegevens in SQL Data Warehouse.
* Gebruik een eenvoudig opdrachtregelprogramma tooextract gegevens uit SQL Data Warehouse.

In deze zelfstudie leert u hoe u het volgende kunt doen:

* Gegevens importeren in een tabel met behulp van bcp Hallo in de opdracht
* Gegevens exporteren uit een tabel met behulp Hallo bcp-opdracht out

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a>Vereisten
toostep voor deze zelfstudie hebt u nodig:

* Een SQL Data Warehouse-database
* Hallo bcp opdrachtregel-hulpprogramma is geïnstalleerd
* Hallo SQLCMD vanaf de opdrachtregel-hulpprogramma is geïnstalleerd

> [!NOTE]
> U kunt hulpprogramma's voor Hallo bcp en sqlcmd downloaden van Hallo [Microsoft Download Center][Microsoft Download Center].
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a>Gegevens importeren in SQL Data Warehouse
In deze zelfstudie maakt u een tabel maken in Azure SQL Data Warehouse en gegevens importeren in de tabel Hallo.

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a>Stap 1: een tabel maken in Azure SQL Data Warehouse
Gebruik vanaf een opdrachtprompt sqlcmd toorun Hallo query toocreate een tabel op uw exemplaar te volgen:

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

> [!NOTE]
> Zie [tabel overzicht] [ Table Overview] of [syntaxis voor CREATE TABLE] [ CREATE TABLE syntax] voor meer informatie over het maken van een tabel in SQL Data Warehouse en Hallo  beschikbare opties in de component WITH Hallo.
> 
> 

### <a name="step-2-create-a-source-data-file"></a>Stap 2: een brongegevensbestand maken
Open Kladblok en kopieer Hallo volgende regels van gegevens naar een nieuw tekstbestand en sla dit bestand tooyour lokale tijdelijke map C:\Temp\DimDate2.txt.

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

> [!NOTE]
> Het is belangrijk tooremember die bcp.exe biedt geen ondersteuning voor UTF-8 Hallo bestandscodering. Gebruik ASCII-bestanden of bestanden met de bestandscodering UTF-16 als u bcp.exe gebruikt.
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a>Stap 3: Verbinding maken en Hallo gegevens importeren
Met bcp kunt u verbinding maken en importeren van Hallo-gegevens met behulp van Hallo opdracht vervangen Hallo waarden waar nodig te volgen:

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

U kunt de gegevens zijn geladen door het uitvoeren van de volgende query met sqlcmd Hallo Hallo controleren:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Dit resultaat moet geven Hallo resultaten te volgen:

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

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Stap 4: statistieken maken voor uw zojuist geladen gegevens
Azure SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken. Het is belangrijk dat u statistieken voor alle kolommen van alle tabellen nadat Hallo eerst zijn geladen maakt of belangrijke wijzigingen plaatsvinden in Hallo gegevens in volgorde tooget Hallo optimale prestaties van uw query. Zie voor een gedetailleerde uitleg van statistieken Hallo [statistieken] [ Statistics] onderwerp in Hallo groep onderwerpen. Hieronder vindt u een kort voorbeeld van hoe toocreate statistieken op Hallo ingediend in dit voorbeeld geladen

Hallo volgende CREATE STATISTICS-instructies uit een sqlcmd-opdrachtprompt uitvoeren:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a>Gegevens uit SQL Data Warehouse exporteren
In deze zelfstudie maakt u een gegevensbestand op basis van een tabel in SQL Data Warehouse. We worden tooa nieuw gegevensbestand naam DimDate2_export.txt gemaakte Hallo-gegevens geëxporteerd.

### <a name="step-1-export-hello-data"></a>Stap 1: Hallo gegevens exporteren
Hallo bcp-hulpprogramma gebruikt, kunt u verbinding maken en gegevens exporteren met de Hallo na opdracht vervangen Hallo waarden waar nodig:

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
U kunt controleren of Hallo gegevens correct zijn geëxporteerd door nieuwe Hallo-bestand te openen. Hallo-gegevens in Hallo-bestand moet overeenkomen met de Hallo onderstaande tekst:

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

> [!NOTE]
> Vervaldatum toohello aard van gedistribueerde systemen, Hallo gegevensvolgorde mogelijk niet dezelfde Hallo tussen databases van SQL Data Warehouse. Een andere optie is toouse hello **queryout** functie van bcp toowrite een query uitpakken in plaats van de gehele tabel Hallo exporteren.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Zie [Gegevens laden in SQL Data Warehouse][Load data into SQL Data Warehouse] voor een overzicht van het laden.
Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.

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
