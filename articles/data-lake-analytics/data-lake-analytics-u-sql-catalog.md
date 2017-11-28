---
title: Aan de slag met de U-SQL-catalogus | Microsoft Docs
description: Informatie over het gebruik van de U-SQL-catalogus code en gegevens delen.
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
ms.openlocfilehash: 08364c6c7bea53807844e3b1cc327dc3742e0487
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-u-sql-catalog"></a><span data-ttu-id="6bf4f-103">Aan de slag met de U-SQL-catalogus</span><span class="sxs-lookup"><span data-stu-id="6bf4f-103">Get started with the U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="6bf4f-104">Maken van een TVF</span><span class="sxs-lookup"><span data-stu-id="6bf4f-104">Create a TVF</span></span>

<span data-ttu-id="6bf4f-105">In de vorige U-SQL-script wordt herhaald u het gebruik van EXTRACT lezen uit het bronbestand met dezelfde.</span><span class="sxs-lookup"><span data-stu-id="6bf4f-105">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span></span> <span data-ttu-id="6bf4f-106">Met de U-SQL-functie met tabelwaarden (TVF), kunt u de gegevens voor toekomstig gebruik inkapselen.</span><span class="sxs-lookup"><span data-stu-id="6bf4f-106">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span></span>  

<span data-ttu-id="6bf4f-107">Het volgende script maakt een TVF aangeroepen `Searchlog()` in de standaarddatabase en het schema:</span><span class="sxs-lookup"><span data-stu-id="6bf4f-107">The following script creates a TVF called `Searchlog()` in the default database and schema:</span></span>

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

<span data-ttu-id="6bf4f-108">Het volgende script toont hoe u de TVF die is gedefinieerd in het vorige script:</span><span class="sxs-lookup"><span data-stu-id="6bf4f-108">The following script shows you how to use the TVF that was defined in the previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="6bf4f-109">Weergaven maken</span><span class="sxs-lookup"><span data-stu-id="6bf4f-109">Create views</span></span>

<span data-ttu-id="6bf4f-110">Als u een enkele query-expressie hebt, in plaats van een TVF kunt u een U-SQL-weergave inkapselen die expressie.</span><span class="sxs-lookup"><span data-stu-id="6bf4f-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW to encapsulate that expression.</span></span>

<span data-ttu-id="6bf4f-111">Het volgende script maakt een weergave met de naam `SearchlogView` in de standaarddatabase en het schema:</span><span class="sxs-lookup"><span data-stu-id="6bf4f-111">The following script creates a view called `SearchlogView` in the default database and schema:</span></span>

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

<span data-ttu-id="6bf4f-112">Het volgende script toont het gebruik van de gedefinieerde weergave:</span><span class="sxs-lookup"><span data-stu-id="6bf4f-112">The following script demonstrates the use of the defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="6bf4f-113">Tabellen maken</span><span class="sxs-lookup"><span data-stu-id="6bf4f-113">Create tables</span></span>
<span data-ttu-id="6bf4f-114">Zoals met relationele database-tabellen met U-SQL kunt u een tabel met een vooraf gedefinieerd schema maken of een tabel maken die het schema uit de query afleidt die de tabel (ook wel bekend als CREATE TABLE AS SELECT of CTAS) gevuld.</span><span class="sxs-lookup"><span data-stu-id="6bf4f-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="6bf4f-115">Een database en de twee tabellen maken met het volgende script:</span><span class="sxs-lookup"><span data-stu-id="6bf4f-115">Create a database and two tables by using the following script:</span></span>

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

## <a name="query-tables"></a><span data-ttu-id="6bf4f-116">Querytabellen</span><span class="sxs-lookup"><span data-stu-id="6bf4f-116">Query tables</span></span>
<span data-ttu-id="6bf4f-117">U kunt de tabellen, zoals die zijn gemaakt in het vorige script, op dezelfde manier als dat u de gegevensbestanden query opvragen.</span><span class="sxs-lookup"><span data-stu-id="6bf4f-117">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span></span> <span data-ttu-id="6bf4f-118">In plaats van een rijenset maken met behulp van EXTRACT, nu raadpleegt u de naam van de tabel.</span><span class="sxs-lookup"><span data-stu-id="6bf4f-118">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span></span>

<span data-ttu-id="6bf4f-119">Als u wilt lezen uit de tabellen, wijzig de transformatie-script dat u eerder hebt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="6bf4f-119">To read from the tables, modify the transform script that you used previously:</span></span>

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
    TO "/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="6bf4f-120">U uitvoeren niet een SELECT op dit moment op een tabel in hetzelfde script als het account waar u de tabel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bf4f-120">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bf4f-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6bf4f-121">Next Steps</span></span>
* [<span data-ttu-id="6bf4f-122">Overzicht van Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6bf4f-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="6bf4f-123">U-SQL-scripts ontwikkelen met Data Lake-hulpmiddelen voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6bf4f-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="6bf4f-124">Azure Data Lake Analytics-taken bewaken en problemen oplossen met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6bf4f-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
