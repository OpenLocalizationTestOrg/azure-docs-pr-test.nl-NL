---
title: Gegevens laden in SQL Data Warehouse met behulp van BCP | Microsoft Docs
description: Informatie over BCP en het gebruik van BCP voor datawarehousescenario's.
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
ms.openlocfilehash: 7596eac10fdf53380d85128265430ce07b551fe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="99f81-103">Gegevens laden met bcp</span><span class="sxs-lookup"><span data-stu-id="99f81-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="99f81-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="99f81-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="99f81-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="99f81-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="99f81-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="99f81-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="99f81-107">BCP</span><span class="sxs-lookup"><span data-stu-id="99f81-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="99f81-108">**[BCP][bcp]** is een opdrachtregelprogramma voor het bulksgewijs laden van gegevens. Hiermee kunt u gegevens kopiëren van en naar SQL Server, gegevensbestanden en SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="99f81-108">**[bcp][bcp]** is a command-line bulk load utility that allows you to copy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="99f81-109">Gebruikt BCP om veel rijen in SQL Data Warehouse-tabellen te importeren of gegevens uit SQL Server-tabellen te exporteren naar gegevensbestanden.</span><span class="sxs-lookup"><span data-stu-id="99f81-109">Use bcp to import large numbers of rows into SQL Data Warehouse tables or to export data from SQL Server tables into data files.</span></span> <span data-ttu-id="99f81-110">Voor het gebruik van BCP is geen kennis van Transact-SQL vereist, behalve wanneer u de optie queryout wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="99f81-110">Except when used with the queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="99f81-111">Met BCP kunt u snel en eenvoudig kleinere gegevenssets verplaatsen van en naar een SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="99f81-111">bcp is a quick and easy way to move smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="99f81-112">De exacte aanbevolen hoeveelheid gegevens die u kunt laden/extraheren met BCP is afhankelijk van uw netwerkverbinding met het Azure-datacentrum.</span><span class="sxs-lookup"><span data-stu-id="99f81-112">The exact amount of data that is recommended to load/extract via bcp will depend on you network connection to the Azure data center.</span></span>  <span data-ttu-id="99f81-113">Over het algemeen kunt u dimensietabellen probleemloos laden en extraheren met BCP. Voor grote hoeveelheden gegevens wordt BCP echter niet aangeraden.</span><span class="sxs-lookup"><span data-stu-id="99f81-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="99f81-114">Als u veel gegevens wilt laden en extraheren, kunt u het beste Polybase gebruiken. Dit hulpprogramma is beter geschikt voor de uitgebreide parallelle verwerkingsarchitectuur van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="99f81-114">Polybase is the recommended tool for loading and extracting large volumes of data as it does a better job leveraging the massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="99f81-115">Met BCP kunt u:</span><span class="sxs-lookup"><span data-stu-id="99f81-115">With bcp you can:</span></span>

* <span data-ttu-id="99f81-116">Gegevens in SQL Data Warehouse laden met behulp van een eenvoudig opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="99f81-116">Use a simple command-line utility to load data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="99f81-117">Gegevens uit SQL Data Warehouse extraheren met behulp van een eenvoudig opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="99f81-117">Use a simple command-line utility to extract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="99f81-118">In deze zelfstudie leert u hoe u het volgende kunt doen:</span><span class="sxs-lookup"><span data-stu-id="99f81-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="99f81-119">Gegevens importeren in een tabel met behulp van de BCP-opdracht in</span><span class="sxs-lookup"><span data-stu-id="99f81-119">Import data into a table using the bcp in command</span></span>
* <span data-ttu-id="99f81-120">Gegevens exporteren uit een tabel met behulp van de BCP-opdracht out</span><span class="sxs-lookup"><span data-stu-id="99f81-120">Export data from a table uisng the bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="99f81-121">Vereisten</span><span class="sxs-lookup"><span data-stu-id="99f81-121">Prerequisites</span></span>
<span data-ttu-id="99f81-122">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="99f81-122">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="99f81-123">Een SQL Data Warehouse-database</span><span class="sxs-lookup"><span data-stu-id="99f81-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="99f81-124">Het opdrachtregelprogramma BCP (moet zijn geïnstalleerd)</span><span class="sxs-lookup"><span data-stu-id="99f81-124">The bcp command line utility installed</span></span>
* <span data-ttu-id="99f81-125">Het opdrachtregelprogramma SQLCMD (moet zijn geïnstalleerd)</span><span class="sxs-lookup"><span data-stu-id="99f81-125">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="99f81-126">U kunt de opdrachtregelprogramma's BCP en SQLCMD downloaden van het [Microsoft Downloadcentrum][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="99f81-126">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="99f81-127">Gegevens importeren in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="99f81-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="99f81-128">In deze zelfstudie maakt u een tabel in Azure SQL Data Warehouse en importeert u gegevens in de tabel.</span><span class="sxs-lookup"><span data-stu-id="99f81-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="99f81-129">Stap 1: een tabel maken in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="99f81-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="99f81-130">Open een opdrachtprompt en voer de volgende query voor het maken van een tabel op uw exemplaar uit met SQLCMD:</span><span class="sxs-lookup"><span data-stu-id="99f81-130">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

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
> <span data-ttu-id="99f81-131">Zie [Tabeloverzicht][Table Overview] of [Syntaxis voor CREATE TABLE][CREATE TABLE syntax] voor meer informatie over het maken van een tabel in SQL Data Warehouse en de beschikbare opties in de WITH-clausule.</span><span class="sxs-lookup"><span data-stu-id="99f81-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="99f81-132">Stap 2: een brongegevensbestand maken</span><span class="sxs-lookup"><span data-stu-id="99f81-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="99f81-133">Open Kladblok, kopieer de volgende regels met gegevens naar een nieuw tekstbestand en sla dit bestand op in de lokale tijdelijke map C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="99f81-133">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="99f81-134">Denk eraan dat de bestandscodering UTF-8 niet wordt ondersteund in bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="99f81-134">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="99f81-135">Gebruik ASCII-bestanden of bestanden met de bestandscodering UTF-16 als u bcp.exe gebruikt.</span><span class="sxs-lookup"><span data-stu-id="99f81-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="99f81-136">Stap 3: verbinding maken en de gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="99f81-136">Step 3: Connect and import the data</span></span>
<span data-ttu-id="99f81-137">Met BCP kunt u verbinding maken en de gegevens importeren met de volgende opdracht, waarbij u de waarden waar nodig vervangt:</span><span class="sxs-lookup"><span data-stu-id="99f81-137">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="99f81-138">U kunt controleren of de gegevens zijn geladen door de volgende query uit te voeren met SQLCMD:</span><span class="sxs-lookup"><span data-stu-id="99f81-138">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="99f81-139">Hierdoor zouden de volgende resultaten moeten worden geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="99f81-139">This should return the following results:</span></span>

