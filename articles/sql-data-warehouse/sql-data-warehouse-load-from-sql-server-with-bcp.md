---
title: Gegevens uit SQL Server laden in Azure SQL Data Warehouse (bcp) | Microsoft Docs
description: Voor kleine gegevenssets gebruikt u BCP om gegevens uit SQL Server te exporteren naar platte bestanden en de gegevens rechtstreeks in Azure SQL Data Warehouse te importeren.
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
ms.openlocfilehash: dae7b5f7456f4ec0daf60d55f9c38b780896ff83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="ff606-103">Gegevens uit SQL Server laden in Azure SQL Data Warehouse (platte bestanden)</span><span class="sxs-lookup"><span data-stu-id="ff606-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff606-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="ff606-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="ff606-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="ff606-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="ff606-106">bcp</span><span class="sxs-lookup"><span data-stu-id="ff606-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="ff606-107">Voor kleine gegevenssets kunt u het opdrachtregelprogramma BCP gebruiken om gegevens uit SQL Server te exporteren en deze vervolgens rechtstreeks in Azure SQL Data Warehouse te laden.</span><span class="sxs-lookup"><span data-stu-id="ff606-107">For small data sets, you can use the bcp command-line utility to export data from SQL Server and then load it directly to Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="ff606-108">In deze zelfstudie gebruikt u BCP voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="ff606-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="ff606-109">Een tabel uit SQL Server exporteren met behulp van de opdracht out in BCP (of een eenvoudig voorbeeldbestand maken)</span><span class="sxs-lookup"><span data-stu-id="ff606-109">Export a table from from SQL Server by using the bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="ff606-110">De tabel uit een plat bestand importeren in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ff606-110">Import the table from a flat file to SQL Data Warehouse.</span></span>
* <span data-ttu-id="ff606-111">Statistieken maken voor de geladen gegevens.</span><span class="sxs-lookup"><span data-stu-id="ff606-111">Create statistics on the loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="ff606-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="ff606-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="ff606-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ff606-113">Prerequisites</span></span>
<span data-ttu-id="ff606-114">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="ff606-114">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="ff606-115">Een SQL Data Warehouse-database</span><span class="sxs-lookup"><span data-stu-id="ff606-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="ff606-116">Het opdrachtregelprogramma BCP (moet zijn geïnstalleerd)</span><span class="sxs-lookup"><span data-stu-id="ff606-116">The bcp command-line utility installed</span></span>
* <span data-ttu-id="ff606-117">Het opdrachtregelprogramma SQLCMD (moet zijn geïnstalleerd)</span><span class="sxs-lookup"><span data-stu-id="ff606-117">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="ff606-118">U kunt de opdrachtregelprogramma's BCP en SQLCMD downloaden van het [Microsoft Downloadcentrum][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="ff606-118">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="ff606-119">Gegevens in ASCII- of UTF-16-indeling</span><span class="sxs-lookup"><span data-stu-id="ff606-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="ff606-120">Als u deze zelfstudie wilt uitvoeren met uw eigen gegevens, moeten deze zijn gecodeerd in de ASCII- of UTF-16-indeling, omdat de indeling UTF-8 niet wordt ondersteund in BCP.</span><span class="sxs-lookup"><span data-stu-id="ff606-120">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="ff606-121">UTF-8 wordt wel ondersteund in PolyBase, maar UTF-16 nog niet.</span><span class="sxs-lookup"><span data-stu-id="ff606-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="ff606-122">Als u BCP wilt gebruiken in combinatie met PolyBase, moet u de gegevens na het exporteren uit SQL Server transformeren naar UTF-8.</span><span class="sxs-lookup"><span data-stu-id="ff606-122">Note that if you want to combine bcp with PolyBase you will need to transform the data to UTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="ff606-123">1. Een doeltabel maken</span><span class="sxs-lookup"><span data-stu-id="ff606-123">1. Create a destination table</span></span>
<span data-ttu-id="ff606-124">Definieer een (doel)tabel in SQL Data Warehouse waarin u de gegevens wilt laden.</span><span class="sxs-lookup"><span data-stu-id="ff606-124">Define a table in SQL Data Warehouse that will be the destination table for the load.</span></span> <span data-ttu-id="ff606-125">De kolommen in de tabel moeten overeenkomen met de gegevens in elke rij van het gegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="ff606-125">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="ff606-126">Open een opdrachtprompt en voer de volgende opdracht uit met sqlcmd.exe om een tabel te maken:</span><span class="sxs-lookup"><span data-stu-id="ff606-126">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="ff606-127">2. Een brongegevensbestand maken</span><span class="sxs-lookup"><span data-stu-id="ff606-127">2. Create a source data file</span></span>
<span data-ttu-id="ff606-128">Open Kladblok, kopieer de volgende regels met gegevens naar een nieuw tekstbestand en sla dit bestand op in de lokale tijdelijke map C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="ff606-128">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="ff606-129">Dit zijn gegevens in ASCII-indeling.</span><span class="sxs-lookup"><span data-stu-id="ff606-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="ff606-130">(Optioneel) Open een opdrachtprompt en voer de volgende opdracht uit om uw eigen gegevens uit een SQL Server-database te exporteren.</span><span class="sxs-lookup"><span data-stu-id="ff606-130">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="ff606-131">Vervang TableName, ServerName, DatabaseName, Username en Password door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="ff606-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-the-data"></a><span data-ttu-id="ff606-132">3. De gegevens laden</span><span class="sxs-lookup"><span data-stu-id="ff606-132">3. Load the data</span></span>
<span data-ttu-id="ff606-133">Open een opdrachtprompt en voer de volgende opdracht uit om de gegevens te laden. Vervang de waarden voor ServerName, DatabaseName, Username en Password door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="ff606-133">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="ff606-134">Gebruik deze opdracht om te controleren of de gegevens correct zijn geladen</span><span class="sxs-lookup"><span data-stu-id="ff606-134">Use this command to verify the data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="ff606-135">De resultaten horen er als volgt uit te zien:</span><span class="sxs-lookup"><span data-stu-id="ff606-135">The results should look like this:</span></span>

