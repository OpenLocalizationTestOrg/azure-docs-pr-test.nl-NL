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
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="87797-103">Gegevens uit SQL Server laden in Azure SQL Data Warehouse (platte bestanden)</span><span class="sxs-lookup"><span data-stu-id="87797-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="87797-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="87797-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="87797-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="87797-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="87797-106">bcp</span><span class="sxs-lookup"><span data-stu-id="87797-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="87797-107">U kunt voor kleine gegevenssets Hallo bcp opdrachtregelprogramma tooexport gegevens uit SQL Server gebruiken en deze direct tooAzure SQL Data Warehouse laden.</span><span class="sxs-lookup"><span data-stu-id="87797-107">For small data sets, you can use hello bcp command-line utility tooexport data from SQL Server and then load it directly tooAzure SQL Data Warehouse.</span></span>

<span data-ttu-id="87797-108">In deze zelfstudie gebruikt u BCP voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="87797-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="87797-109">Een tabel uit exporteren uit SQL Server met behulp van Hallo opdracht out in bcp (of een eenvoudig voorbeeldbestand maken)</span><span class="sxs-lookup"><span data-stu-id="87797-109">Export a table from from SQL Server by using hello bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="87797-110">Hallo tabel importeren uit een plat bestand-tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="87797-110">Import hello table from a flat file tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="87797-111">Statistieken maken voor Hallo geladen gegevens.</span><span class="sxs-lookup"><span data-stu-id="87797-111">Create statistics on hello loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="87797-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="87797-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="87797-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="87797-113">Prerequisites</span></span>
<span data-ttu-id="87797-114">toostep voor deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="87797-114">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="87797-115">Een SQL Data Warehouse-database</span><span class="sxs-lookup"><span data-stu-id="87797-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="87797-116">Hallo opdrachtregelprogramma bcp geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="87797-116">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="87797-117">Hallo sqlcmd-opdrachtregelprogramma geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="87797-117">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="87797-118">U kunt hulpprogramma's voor Hallo bcp en sqlcmd downloaden van Hallo [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="87797-118">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="87797-119">Gegevens in ASCII- of UTF-16-indeling</span><span class="sxs-lookup"><span data-stu-id="87797-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="87797-120">Als u deze zelfstudie met uw eigen gegevens probeert, moet uw gegevens toouse Hallo ASCII- of UTF-16 omdat bcp biedt geen ondersteuning voor UTF-8-codering.</span><span class="sxs-lookup"><span data-stu-id="87797-120">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="87797-121">UTF-8 wordt wel ondersteund in PolyBase, maar UTF-16 nog niet.</span><span class="sxs-lookup"><span data-stu-id="87797-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="87797-122">Houd er rekening mee dat als u wilt dat toocombine bcp met PolyBase u tootransform Hallo gegevens tooUTF-8 moet na het exporteren uit SQL Server.</span><span class="sxs-lookup"><span data-stu-id="87797-122">Note that if you want toocombine bcp with PolyBase you will need tootransform hello data tooUTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="87797-123">1. Een doeltabel maken</span><span class="sxs-lookup"><span data-stu-id="87797-123">1. Create a destination table</span></span>
<span data-ttu-id="87797-124">Definieer een tabel in SQL Data Warehouse die Hallo doeltabel voor Hallo belasting.</span><span class="sxs-lookup"><span data-stu-id="87797-124">Define a table in SQL Data Warehouse that will be hello destination table for hello load.</span></span> <span data-ttu-id="87797-125">Hallo-kolommen in tabel Hallo moeten overeenkomen met toohello gegevens in elke rij van het gegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="87797-125">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="87797-126">toocreate een tabel, open een opdrachtprompt en sqlcmd.exe toorun Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="87797-126">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="87797-127">2. Een brongegevensbestand maken</span><span class="sxs-lookup"><span data-stu-id="87797-127">2. Create a source data file</span></span>
<span data-ttu-id="87797-128">Open Kladblok en kopieer Hallo volgende regels van gegevens naar een nieuw tekstbestand en sla dit bestand tooyour lokale tijdelijke map C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="87797-128">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="87797-129">Dit zijn gegevens in ASCII-indeling.</span><span class="sxs-lookup"><span data-stu-id="87797-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="87797-130">(Optioneel) tooexport uw eigen gegevens uit een SQL Server-database, open een opdrachtprompt en Voer Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="87797-130">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="87797-131">Vervang TableName, ServerName, DatabaseName, Username en Password door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="87797-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a><span data-ttu-id="87797-132">3. Hallo gegevens laden</span><span class="sxs-lookup"><span data-stu-id="87797-132">3. Load hello data</span></span>
<span data-ttu-id="87797-133">tooload hello gegevens, open een opdrachtprompt en Voer Hallo de volgende opdracht, Hallo waarden voor de servernaam, Database-naam, gebruikersnaam en wachtwoord worden vervangen door uw eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="87797-133">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="87797-134">Gebruik die deze opdracht tooverify Hallo gegevens correct zijn geladen</span><span class="sxs-lookup"><span data-stu-id="87797-134">Use this command tooverify hello data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="87797-135">Hallo resultaten er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="87797-135">hello results should look like this:</span></span>