| <span data-ttu-id="99f81-140">DateId</span><span class="sxs-lookup"><span data-stu-id="99f81-140">DateId</span></span> | <span data-ttu-id="99f81-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="99f81-141">CalendarQuarter</span></span> | <span data-ttu-id="99f81-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="99f81-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99f81-143">20150101</span><span class="sxs-lookup"><span data-stu-id="99f81-143">20150101</span></span> |<span data-ttu-id="99f81-144">1</span><span class="sxs-lookup"><span data-stu-id="99f81-144">1</span></span> |<span data-ttu-id="99f81-145">3</span><span class="sxs-lookup"><span data-stu-id="99f81-145">3</span></span> |
| <span data-ttu-id="99f81-146">20150201</span><span class="sxs-lookup"><span data-stu-id="99f81-146">20150201</span></span> |<span data-ttu-id="99f81-147">1</span><span class="sxs-lookup"><span data-stu-id="99f81-147">1</span></span> |<span data-ttu-id="99f81-148">3</span><span class="sxs-lookup"><span data-stu-id="99f81-148">3</span></span> |
| <span data-ttu-id="99f81-149">20150301</span><span class="sxs-lookup"><span data-stu-id="99f81-149">20150301</span></span> |<span data-ttu-id="99f81-150">1</span><span class="sxs-lookup"><span data-stu-id="99f81-150">1</span></span> |<span data-ttu-id="99f81-151">3</span><span class="sxs-lookup"><span data-stu-id="99f81-151">3</span></span> |
| <span data-ttu-id="99f81-152">20150401</span><span class="sxs-lookup"><span data-stu-id="99f81-152">20150401</span></span> |<span data-ttu-id="99f81-153">2</span><span class="sxs-lookup"><span data-stu-id="99f81-153">2</span></span> |<span data-ttu-id="99f81-154">4</span><span class="sxs-lookup"><span data-stu-id="99f81-154">4</span></span> |
| <span data-ttu-id="99f81-155">20150501</span><span class="sxs-lookup"><span data-stu-id="99f81-155">20150501</span></span> |<span data-ttu-id="99f81-156">2</span><span class="sxs-lookup"><span data-stu-id="99f81-156">2</span></span> |<span data-ttu-id="99f81-157">4</span><span class="sxs-lookup"><span data-stu-id="99f81-157">4</span></span> |
| <span data-ttu-id="99f81-158">20150601</span><span class="sxs-lookup"><span data-stu-id="99f81-158">20150601</span></span> |<span data-ttu-id="99f81-159">2</span><span class="sxs-lookup"><span data-stu-id="99f81-159">2</span></span> |<span data-ttu-id="99f81-160">4</span><span class="sxs-lookup"><span data-stu-id="99f81-160">4</span></span> |
| <span data-ttu-id="99f81-161">20150701</span><span class="sxs-lookup"><span data-stu-id="99f81-161">20150701</span></span> |<span data-ttu-id="99f81-162">3</span><span class="sxs-lookup"><span data-stu-id="99f81-162">3</span></span> |<span data-ttu-id="99f81-163">1</span><span class="sxs-lookup"><span data-stu-id="99f81-163">1</span></span> |
| <span data-ttu-id="99f81-164">20150801</span><span class="sxs-lookup"><span data-stu-id="99f81-164">20150801</span></span> |<span data-ttu-id="99f81-165">3</span><span class="sxs-lookup"><span data-stu-id="99f81-165">3</span></span> |<span data-ttu-id="99f81-166">1</span><span class="sxs-lookup"><span data-stu-id="99f81-166">1</span></span> |
| <span data-ttu-id="99f81-167">20150801</span><span class="sxs-lookup"><span data-stu-id="99f81-167">20150801</span></span> |<span data-ttu-id="99f81-168">3</span><span class="sxs-lookup"><span data-stu-id="99f81-168">3</span></span> |<span data-ttu-id="99f81-169">1</span><span class="sxs-lookup"><span data-stu-id="99f81-169">1</span></span> |
| <span data-ttu-id="99f81-170">20151001</span><span class="sxs-lookup"><span data-stu-id="99f81-170">20151001</span></span> |<span data-ttu-id="99f81-171">4</span><span class="sxs-lookup"><span data-stu-id="99f81-171">4</span></span> |<span data-ttu-id="99f81-172">2</span><span class="sxs-lookup"><span data-stu-id="99f81-172">2</span></span> |
| <span data-ttu-id="99f81-173">20151101</span><span class="sxs-lookup"><span data-stu-id="99f81-173">20151101</span></span> |<span data-ttu-id="99f81-174">4</span><span class="sxs-lookup"><span data-stu-id="99f81-174">4</span></span> |<span data-ttu-id="99f81-175">2</span><span class="sxs-lookup"><span data-stu-id="99f81-175">2</span></span> |
| <span data-ttu-id="99f81-176">20151201</span><span class="sxs-lookup"><span data-stu-id="99f81-176">20151201</span></span> |<span data-ttu-id="99f81-177">4</span><span class="sxs-lookup"><span data-stu-id="99f81-177">4</span></span> |<span data-ttu-id="99f81-178">2</span><span class="sxs-lookup"><span data-stu-id="99f81-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="99f81-179">Stap 4: statistieken maken voor uw zojuist geladen gegevens</span><span class="sxs-lookup"><span data-stu-id="99f81-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="99f81-180">Azure SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="99f81-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="99f81-181">Voor optimale resultaten van uw query's is het belangrijk dat u statistieken maakt voor alle kolommen van alle tabellen nadat de gegevens voor het eerst zijn geladen of wanneer de gegevens substantieel zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="99f81-181">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="99f81-182">Zie het onderwerp [Statistieken][Statistics] in de groep onderwerpen voor ontwikkelaars voor gedetailleerde uitleg van statistieken.</span><span class="sxs-lookup"><span data-stu-id="99f81-182">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="99f81-183">Hieronder ziet u een kort voorbeeld van het maken van statistieken voor de tabellen die zijn geladen in dit voorbeeld</span><span class="sxs-lookup"><span data-stu-id="99f81-183">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="99f81-184">Voer de volgende CREATE STATISTICS-instructies uit vanaf een SQLCMD-opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="99f81-184">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="99f81-185">Gegevens uit SQL Data Warehouse exporteren</span><span class="sxs-lookup"><span data-stu-id="99f81-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="99f81-186">In deze zelfstudie maakt u een gegevensbestand op basis van een tabel in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="99f81-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="99f81-187">U exporteert de eerder gemaakte gegevens naar een nieuw gegevensbestand met de naam DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="99f81-187">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="99f81-188">Stap 1: de gegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="99f81-188">Step 1: Export the data</span></span>
<span data-ttu-id="99f81-189">Met het hulpprogramma BCP kunt u verbinding maken en gegevens exporteren met de volgende opdracht, waarbij u de waarden waar nodig vervangt:</span><span class="sxs-lookup"><span data-stu-id="99f81-189">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="99f81-190">U kunt controleren of de gegevens correct zijn geëxporteerd door het nieuwe bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="99f81-190">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="99f81-191">De gegevens in het bestand moeten overeenkomen met de onderstaande tekst:</span><span class="sxs-lookup"><span data-stu-id="99f81-191">The data in the file should match the text below:</span></span>

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
> <span data-ttu-id="99f81-192">Vanwege de aard van gedistribueerde systemen kan de gegevensvolgorde per SQL Data Warehouse-database verschillen.</span><span class="sxs-lookup"><span data-stu-id="99f81-192">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="99f81-193">In plaats van de hele tabel te exporteren kunt u ook een query voor het extraheren van gegevens schrijven met de functie **queryout** van BCP.</span><span class="sxs-lookup"><span data-stu-id="99f81-193">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="99f81-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99f81-194">Next steps</span></span>
<span data-ttu-id="99f81-195">Zie [Gegevens laden in SQL Data Warehouse][Load data into SQL Data Warehouse] voor een overzicht van het laden.</span><span class="sxs-lookup"><span data-stu-id="99f81-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="99f81-196">Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="99f81-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
