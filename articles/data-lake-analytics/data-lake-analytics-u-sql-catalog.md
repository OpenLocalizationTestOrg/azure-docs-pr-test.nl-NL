---
title: Aan de slag met Hallo U-SQL-catalogus | Microsoft Docs
description: Meer informatie over hoe toouse Hallo U-SQL-catalogus tooshare code en gegevens.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: edmaca
ms.openlocfilehash: 559bb7a3879031eb290a3e82946d7bf42ac9f553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-u-sql-catalog"></a>Aan de slag met Hallo U-SQL-catalogus

## <a name="create-a-tvf"></a>Maken van een TVF

In vorige U-SQL-script hello wordt herhaald u Hallo gebruik van EXTRACT tooread van Hallo hetzelfde bronbestand. Met de Hallo U-SQL-functie met tabelwaarden (TVF), kunt u inkapselen Hallo-gegevens voor toekomstig gebruik.  

Hallo volgende script maakt een TVF aangeroepen `Searchlog()` in Hallo standaarddatabase en schema:

```
DROP FUNCTION IF EXISTS Searchlog;

CREATE FUNCTION Searchlog()
RETURNS @searchlog TABLE
(
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
)
AS BEGIN
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
RETURN;
END;
```

Hallo volgende script toont hoe toouse TVF die is gedefinieerd in de vorige script Hallo Hallo:

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a>Weergaven maken

Als u een enkele query-expressie hebt, in plaats van een TVF kunt u een U-SQL-weergave tooencapsulate die expressie.

Hallo volgende script maakt een weergave met de naam `SearchlogView` in Hallo standaarddatabase en schema:

```
DROP VIEW IF EXISTS SearchlogView;

CREATE VIEW SearchlogView AS  
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
```

Hallo volgende script toont Hallo gebruik van de weergave Hallo gedefinieerd:

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a>Tabellen maken
Zoals met relationele database-tabellen met U-SQL kunt u een tabel met een vooraf gedefinieerd schema maken of een tabel maken Hallo schema afleidt uit Hallo-query die wordt gevuld Hallo-tabel (ook wel bekend als CREATE TABLE AS SELECT of CTAS).

Een database en de twee tabellen maken met behulp van Hallo script volgen:

```
DROP DATABASE IF EXISTS SearchLogDb;
CREATE DATABASE SearchLogDb;
USE DATABASE SearchLogDb;

DROP TABLE IF EXISTS SearchLog1;
DROP TABLE IF EXISTS SearchLog2;

CREATE TABLE SearchLog1 (
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string,

            INDEX sl_idx CLUSTERED (UserId ASC)
                DISTRIBUTED BY HASH (UserId)
);

INSERT INTO SearchLog1 SELECT * FROM master.dbo.Searchlog() AS s;

CREATE TABLE SearchLog2(
    INDEX sl_idx CLUSTERED (UserId ASC)
            DISTRIBUTED BY HASH (UserId)
) AS SELECT * FROM master.dbo.Searchlog() AS S; // You can use EXTRACT or SELECT here
```

## <a name="query-tables"></a>Querytabellen
U kunt een query tabellen, zoals die zijn gemaakt in de vorige script Hallo in Hallo dezelfde manier als dat u een query Hallo gegevensbestanden worden opgeslagen. In plaats van een rijenset maken met behulp van EXTRACT, kunt u nu de tabelnaam toohello verwijzen.

tooread uit Hallo tabellen, wijzig Hallo transformatie-script dat u eerder hebt gebruikt:

```
@rs1 =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchLogDb.dbo.SearchLog2
GROUP BY Region;

@res =
    SELECT *
    FROM @rs1
    ORDER BY TotalDuration DESC
    FETCH 5 ROWS;

OUTPUT @res
    too"/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 >U uitvoeren niet een SELECT op dit moment kunnen op een tabel in hetzelfde script, zoals een Hallo Hallo waar u Hallo tabel hebt gemaakt.

## <a name="next-steps"></a>Volgende stappen
* [Overzicht van Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [U-SQL-scripts ontwikkelen met Data Lake-hulpmiddelen voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Azure Data Lake Analytics-taken bewaken en problemen oplossen met Azure Portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