| <span data-ttu-id="87797-136">DateId</span><span class="sxs-lookup"><span data-stu-id="87797-136">DateId</span></span> | <span data-ttu-id="87797-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="87797-137">CalendarQuarter</span></span> | <span data-ttu-id="87797-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="87797-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="87797-139">20150101</span><span class="sxs-lookup"><span data-stu-id="87797-139">20150101</span></span> |<span data-ttu-id="87797-140">1</span><span class="sxs-lookup"><span data-stu-id="87797-140">1</span></span> |<span data-ttu-id="87797-141">3</span><span class="sxs-lookup"><span data-stu-id="87797-141">3</span></span> |
| <span data-ttu-id="87797-142">20150201</span><span class="sxs-lookup"><span data-stu-id="87797-142">20150201</span></span> |<span data-ttu-id="87797-143">1</span><span class="sxs-lookup"><span data-stu-id="87797-143">1</span></span> |<span data-ttu-id="87797-144">3</span><span class="sxs-lookup"><span data-stu-id="87797-144">3</span></span> |
| <span data-ttu-id="87797-145">20150301</span><span class="sxs-lookup"><span data-stu-id="87797-145">20150301</span></span> |<span data-ttu-id="87797-146">1</span><span class="sxs-lookup"><span data-stu-id="87797-146">1</span></span> |<span data-ttu-id="87797-147">3</span><span class="sxs-lookup"><span data-stu-id="87797-147">3</span></span> |
| <span data-ttu-id="87797-148">20150401</span><span class="sxs-lookup"><span data-stu-id="87797-148">20150401</span></span> |<span data-ttu-id="87797-149">2</span><span class="sxs-lookup"><span data-stu-id="87797-149">2</span></span> |<span data-ttu-id="87797-150">4</span><span class="sxs-lookup"><span data-stu-id="87797-150">4</span></span> |
| <span data-ttu-id="87797-151">20150501</span><span class="sxs-lookup"><span data-stu-id="87797-151">20150501</span></span> |<span data-ttu-id="87797-152">2</span><span class="sxs-lookup"><span data-stu-id="87797-152">2</span></span> |<span data-ttu-id="87797-153">4</span><span class="sxs-lookup"><span data-stu-id="87797-153">4</span></span> |
| <span data-ttu-id="87797-154">20150601</span><span class="sxs-lookup"><span data-stu-id="87797-154">20150601</span></span> |<span data-ttu-id="87797-155">2</span><span class="sxs-lookup"><span data-stu-id="87797-155">2</span></span> |<span data-ttu-id="87797-156">4</span><span class="sxs-lookup"><span data-stu-id="87797-156">4</span></span> |
| <span data-ttu-id="87797-157">20150701</span><span class="sxs-lookup"><span data-stu-id="87797-157">20150701</span></span> |<span data-ttu-id="87797-158">3</span><span class="sxs-lookup"><span data-stu-id="87797-158">3</span></span> |<span data-ttu-id="87797-159">1</span><span class="sxs-lookup"><span data-stu-id="87797-159">1</span></span> |
| <span data-ttu-id="87797-160">20150801</span><span class="sxs-lookup"><span data-stu-id="87797-160">20150801</span></span> |<span data-ttu-id="87797-161">3</span><span class="sxs-lookup"><span data-stu-id="87797-161">3</span></span> |<span data-ttu-id="87797-162">1</span><span class="sxs-lookup"><span data-stu-id="87797-162">1</span></span> |
| <span data-ttu-id="87797-163">20150801</span><span class="sxs-lookup"><span data-stu-id="87797-163">20150801</span></span> |<span data-ttu-id="87797-164">3</span><span class="sxs-lookup"><span data-stu-id="87797-164">3</span></span> |<span data-ttu-id="87797-165">1</span><span class="sxs-lookup"><span data-stu-id="87797-165">1</span></span> |
| <span data-ttu-id="87797-166">20151001</span><span class="sxs-lookup"><span data-stu-id="87797-166">20151001</span></span> |<span data-ttu-id="87797-167">4</span><span class="sxs-lookup"><span data-stu-id="87797-167">4</span></span> |<span data-ttu-id="87797-168">2</span><span class="sxs-lookup"><span data-stu-id="87797-168">2</span></span> |
| <span data-ttu-id="87797-169">20151101</span><span class="sxs-lookup"><span data-stu-id="87797-169">20151101</span></span> |<span data-ttu-id="87797-170">4</span><span class="sxs-lookup"><span data-stu-id="87797-170">4</span></span> |<span data-ttu-id="87797-171">2</span><span class="sxs-lookup"><span data-stu-id="87797-171">2</span></span> |
| <span data-ttu-id="87797-172">20151201</span><span class="sxs-lookup"><span data-stu-id="87797-172">20151201</span></span> |<span data-ttu-id="87797-173">4</span><span class="sxs-lookup"><span data-stu-id="87797-173">4</span></span> |<span data-ttu-id="87797-174">2</span><span class="sxs-lookup"><span data-stu-id="87797-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="87797-175">4. Statistieken maken</span><span class="sxs-lookup"><span data-stu-id="87797-175">4. Create statistics</span></span>
<span data-ttu-id="87797-176">SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="87797-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="87797-177">tooget hello beste prestaties van query's, is belangrijk toocreate statistieken voor alle kolommen van alle tabellen na Hallo eerst zijn geladen of nadat belangrijke wijzigingen in Hallo-gegevens plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="87797-177">tooget hello best query performance, it's important toocreate statistics on all columns of all tables after hello first load or after any substantial changes occur in hello data.</span></span> <span data-ttu-id="87797-178">Zie voor een gedetailleerde uitleg van statistieken [statistieken][Statistics].</span><span class="sxs-lookup"><span data-stu-id="87797-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="87797-179">Voer Hallo opdracht toocreate statistieken op uw zojuist geladen tabel te volgen.</span><span class="sxs-lookup"><span data-stu-id="87797-179">Run hello following command toocreate statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="87797-180">5. Gegevens uit SQL Data Warehouse exporteren</span><span class="sxs-lookup"><span data-stu-id="87797-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="87797-181">U kunt desgewenst Hallo-gegevens die u zojuist hebt geladen, weer uit SQL Data Warehouse exporteren.</span><span class="sxs-lookup"><span data-stu-id="87797-181">For fun, you can export hello data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="87797-182">Hallo opdracht tooexport is precies hetzelfde als het exporteren uit SQL Server Hallo.</span><span class="sxs-lookup"><span data-stu-id="87797-182">hello command tooexport is exactly hello same as exporting from SQL Server.</span></span>

