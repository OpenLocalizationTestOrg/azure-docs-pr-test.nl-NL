---
title: aaaLoad gegevens uit CSV-bestand in Azure SQL Database (bcp) | Microsoft Docs
description: Voor kleine gegevenssets gebruikt bcp tooimport gegevens in Azure SQL Database.
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>Gegevens vanuit een CSV-bestand laden in een Azure SQL-database (platte bestanden)
U kunt Hallo bcp opdrachtregelprogramma tooimport gegevens uit een CSV-bestand in Azure SQL Database.

## <a name="before-you-begin"></a>Voordat u begint
### <a name="prerequisites"></a>Vereisten
toocomplete hello stappen in dit artikel, moet u:

* Een logische Azure SQL-databaseserver en -database
* Hallo opdrachtregelprogramma bcp geïnstalleerd
* Hallo sqlcmd-opdrachtregelprogramma geïnstalleerd

U kunt hulpprogramma's voor Hallo bcp en sqlcmd downloaden van Hallo [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Gegevens in ASCII- of UTF-16-indeling
Als u deze zelfstudie met uw eigen gegevens probeert, moet uw gegevens toouse Hallo ASCII- of UTF-16 omdat bcp biedt geen ondersteuning voor UTF-8-codering. 

## <a name="1-create-a-destination-table"></a>1. Een doeltabel maken
Een tabel in SQL-Database te definiëren als Hallo doeltabel. Hallo-kolommen in tabel Hallo moeten overeenkomen met toohello gegevens in elke rij van het gegevensbestand.

toocreate een tabel, open een opdrachtprompt en sqlcmd.exe toorun Hallo volgende opdracht gebruiken:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
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

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a>3. Hallo gegevens laden
tooload hello gegevens, open een opdrachtprompt en Voer Hallo de volgende opdracht, Hallo waarden voor de servernaam, Database-naam, gebruikersnaam en wachtwoord worden vervangen door uw eigen gegevens.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

Gebruik die deze opdracht tooverify Hallo gegevens correct zijn geladen

```bcp
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

## <a name="next-steps"></a>Volgende stappen
Zie SQL Server-database toomigrate [migratie van SQL Server-database](sql-database-cloud-migrate.md).

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