| <span data-ttu-id="ff606-136">DateId</span><span class="sxs-lookup"><span data-stu-id="ff606-136">DateId</span></span> | <span data-ttu-id="ff606-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="ff606-137">CalendarQuarter</span></span> | <span data-ttu-id="ff606-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="ff606-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ff606-139">20150101</span><span class="sxs-lookup"><span data-stu-id="ff606-139">20150101</span></span> |<span data-ttu-id="ff606-140">1</span><span class="sxs-lookup"><span data-stu-id="ff606-140">1</span></span> |<span data-ttu-id="ff606-141">3</span><span class="sxs-lookup"><span data-stu-id="ff606-141">3</span></span> |
| <span data-ttu-id="ff606-142">20150201</span><span class="sxs-lookup"><span data-stu-id="ff606-142">20150201</span></span> |<span data-ttu-id="ff606-143">1</span><span class="sxs-lookup"><span data-stu-id="ff606-143">1</span></span> |<span data-ttu-id="ff606-144">3</span><span class="sxs-lookup"><span data-stu-id="ff606-144">3</span></span> |
| <span data-ttu-id="ff606-145">20150301</span><span class="sxs-lookup"><span data-stu-id="ff606-145">20150301</span></span> |<span data-ttu-id="ff606-146">1</span><span class="sxs-lookup"><span data-stu-id="ff606-146">1</span></span> |<span data-ttu-id="ff606-147">3</span><span class="sxs-lookup"><span data-stu-id="ff606-147">3</span></span> |
| <span data-ttu-id="ff606-148">20150401</span><span class="sxs-lookup"><span data-stu-id="ff606-148">20150401</span></span> |<span data-ttu-id="ff606-149">2</span><span class="sxs-lookup"><span data-stu-id="ff606-149">2</span></span> |<span data-ttu-id="ff606-150">4</span><span class="sxs-lookup"><span data-stu-id="ff606-150">4</span></span> |
| <span data-ttu-id="ff606-151">20150501</span><span class="sxs-lookup"><span data-stu-id="ff606-151">20150501</span></span> |<span data-ttu-id="ff606-152">2</span><span class="sxs-lookup"><span data-stu-id="ff606-152">2</span></span> |<span data-ttu-id="ff606-153">4</span><span class="sxs-lookup"><span data-stu-id="ff606-153">4</span></span> |
| <span data-ttu-id="ff606-154">20150601</span><span class="sxs-lookup"><span data-stu-id="ff606-154">20150601</span></span> |<span data-ttu-id="ff606-155">2</span><span class="sxs-lookup"><span data-stu-id="ff606-155">2</span></span> |<span data-ttu-id="ff606-156">4</span><span class="sxs-lookup"><span data-stu-id="ff606-156">4</span></span> |
| <span data-ttu-id="ff606-157">20150701</span><span class="sxs-lookup"><span data-stu-id="ff606-157">20150701</span></span> |<span data-ttu-id="ff606-158">3</span><span class="sxs-lookup"><span data-stu-id="ff606-158">3</span></span> |<span data-ttu-id="ff606-159">1</span><span class="sxs-lookup"><span data-stu-id="ff606-159">1</span></span> |
| <span data-ttu-id="ff606-160">20150801</span><span class="sxs-lookup"><span data-stu-id="ff606-160">20150801</span></span> |<span data-ttu-id="ff606-161">3</span><span class="sxs-lookup"><span data-stu-id="ff606-161">3</span></span> |<span data-ttu-id="ff606-162">1</span><span class="sxs-lookup"><span data-stu-id="ff606-162">1</span></span> |
| <span data-ttu-id="ff606-163">20150801</span><span class="sxs-lookup"><span data-stu-id="ff606-163">20150801</span></span> |<span data-ttu-id="ff606-164">3</span><span class="sxs-lookup"><span data-stu-id="ff606-164">3</span></span> |<span data-ttu-id="ff606-165">1</span><span class="sxs-lookup"><span data-stu-id="ff606-165">1</span></span> |
| <span data-ttu-id="ff606-166">20151001</span><span class="sxs-lookup"><span data-stu-id="ff606-166">20151001</span></span> |<span data-ttu-id="ff606-167">4</span><span class="sxs-lookup"><span data-stu-id="ff606-167">4</span></span> |<span data-ttu-id="ff606-168">2</span><span class="sxs-lookup"><span data-stu-id="ff606-168">2</span></span> |
| <span data-ttu-id="ff606-169">20151101</span><span class="sxs-lookup"><span data-stu-id="ff606-169">20151101</span></span> |<span data-ttu-id="ff606-170">4</span><span class="sxs-lookup"><span data-stu-id="ff606-170">4</span></span> |<span data-ttu-id="ff606-171">2</span><span class="sxs-lookup"><span data-stu-id="ff606-171">2</span></span> |
| <span data-ttu-id="ff606-172">20151201</span><span class="sxs-lookup"><span data-stu-id="ff606-172">20151201</span></span> |<span data-ttu-id="ff606-173">4</span><span class="sxs-lookup"><span data-stu-id="ff606-173">4</span></span> |<span data-ttu-id="ff606-174">2</span><span class="sxs-lookup"><span data-stu-id="ff606-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="ff606-175">4. Statistieken maken</span><span class="sxs-lookup"><span data-stu-id="ff606-175">4. Create statistics</span></span>
<span data-ttu-id="ff606-176">SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="ff606-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="ff606-177">Voor optimale resultaten van uw query's is het belangrijk dat u statistieken maakt voor alle kolommen van alle tabellen nadat de gegevens voor het eerst zijn geladen of wanneer de gegevens substantieel zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="ff606-177">To get the best query performance, it's important to create statistics on all columns of all tables after the first load or after any substantial changes occur in the data.</span></span> <span data-ttu-id="ff606-178">Zie voor een gedetailleerde uitleg van statistieken [statistieken][Statistics].</span><span class="sxs-lookup"><span data-stu-id="ff606-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="ff606-179">Voer de volgende opdracht uit om statistieken te maken voor uw zojuist geladen tabel.</span><span class="sxs-lookup"><span data-stu-id="ff606-179">Run the following command to create statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="ff606-180">5. Gegevens uit SQL Data Warehouse exporteren</span><span class="sxs-lookup"><span data-stu-id="ff606-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="ff606-181">Desgewenst kunt u de gegevens die u zojuist hebt geladen, weer uit SQL Data Warehouse exporteren.</span><span class="sxs-lookup"><span data-stu-id="ff606-181">For fun, you can export the data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="ff606-182">De opdracht voor het exporteren is exact hetzelfde als die voor het exporteren uit SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ff606-182">The command to export is exactly the same as exporting from SQL Server.</span></span>

