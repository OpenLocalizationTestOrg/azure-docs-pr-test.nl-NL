---
title: aaaLoad voorbeeldgegevens in SQL Data Warehouse | Microsoft Docs
description: Voorbeeldgegevens laden in SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a>Voorbeeldgegevens laden in SQL Data Warehouse
Volg deze eenvoudige stappen tooload en query Hallo Adventure Works voorbeelddatabase. Deze scripts voor het eerst sqlcmd toorun SQL waarmee wordt gemaakt, tabellen en weergaven gebruiken. Zodra de tabellen zijn gemaakt, zal Hallo scripts bcp tooload gegevens gebruiken.  Als u nog sqlcmd en bcp geïnstalleerd hebt, volgt u deze koppelingen te[bcp installeren] [ install bcp] en te[sqlcmd installeren][install sqlcmd].

## <a name="load-sample-data"></a>Voorbeeldgegevens laden
1. Hallo downloaden [voorbeeldscripts van Adventure Works voor SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] zip-bestand.
2. Hallo-bestanden extraheren uit gedownloade zip tooa directory op uw lokale machine.
3. Hallo uitgepakt bestand aw_create.bat bewerken en stel Hallo variabelen Hallo boven aan het Hallo-bestand te volgen.  Niet zeker tooleave geen witruimte tussen Hallo isgelijkteken (=) en het Hallo-parameter.  Hieronder vindt u voorbeelden van hoe uw bewerkingen uitzien.
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. Uitvoeren van een Windows-opdrachtprompt aw_create.bat Hallo bewerkt.  Zorg ervoor dat u in het Hallo-directory waar u uw bewerkte versie van aw_create.bat opgeslagen.
   Dit script wordt...
   
   * Adventure Works tabellen of weergaven die al bestaan in de database verwijderen
   * Hallo Adventure Works tabellen en weergaven maken
   * Laden van elke Adventure Works tabel met bcp
   * Hallo Rijtellingen voor elke tabel Adventure Works valideren
   * Statistieken voor elke kolom voor elke tabel Adventure Works verzamelen

## <a name="query-sample-data"></a>Voorbeeldgegevens query
Wanneer u voorbeeldgegevens in uw SQL Data Warehouse hebt geladen, kunt u snel enkele query's uitvoeren.  toorun een query verbinding maken met database van Adventure Works tooyour nieuw gemaakt in Azure SQL DW met behulp van Visual Studio en SSDT, zoals beschreven in Hallo [query met Visual Studio] [ query with Visual Studio] document.

Voorbeeld van een eenvoudige Selecteer instructie tooget alle Hallo info Hallo werknemers:

```sql
SELECT * FROM DimEmployee;
```

Voorbeeld van een complexere query met constructies zoals GROUP BY toolook op Hallo totaalbedrag voor alle verkoop op elke dag:

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

Voorbeeld van een SELECT met een WHERE-component toofilter uit orders uit voor een bepaalde datum:

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

SQL Data Warehouse ondersteunt bijna alle T-SQL-constructs die ondersteuning biedt voor SQL Server.  Eventuele verschillen zijn gedocumenteerd in onze [code migreren] [ migrate code] documentatie.

## <a name="next-steps"></a>Volgende stappen
Nu dat u een kans tootry sommige query's met voorbeeldgegevens hebt, bekijk hoe te[ontwikkelen][develop], [laden][load], of [ migreren] [ migrate] tooSQL Data Warehouse.

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
