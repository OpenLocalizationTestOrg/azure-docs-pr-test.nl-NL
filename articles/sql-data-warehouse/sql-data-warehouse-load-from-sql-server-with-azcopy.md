---
title: Gegevens uit SQL Server laden in Azure SQL Data Warehouse (PolyBase) | Microsoft Docs
description: Gebruikt bcp om gegevens uit SQL Server te exporteren naar platte bestanden, AZCopy om gegevens te importeren in een Azure Blob Storage en PolyBase om de gegevens op te nemen in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 08f94bc26d8b1e1f5a56dfccd41e394dbd721024
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="82839-103">Gegevens uit SQL Server laden in Azure SQL Data Warehouse (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="82839-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="82839-104">Gebruik de opdrachtregelprogramma's BCP en AZCopy om gegevens uit SQL Server te laden in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="82839-104">Use bcp and AZCopy command-line utilities to load data from SQL Server to Azure blob storage.</span></span> <span data-ttu-id="82839-105">Gebruik vervolgens PolyBase of Azure Data Factory om de gegevens in Azure SQL Data Warehouse te laden.</span><span class="sxs-lookup"><span data-stu-id="82839-105">Then use PolyBase or Azure Data Factory to load the data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="82839-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="82839-106">Prerequisites</span></span>
<span data-ttu-id="82839-107">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="82839-107">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="82839-108">Een SQL Data Warehouse-database</span><span class="sxs-lookup"><span data-stu-id="82839-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="82839-109">Het opdrachtregelprogramma BCP (moet zijn geïnstalleerd)</span><span class="sxs-lookup"><span data-stu-id="82839-109">The bcp command line utility installed</span></span>
* <span data-ttu-id="82839-110">Het opdrachtregelprogramma SQLCMD (moet zijn geïnstalleerd)</span><span class="sxs-lookup"><span data-stu-id="82839-110">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="82839-111">U kunt de opdrachtregelprogramma's BCP en SQLCMD downloaden van het [Microsoft Downloadcentrum][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="82839-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="82839-112">Gegevens importeren in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="82839-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="82839-113">In deze zelfstudie maakt u een tabel in Azure SQL Data Warehouse en importeert u gegevens in de tabel.</span><span class="sxs-lookup"><span data-stu-id="82839-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="82839-114">Stap 1: een tabel maken in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="82839-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="82839-115">Open een opdrachtprompt en voer de volgende query voor het maken van een tabel op uw exemplaar uit met SQLCMD:</span><span class="sxs-lookup"><span data-stu-id="82839-115">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

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
> <span data-ttu-id="82839-116">Zie [Tabeloverzicht][Table Overview] of [Syntaxis voor CREATE TABLE][CREATE TABLE syntax] voor meer informatie over het maken van een tabel in SQL Data Warehouse en de beschikbare opties in de WITH-clausule.</span><span class="sxs-lookup"><span data-stu-id="82839-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="82839-117">Stap 2: een brongegevensbestand maken</span><span class="sxs-lookup"><span data-stu-id="82839-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="82839-118">Open Kladblok, kopieer de volgende regels met gegevens naar een nieuw tekstbestand en sla dit bestand op in de lokale tijdelijke map C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="82839-118">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="82839-119">Denk eraan dat de bestandscodering UTF-8 niet wordt ondersteund in bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="82839-119">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="82839-120">Gebruik ASCII-bestanden of bestanden met de bestandscodering UTF-16 als u bcp.exe gebruikt.</span><span class="sxs-lookup"><span data-stu-id="82839-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="82839-121">Stap 3: verbinding maken en de gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="82839-121">Step 3: Connect and import the data</span></span>
<span data-ttu-id="82839-122">Met BCP kunt u verbinding maken en de gegevens importeren met de volgende opdracht, waarbij u de waarden waar nodig vervangt:</span><span class="sxs-lookup"><span data-stu-id="82839-122">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="82839-123">U kunt controleren of de gegevens zijn geladen door de volgende query uit te voeren met SQLCMD:</span><span class="sxs-lookup"><span data-stu-id="82839-123">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="82839-124">Hierdoor zouden de volgende resultaten moeten worden geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="82839-124">This should return the following results:</span></span>

| <span data-ttu-id="82839-125">DateId</span><span class="sxs-lookup"><span data-stu-id="82839-125">DateId</span></span> | <span data-ttu-id="82839-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="82839-126">CalendarQuarter</span></span> | <span data-ttu-id="82839-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="82839-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82839-128">20150101</span><span class="sxs-lookup"><span data-stu-id="82839-128">20150101</span></span> |<span data-ttu-id="82839-129">1</span><span class="sxs-lookup"><span data-stu-id="82839-129">1</span></span> |<span data-ttu-id="82839-130">3</span><span class="sxs-lookup"><span data-stu-id="82839-130">3</span></span> |
| <span data-ttu-id="82839-131">20150201</span><span class="sxs-lookup"><span data-stu-id="82839-131">20150201</span></span> |<span data-ttu-id="82839-132">1</span><span class="sxs-lookup"><span data-stu-id="82839-132">1</span></span> |<span data-ttu-id="82839-133">3</span><span class="sxs-lookup"><span data-stu-id="82839-133">3</span></span> |
| <span data-ttu-id="82839-134">20150301</span><span class="sxs-lookup"><span data-stu-id="82839-134">20150301</span></span> |<span data-ttu-id="82839-135">1</span><span class="sxs-lookup"><span data-stu-id="82839-135">1</span></span> |<span data-ttu-id="82839-136">3</span><span class="sxs-lookup"><span data-stu-id="82839-136">3</span></span> |
| <span data-ttu-id="82839-137">20150401</span><span class="sxs-lookup"><span data-stu-id="82839-137">20150401</span></span> |<span data-ttu-id="82839-138">2</span><span class="sxs-lookup"><span data-stu-id="82839-138">2</span></span> |<span data-ttu-id="82839-139">4</span><span class="sxs-lookup"><span data-stu-id="82839-139">4</span></span> |
| <span data-ttu-id="82839-140">20150501</span><span class="sxs-lookup"><span data-stu-id="82839-140">20150501</span></span> |<span data-ttu-id="82839-141">2</span><span class="sxs-lookup"><span data-stu-id="82839-141">2</span></span> |<span data-ttu-id="82839-142">4</span><span class="sxs-lookup"><span data-stu-id="82839-142">4</span></span> |
| <span data-ttu-id="82839-143">20150601</span><span class="sxs-lookup"><span data-stu-id="82839-143">20150601</span></span> |<span data-ttu-id="82839-144">2</span><span class="sxs-lookup"><span data-stu-id="82839-144">2</span></span> |<span data-ttu-id="82839-145">4</span><span class="sxs-lookup"><span data-stu-id="82839-145">4</span></span> |
| <span data-ttu-id="82839-146">20150701</span><span class="sxs-lookup"><span data-stu-id="82839-146">20150701</span></span> |<span data-ttu-id="82839-147">3</span><span class="sxs-lookup"><span data-stu-id="82839-147">3</span></span> |<span data-ttu-id="82839-148">1</span><span class="sxs-lookup"><span data-stu-id="82839-148">1</span></span> |
| <span data-ttu-id="82839-149">20150801</span><span class="sxs-lookup"><span data-stu-id="82839-149">20150801</span></span> |<span data-ttu-id="82839-150">3</span><span class="sxs-lookup"><span data-stu-id="82839-150">3</span></span> |<span data-ttu-id="82839-151">1</span><span class="sxs-lookup"><span data-stu-id="82839-151">1</span></span> |
| <span data-ttu-id="82839-152">20150801</span><span class="sxs-lookup"><span data-stu-id="82839-152">20150801</span></span> |<span data-ttu-id="82839-153">3</span><span class="sxs-lookup"><span data-stu-id="82839-153">3</span></span> |<span data-ttu-id="82839-154">1</span><span class="sxs-lookup"><span data-stu-id="82839-154">1</span></span> |
| <span data-ttu-id="82839-155">20151001</span><span class="sxs-lookup"><span data-stu-id="82839-155">20151001</span></span> |<span data-ttu-id="82839-156">4</span><span class="sxs-lookup"><span data-stu-id="82839-156">4</span></span> |<span data-ttu-id="82839-157">2</span><span class="sxs-lookup"><span data-stu-id="82839-157">2</span></span> |
| <span data-ttu-id="82839-158">20151101</span><span class="sxs-lookup"><span data-stu-id="82839-158">20151101</span></span> |<span data-ttu-id="82839-159">4</span><span class="sxs-lookup"><span data-stu-id="82839-159">4</span></span> |<span data-ttu-id="82839-160">2</span><span class="sxs-lookup"><span data-stu-id="82839-160">2</span></span> |
| <span data-ttu-id="82839-161">20151201</span><span class="sxs-lookup"><span data-stu-id="82839-161">20151201</span></span> |<span data-ttu-id="82839-162">4</span><span class="sxs-lookup"><span data-stu-id="82839-162">4</span></span> |<span data-ttu-id="82839-163">2</span><span class="sxs-lookup"><span data-stu-id="82839-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="82839-164">Stap 4: statistieken maken voor uw zojuist geladen gegevens</span><span class="sxs-lookup"><span data-stu-id="82839-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="82839-165">Azure SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="82839-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="82839-166">Voor optimale resultaten van uw query's is het belangrijk dat u statistieken maakt voor alle kolommen van alle tabellen nadat de gegevens voor het eerst zijn geladen of wanneer de gegevens substantieel zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="82839-166">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="82839-167">Zie het onderwerp [Statistieken][Statistics] in de groep onderwerpen voor ontwikkelaars voor gedetailleerde uitleg van statistieken.</span><span class="sxs-lookup"><span data-stu-id="82839-167">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="82839-168">Hieronder ziet u een kort voorbeeld van het maken van statistieken voor de tabellen die zijn geladen in dit voorbeeld</span><span class="sxs-lookup"><span data-stu-id="82839-168">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="82839-169">Voer de volgende CREATE STATISTICS-instructies uit vanaf een SQLCMD-opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="82839-169">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="82839-170">Gegevens uit SQL Data Warehouse exporteren</span><span class="sxs-lookup"><span data-stu-id="82839-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="82839-171">In deze zelfstudie maakt u een gegevensbestand op basis van een tabel in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="82839-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="82839-172">U exporteert de eerder gemaakte gegevens naar een nieuw gegevensbestand met de naam DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="82839-172">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="82839-173">Stap 1: de gegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="82839-173">Step 1: Export the data</span></span>
<span data-ttu-id="82839-174">Met het hulpprogramma BCP kunt u verbinding maken en gegevens exporteren met de volgende opdracht, waarbij u de waarden waar nodig vervangt:</span><span class="sxs-lookup"><span data-stu-id="82839-174">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="82839-175">U kunt controleren of de gegevens correct zijn geëxporteerd door het nieuwe bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="82839-175">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="82839-176">De gegevens in het bestand moeten overeenkomen met de onderstaande tekst:</span><span class="sxs-lookup"><span data-stu-id="82839-176">The data in the file should match the text below:</span></span>

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
> <span data-ttu-id="82839-177">Vanwege de aard van gedistribueerde systemen kan de gegevensvolgorde per SQL Data Warehouse-database verschillen.</span><span class="sxs-lookup"><span data-stu-id="82839-177">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="82839-178">In plaats van de hele tabel te exporteren kunt u ook een query voor het extraheren van gegevens schrijven met de functie **queryout** van BCP.</span><span class="sxs-lookup"><span data-stu-id="82839-178">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="82839-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="82839-179">Next steps</span></span>
<span data-ttu-id="82839-180">Zie [Gegevens laden in SQL Data Warehouse][Load data into SQL Data Warehouse] voor een overzicht van het laden.</span><span class="sxs-lookup"><span data-stu-id="82839-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="82839-181">Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="82839-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