<span data-ttu-id="ff606-183">De resultaten zijn echter verschillend.</span><span class="sxs-lookup"><span data-stu-id="ff606-183">However, there is a difference in the results.</span></span> <span data-ttu-id="ff606-184">Omdat de gegevens zijn opgeslagen op gedistribueerde locaties in SQL Data Warehouse, worden de gegevens van elk rekenknooppunt bij het exporteren weggeschreven naar het uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="ff606-184">Since the data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data to the output file.</span></span> <span data-ttu-id="ff606-185">De volgorde van de gegevens in het uitvoerbestand is waarschijnlijk anders dan de volgorde van de gegevens in het invoerbestand.</span><span class="sxs-lookup"><span data-stu-id="ff606-185">The order of the data in the output file is likely to be different than the order of the data in the input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="ff606-186">Een tabel exporteren en exportresultaten vergelijken</span><span class="sxs-lookup"><span data-stu-id="ff606-186">Export a table and compare exported results</span></span>
<span data-ttu-id="ff606-187">Om de geëxporteerde gegevens te bekijken, opent u een opdrachtprompt en voert u deze opdracht uit met uw eigen parameters.</span><span class="sxs-lookup"><span data-stu-id="ff606-187">To see the exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="ff606-188">ServerName is de naam van uw logische Azure SQL-server.</span><span class="sxs-lookup"><span data-stu-id="ff606-188">ServerName is the name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="ff606-189">U kunt controleren of de gegevens correct zijn geëxporteerd door het nieuwe bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="ff606-189">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="ff606-190">De gegevens in het bestand moeten overeenkomen met de onderstaande tekst, maar staan waarschijnlijk in een andere volgorde:</span><span class="sxs-lookup"><span data-stu-id="ff606-190">The data in the file should match the text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-the-results-of-a-query"></a><span data-ttu-id="ff606-191">De resultaten van een query exporteren</span><span class="sxs-lookup"><span data-stu-id="ff606-191">Export the results of a query</span></span>
<span data-ttu-id="ff606-192">U kunt de functie **queryout** van BCP gebruiken om de resultaten van een query te exporteren in plaats van de hele tabel te exporteren.</span><span class="sxs-lookup"><span data-stu-id="ff606-192">You can use the **queryout** function of bcp to export the results of a query instead of exporting the entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ff606-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ff606-193">Next steps</span></span>
<span data-ttu-id="ff606-194">Zie [Gegevens laden in SQL Data Warehouse][Load data into SQL Data Warehouse] voor een overzicht van het laden.</span><span class="sxs-lookup"><span data-stu-id="ff606-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="ff606-195">Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="ff606-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="ff606-196">Zie [tabel overzicht] [ Table Overview] of [syntaxis voor CREATE TABLE] [ CREATE TABLE syntax] voor meer informatie over het maken van een tabel in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ff606-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

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