<span data-ttu-id="87797-183">Er is echter een verschil in Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="87797-183">However, there is a difference in hello results.</span></span> <span data-ttu-id="87797-184">Aangezien het Hallo-gegevens worden opgeslagen op gedistribueerde locaties in SQL Data Warehouse, wanneer u gegevens exporteren schrijft deze elk rekenknooppunt gegevens toohello-uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="87797-184">Since hello data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data toohello output file.</span></span> <span data-ttu-id="87797-185">Hallo-volgorde van Hallo-gegevens in het Hallo-uitvoerbestand is waarschijnlijk anders dan de volgorde van gegevens in het invoerbestand Hallo HALLO hallo toobe.</span><span class="sxs-lookup"><span data-stu-id="87797-185">hello order of hello data in hello output file is likely toobe different than hello order of hello data in hello input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="87797-186">Een tabel exporteren en exportresultaten vergelijken</span><span class="sxs-lookup"><span data-stu-id="87797-186">Export a table and compare exported results</span></span>
<span data-ttu-id="87797-187">toosee Hallo geëxporteerde gegevens, open een opdrachtprompt en voer deze opdracht met uw eigen parameters.</span><span class="sxs-lookup"><span data-stu-id="87797-187">toosee hello exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="87797-188">ServerName is Hallo-naam van uw logische Azure SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="87797-188">ServerName is hello name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="87797-189">U kunt controleren of Hallo gegevens correct zijn geëxporteerd door nieuwe Hallo-bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="87797-189">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="87797-190">Hallo-gegevens in Hallo-bestand moet overeenkomen met de onderstaande Hallo tekst, maar waarschijnlijk in een andere volgorde worden gesorteerd:</span><span class="sxs-lookup"><span data-stu-id="87797-190">hello data in hello file should match hello text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-hello-results-of-a-query"></a><span data-ttu-id="87797-191">Hallo-resultaten van een query exporteren</span><span class="sxs-lookup"><span data-stu-id="87797-191">Export hello results of a query</span></span>
<span data-ttu-id="87797-192">U kunt Hallo **queryout** functie van bcp tooexport Hallo resultaten van een query in plaats van de gehele tabel Hallo exporteren.</span><span class="sxs-lookup"><span data-stu-id="87797-192">You can use hello **queryout** function of bcp tooexport hello results of a query instead of exporting hello entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="87797-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="87797-193">Next steps</span></span>
<span data-ttu-id="87797-194">Zie [Gegevens laden in SQL Data Warehouse][Load data into SQL Data Warehouse] voor een overzicht van het laden.</span><span class="sxs-lookup"><span data-stu-id="87797-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="87797-195">Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="87797-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="87797-196">Zie [tabel overzicht] [ Table Overview] of [syntaxis voor CREATE TABLE] [ CREATE TABLE syntax] voor meer informatie over het maken van een tabel in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="87797-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

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
