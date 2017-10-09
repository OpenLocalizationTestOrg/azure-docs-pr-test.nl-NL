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
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="4edf4-103">Voorbeeldgegevens laden in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4edf4-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="4edf4-104">Volg deze eenvoudige stappen tooload en query Hallo Adventure Works voorbeelddatabase.</span><span class="sxs-lookup"><span data-stu-id="4edf4-104">Follow these simple steps tooload and query hello Adventure Works Sample database.</span></span> <span data-ttu-id="4edf4-105">Deze scripts voor het eerst sqlcmd toorun SQL waarmee wordt gemaakt, tabellen en weergaven gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4edf4-105">These scripts first use sqlcmd toorun SQL which will create tables and views.</span></span> <span data-ttu-id="4edf4-106">Zodra de tabellen zijn gemaakt, zal Hallo scripts bcp tooload gegevens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4edf4-106">Once tables have been created, hello scripts will use bcp tooload data.</span></span>  <span data-ttu-id="4edf4-107">Als u nog sqlcmd en bcp geïnstalleerd hebt, volgt u deze koppelingen te[bcp installeren] [ install bcp] en te[sqlcmd installeren][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="4edf4-107">If you don't already have sqlcmd and bcp installed, follow these links too[install bcp][install bcp] and too[install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="4edf4-108">Voorbeeldgegevens laden</span><span class="sxs-lookup"><span data-stu-id="4edf4-108">Load sample data</span></span>
1. <span data-ttu-id="4edf4-109">Hallo downloaden [voorbeeldscripts van Adventure Works voor SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] zip-bestand.</span><span class="sxs-lookup"><span data-stu-id="4edf4-109">Download hello [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="4edf4-110">Hallo-bestanden extraheren uit gedownloade zip tooa directory op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="4edf4-110">Extract hello files from downloaded zip tooa directory on your local machine.</span></span>
3. <span data-ttu-id="4edf4-111">Hallo uitgepakt bestand aw_create.bat bewerken en stel Hallo variabelen Hallo boven aan het Hallo-bestand te volgen.</span><span class="sxs-lookup"><span data-stu-id="4edf4-111">Edit hello extracted file aw_create.bat and set hello following variables found at hello top of hello file.</span></span>  <span data-ttu-id="4edf4-112">Niet zeker tooleave geen witruimte tussen Hallo isgelijkteken (=) en het Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="4edf4-112">Be sure tooleave no whitespace between hello "=" and hello parameter.</span></span>  <span data-ttu-id="4edf4-113">Hieronder vindt u voorbeelden van hoe uw bewerkingen uitzien.</span><span class="sxs-lookup"><span data-stu-id="4edf4-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="4edf4-114">Uitvoeren van een Windows-opdrachtprompt aw_create.bat Hallo bewerkt.</span><span class="sxs-lookup"><span data-stu-id="4edf4-114">From a Windows cmd prompt, run hello edited aw_create.bat.</span></span>  <span data-ttu-id="4edf4-115">Zorg ervoor dat u in het Hallo-directory waar u uw bewerkte versie van aw_create.bat opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4edf4-115">Be sure you are in hello directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="4edf4-116">Dit script wordt...</span><span class="sxs-lookup"><span data-stu-id="4edf4-116">This script will...</span></span>
   
   * <span data-ttu-id="4edf4-117">Adventure Works tabellen of weergaven die al bestaan in de database verwijderen</span><span class="sxs-lookup"><span data-stu-id="4edf4-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="4edf4-118">Hallo Adventure Works tabellen en weergaven maken</span><span class="sxs-lookup"><span data-stu-id="4edf4-118">Create hello Adventure Works tables and views</span></span>
   * <span data-ttu-id="4edf4-119">Laden van elke Adventure Works tabel met bcp</span><span class="sxs-lookup"><span data-stu-id="4edf4-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="4edf4-120">Hallo Rijtellingen voor elke tabel Adventure Works valideren</span><span class="sxs-lookup"><span data-stu-id="4edf4-120">Validate hello row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="4edf4-121">Statistieken voor elke kolom voor elke tabel Adventure Works verzamelen</span><span class="sxs-lookup"><span data-stu-id="4edf4-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="4edf4-122">Voorbeeldgegevens query</span><span class="sxs-lookup"><span data-stu-id="4edf4-122">Query sample data</span></span>
<span data-ttu-id="4edf4-123">Wanneer u voorbeeldgegevens in uw SQL Data Warehouse hebt geladen, kunt u snel enkele query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4edf4-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="4edf4-124">toorun een query verbinding maken met database van Adventure Works tooyour nieuw gemaakt in Azure SQL DW met behulp van Visual Studio en SSDT, zoals beschreven in Hallo [query met Visual Studio] [ query with Visual Studio] document.</span><span class="sxs-lookup"><span data-stu-id="4edf4-124">toorun a query, connect tooyour newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in hello [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="4edf4-125">Voorbeeld van een eenvoudige Selecteer instructie tooget alle Hallo info Hallo werknemers:</span><span class="sxs-lookup"><span data-stu-id="4edf4-125">Example of simple select statement tooget all hello info of hello employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="4edf4-126">Voorbeeld van een complexere query met constructies zoals GROUP BY toolook op Hallo totaalbedrag voor alle verkoop op elke dag:</span><span class="sxs-lookup"><span data-stu-id="4edf4-126">Example of a more complex query using constructs such as GROUP BY toolook at hello total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="4edf4-127">Voorbeeld van een SELECT met een WHERE-component toofilter uit orders uit voor een bepaalde datum:</span><span class="sxs-lookup"><span data-stu-id="4edf4-127">Example of a SELECT with a WHERE clause toofilter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="4edf4-128">SQL Data Warehouse ondersteunt bijna alle T-SQL-constructs die ondersteuning biedt voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4edf4-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="4edf4-129">Eventuele verschillen zijn gedocumenteerd in onze [code migreren] [ migrate code] documentatie.</span><span class="sxs-lookup"><span data-stu-id="4edf4-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4edf4-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4edf4-130">Next steps</span></span>
<span data-ttu-id="4edf4-131">Nu dat u een kans tootry sommige query's met voorbeeldgegevens hebt, bekijk hoe te[ontwikkelen][develop], [laden][load], of [ migreren] [ migrate] tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4edf4-131">Now that you've had a chance tootry some queries with sample data, check out how too[develop][develop], [load][load], or [migrate][migrate] tooSQL Data Warehouse.</span></span>

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
