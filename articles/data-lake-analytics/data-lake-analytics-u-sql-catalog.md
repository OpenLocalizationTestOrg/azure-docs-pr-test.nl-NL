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
# <a name="get-started-with-hello-u-sql-catalog"></a><span data-ttu-id="95db7-103">Aan de slag met Hallo U-SQL-catalogus</span><span class="sxs-lookup"><span data-stu-id="95db7-103">Get started with hello U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="95db7-104">Maken van een TVF</span><span class="sxs-lookup"><span data-stu-id="95db7-104">Create a TVF</span></span>

<span data-ttu-id="95db7-105">In vorige U-SQL-script hello wordt herhaald u Hallo gebruik van EXTRACT tooread van Hallo hetzelfde bronbestand.</span><span class="sxs-lookup"><span data-stu-id="95db7-105">In hello previous U-SQL script, you repeated hello use of EXTRACT tooread from hello same source file.</span></span> <span data-ttu-id="95db7-106">Met de Hallo U-SQL-functie met tabelwaarden (TVF), kunt u inkapselen Hallo-gegevens voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="95db7-106">With hello U-SQL table-valued function (TVF), you can encapsulate hello data for future reuse.</span></span>  

<span data-ttu-id="95db7-107">Hallo volgende script maakt een TVF aangeroepen `Searchlog()` in Hallo standaarddatabase en schema:</span><span class="sxs-lookup"><span data-stu-id="95db7-107">hello following script creates a TVF called `Searchlog()` in hello default database and schema:</span></span>

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

<span data-ttu-id="95db7-108">Hallo volgende script toont hoe toouse TVF die is gedefinieerd in de vorige script Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="95db7-108">hello following script shows you how toouse hello TVF that was defined in hello previous script:</span></span>

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

## <a name="create-views"></a><span data-ttu-id="95db7-109">Weergaven maken</span><span class="sxs-lookup"><span data-stu-id="95db7-109">Create views</span></span>

<span data-ttu-id="95db7-110">Als u een enkele query-expressie hebt, in plaats van een TVF kunt u een U-SQL-weergave tooencapsulate die expressie.</span><span class="sxs-lookup"><span data-stu-id="95db7-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW tooencapsulate that expression.</span></span>

<span data-ttu-id="95db7-111">Hallo volgende script maakt een weergave met de naam `SearchlogView` in Hallo standaarddatabase en schema:</span><span class="sxs-lookup"><span data-stu-id="95db7-111">hello following script creates a view called `SearchlogView` in hello default database and schema:</span></span>

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

<span data-ttu-id="95db7-112">Hallo volgende script toont Hallo gebruik van de weergave Hallo gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="95db7-112">hello following script demonstrates hello use of hello defined view:</span></span>

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

## <a name="create-tables"></a><span data-ttu-id="95db7-113">Tabellen maken</span><span class="sxs-lookup"><span data-stu-id="95db7-113">Create tables</span></span>
<span data-ttu-id="95db7-114">Zoals met relationele database-tabellen met U-SQL kunt u een tabel met een vooraf gedefinieerd schema maken of een tabel maken Hallo schema afleidt uit Hallo-query die wordt gevuld Hallo-tabel (ook wel bekend als CREATE TABLE AS SELECT of CTAS).</span><span class="sxs-lookup"><span data-stu-id="95db7-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers hello schema from hello query that populates hello table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="95db7-115">Een database en de twee tabellen maken met behulp van Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="95db7-115">Create a database and two tables by using hello following script:</span></span>

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

## <a name="query-tables"></a><span data-ttu-id="95db7-116">Querytabellen</span><span class="sxs-lookup"><span data-stu-id="95db7-116">Query tables</span></span>
<span data-ttu-id="95db7-117">U kunt een query tabellen, zoals die zijn gemaakt in de vorige script Hallo in Hallo dezelfde manier als dat u een query Hallo gegevensbestanden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="95db7-117">You can query tables, such as those created in hello previous script, in hello same way that you query hello data files.</span></span> <span data-ttu-id="95db7-118">In plaats van een rijenset maken met behulp van EXTRACT, kunt u nu de tabelnaam toohello verwijzen.</span><span class="sxs-lookup"><span data-stu-id="95db7-118">Instead of creating a rowset by using EXTRACT, you now can refer toohello table name.</span></span>

<span data-ttu-id="95db7-119">tooread uit Hallo tabellen, wijzig Hallo transformatie-script dat u eerder hebt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="95db7-119">tooread from hello tables, modify hello transform script that you used previously:</span></span>

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
 ><span data-ttu-id="95db7-120">U uitvoeren niet een SELECT op dit moment kunnen op een tabel in hetzelfde script, zoals een Hallo Hallo waar u Hallo tabel hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="95db7-120">Currently, you cannot run a SELECT on a table in hello same script as hello one where you created hello table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95db7-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="95db7-121">Next Steps</span></span>
* [<span data-ttu-id="95db7-122">Overzicht van Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="95db7-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="95db7-123">U-SQL-scripts ontwikkelen met Data Lake-hulpmiddelen voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="95db7-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="95db7-124">Azure Data Lake Analytics-taken bewaken en problemen oplossen met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="95db7-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
