---
title: aaaUse bcp tooload-gegevens in SQL Data Warehouse | Microsoft Docs
description: Meer informatie over welke BCP en hoe toouse voor datawarehousescenario's.
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
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="1b1d9-103">Gegevens laden met bcp</span><span class="sxs-lookup"><span data-stu-id="1b1d9-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b1d9-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="1b1d9-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="1b1d9-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="1b1d9-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="1b1d9-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="1b1d9-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="1b1d9-107">BCP</span><span class="sxs-lookup"><span data-stu-id="1b1d9-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="1b1d9-108">**[BCP] [ bcp]**  is een opdrachtregelprogramma voor het bulksgewijs laden hulpprogramma waarmee u toocopy gegevens tussen de SQL Server, gegevensbestanden en SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-108">**[bcp][bcp]** is a command-line bulk load utility that allows you toocopy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="1b1d9-109">Gebruikt bcp tooimport groot aantal rijen in SQL Data Warehouse-tabellen of tooexport gegevens uit SQL Server-tabellen naar gegevensbestanden.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-109">Use bcp tooimport large numbers of rows into SQL Data Warehouse tables or tooexport data from SQL Server tables into data files.</span></span> <span data-ttu-id="1b1d9-110">Bcp vereist, behalve wanneer gebruikt de optie queryout hello, zonder enige kennis van Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-110">Except when used with hello queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="1b1d9-111">BCP is een snelle en gemakkelijke manier toomove kleinere gegevenssets van en naar een SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-111">bcp is a quick and easy way toomove smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="1b1d9-112">Hallo exacte hoeveelheid gegevens die wordt aanbevolen tooload/extract via bcp hangen af op het netwerk van verbinding toohello Azure-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-112">hello exact amount of data that is recommended tooload/extract via bcp will depend on you network connection toohello Azure data center.</span></span>  <span data-ttu-id="1b1d9-113">Over het algemeen kunt u dimensietabellen probleemloos laden en extraheren met BCP. Voor grote hoeveelheden gegevens wordt BCP echter niet aangeraden.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="1b1d9-114">Polybase is Hallo aanbevolen hulpprogramma voor het laden en extraheren van grote hoeveelheden gegevens als er een beter geschikt Hallo uitgebreide parallelle verwerkingsarchitectuur van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-114">Polybase is hello recommended tool for loading and extracting large volumes of data as it does a better job leveraging hello massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="1b1d9-115">Met BCP kunt u:</span><span class="sxs-lookup"><span data-stu-id="1b1d9-115">With bcp you can:</span></span>

* <span data-ttu-id="1b1d9-116">Gebruik een eenvoudig opdrachtregelprogramma tooload gegevens in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-116">Use a simple command-line utility tooload data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="1b1d9-117">Gebruik een eenvoudig opdrachtregelprogramma tooextract gegevens uit SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-117">Use a simple command-line utility tooextract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="1b1d9-118">In deze zelfstudie leert u hoe u het volgende kunt doen:</span><span class="sxs-lookup"><span data-stu-id="1b1d9-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="1b1d9-119">Gegevens importeren in een tabel met behulp van bcp Hallo in de opdracht</span><span class="sxs-lookup"><span data-stu-id="1b1d9-119">Import data into a table using hello bcp in command</span></span>
* <span data-ttu-id="1b1d9-120">Gegevens exporteren uit een tabel met behulp Hallo bcp-opdracht out</span><span class="sxs-lookup"><span data-stu-id="1b1d9-120">Export data from a table uisng hello bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1b1d9-121">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1b1d9-121">Prerequisites</span></span>
<span data-ttu-id="1b1d9-122">toostep voor deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="1b1d9-122">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="1b1d9-123">Een SQL Data Warehouse-database</span><span class="sxs-lookup"><span data-stu-id="1b1d9-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="1b1d9-124">Hallo bcp opdrachtregel-hulpprogramma is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="1b1d9-124">hello bcp command line utility installed</span></span>
* <span data-ttu-id="1b1d9-125">Hallo SQLCMD vanaf de opdrachtregel-hulpprogramma is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="1b1d9-125">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="1b1d9-126">U kunt hulpprogramma's voor Hallo bcp en sqlcmd downloaden van Hallo [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="1b1d9-126">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="1b1d9-127">Gegevens importeren in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1b1d9-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="1b1d9-128">In deze zelfstudie maakt u een tabel maken in Azure SQL Data Warehouse en gegevens importeren in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="1b1d9-129">Stap 1: een tabel maken in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1b1d9-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="1b1d9-130">Gebruik vanaf een opdrachtprompt sqlcmd toorun Hallo query toocreate een tabel op uw exemplaar te volgen:</span><span class="sxs-lookup"><span data-stu-id="1b1d9-130">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="1b1d9-131">Zie [tabel overzicht] [ Table Overview] of [syntaxis voor CREATE TABLE] [ CREATE TABLE syntax] voor meer informatie over het maken van een tabel in SQL Data Warehouse en Hallo  beschikbare opties in de component WITH Hallo.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="1b1d9-132">Stap 2: een brongegevensbestand maken</span><span class="sxs-lookup"><span data-stu-id="1b1d9-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="1b1d9-133">Open Kladblok en kopieer Hallo volgende regels van gegevens naar een nieuw tekstbestand en sla dit bestand tooyour lokale tijdelijke map C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-133">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="1b1d9-134">Het is belangrijk tooremember die bcp.exe biedt geen ondersteuning voor UTF-8 Hallo bestandscodering.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-134">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="1b1d9-135">Gebruik ASCII-bestanden of bestanden met de bestandscodering UTF-16 als u bcp.exe gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="1b1d9-136">Stap 3: Verbinding maken en Hallo gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="1b1d9-136">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="1b1d9-137">Met bcp kunt u verbinding maken en importeren van Hallo-gegevens met behulp van Hallo opdracht vervangen Hallo waarden waar nodig te volgen:</span><span class="sxs-lookup"><span data-stu-id="1b1d9-137">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="1b1d9-138">U kunt de gegevens zijn geladen door het uitvoeren van de volgende query met sqlcmd Hallo Hallo controleren:</span><span class="sxs-lookup"><span data-stu-id="1b1d9-138">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="1b1d9-139">Dit resultaat moet geven Hallo resultaten te volgen:</span><span class="sxs-lookup"><span data-stu-id="1b1d9-139">This should return hello following results:</span></span>

| <span data-ttu-id="1b1d9-140">DateId</span><span class="sxs-lookup"><span data-stu-id="1b1d9-140">DateId</span></span> | <span data-ttu-id="1b1d9-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="1b1d9-141">CalendarQuarter</span></span> | <span data-ttu-id="1b1d9-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="1b1d9-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b1d9-143">20150101</span><span class="sxs-lookup"><span data-stu-id="1b1d9-143">20150101</span></span> |<span data-ttu-id="1b1d9-144">1</span><span class="sxs-lookup"><span data-stu-id="1b1d9-144">1</span></span> |<span data-ttu-id="1b1d9-145">3</span><span class="sxs-lookup"><span data-stu-id="1b1d9-145">3</span></span> |
| <span data-ttu-id="1b1d9-146">20150201</span><span class="sxs-lookup"><span data-stu-id="1b1d9-146">20150201</span></span> |<span data-ttu-id="1b1d9-147">1</span><span class="sxs-lookup"><span data-stu-id="1b1d9-147">1</span></span> |<span data-ttu-id="1b1d9-148">3</span><span class="sxs-lookup"><span data-stu-id="1b1d9-148">3</span></span> |
| <span data-ttu-id="1b1d9-149">20150301</span><span class="sxs-lookup"><span data-stu-id="1b1d9-149">20150301</span></span> |<span data-ttu-id="1b1d9-150">1</span><span class="sxs-lookup"><span data-stu-id="1b1d9-150">1</span></span> |<span data-ttu-id="1b1d9-151">3</span><span class="sxs-lookup"><span data-stu-id="1b1d9-151">3</span></span> |
| <span data-ttu-id="1b1d9-152">20150401</span><span class="sxs-lookup"><span data-stu-id="1b1d9-152">20150401</span></span> |<span data-ttu-id="1b1d9-153">2</span><span class="sxs-lookup"><span data-stu-id="1b1d9-153">2</span></span> |<span data-ttu-id="1b1d9-154">4</span><span class="sxs-lookup"><span data-stu-id="1b1d9-154">4</span></span> |
| <span data-ttu-id="1b1d9-155">20150501</span><span class="sxs-lookup"><span data-stu-id="1b1d9-155">20150501</span></span> |<span data-ttu-id="1b1d9-156">2</span><span class="sxs-lookup"><span data-stu-id="1b1d9-156">2</span></span> |<span data-ttu-id="1b1d9-157">4</span><span class="sxs-lookup"><span data-stu-id="1b1d9-157">4</span></span> |
| <span data-ttu-id="1b1d9-158">20150601</span><span class="sxs-lookup"><span data-stu-id="1b1d9-158">20150601</span></span> |<span data-ttu-id="1b1d9-159">2</span><span class="sxs-lookup"><span data-stu-id="1b1d9-159">2</span></span> |<span data-ttu-id="1b1d9-160">4</span><span class="sxs-lookup"><span data-stu-id="1b1d9-160">4</span></span> |
| <span data-ttu-id="1b1d9-161">20150701</span><span class="sxs-lookup"><span data-stu-id="1b1d9-161">20150701</span></span> |<span data-ttu-id="1b1d9-162">3</span><span class="sxs-lookup"><span data-stu-id="1b1d9-162">3</span></span> |<span data-ttu-id="1b1d9-163">1</span><span class="sxs-lookup"><span data-stu-id="1b1d9-163">1</span></span> |
| <span data-ttu-id="1b1d9-164">20150801</span><span class="sxs-lookup"><span data-stu-id="1b1d9-164">20150801</span></span> |<span data-ttu-id="1b1d9-165">3</span><span class="sxs-lookup"><span data-stu-id="1b1d9-165">3</span></span> |<span data-ttu-id="1b1d9-166">1</span><span class="sxs-lookup"><span data-stu-id="1b1d9-166">1</span></span> |
| <span data-ttu-id="1b1d9-167">20150801</span><span class="sxs-lookup"><span data-stu-id="1b1d9-167">20150801</span></span> |<span data-ttu-id="1b1d9-168">3</span><span class="sxs-lookup"><span data-stu-id="1b1d9-168">3</span></span> |<span data-ttu-id="1b1d9-169">1</span><span class="sxs-lookup"><span data-stu-id="1b1d9-169">1</span></span> |
| <span data-ttu-id="1b1d9-170">20151001</span><span class="sxs-lookup"><span data-stu-id="1b1d9-170">20151001</span></span> |<span data-ttu-id="1b1d9-171">4</span><span class="sxs-lookup"><span data-stu-id="1b1d9-171">4</span></span> |<span data-ttu-id="1b1d9-172">2</span><span class="sxs-lookup"><span data-stu-id="1b1d9-172">2</span></span> |
| <span data-ttu-id="1b1d9-173">20151101</span><span class="sxs-lookup"><span data-stu-id="1b1d9-173">20151101</span></span> |<span data-ttu-id="1b1d9-174">4</span><span class="sxs-lookup"><span data-stu-id="1b1d9-174">4</span></span> |<span data-ttu-id="1b1d9-175">2</span><span class="sxs-lookup"><span data-stu-id="1b1d9-175">2</span></span> |
| <span data-ttu-id="1b1d9-176">20151201</span><span class="sxs-lookup"><span data-stu-id="1b1d9-176">20151201</span></span> |<span data-ttu-id="1b1d9-177">4</span><span class="sxs-lookup"><span data-stu-id="1b1d9-177">4</span></span> |<span data-ttu-id="1b1d9-178">2</span><span class="sxs-lookup"><span data-stu-id="1b1d9-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="1b1d9-179">Stap 4: statistieken maken voor uw zojuist geladen gegevens</span><span class="sxs-lookup"><span data-stu-id="1b1d9-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="1b1d9-180">Azure SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="1b1d9-181">Het is belangrijk dat u statistieken voor alle kolommen van alle tabellen nadat Hallo eerst zijn geladen maakt of belangrijke wijzigingen plaatsvinden in Hallo gegevens in volgorde tooget Hallo optimale prestaties van uw query.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-181">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="1b1d9-182">Zie voor een gedetailleerde uitleg van statistieken Hallo [statistieken] [ Statistics] onderwerp in Hallo groep onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-182">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="1b1d9-183">Hieronder vindt u een kort voorbeeld van hoe toocreate statistieken op Hallo ingediend in dit voorbeeld geladen</span><span class="sxs-lookup"><span data-stu-id="1b1d9-183">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="1b1d9-184">Hallo volgende CREATE STATISTICS-instructies uit een sqlcmd-opdrachtprompt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1b1d9-184">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="1b1d9-185">Gegevens uit SQL Data Warehouse exporteren</span><span class="sxs-lookup"><span data-stu-id="1b1d9-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="1b1d9-186">In deze zelfstudie maakt u een gegevensbestand op basis van een tabel in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="1b1d9-187">We worden tooa nieuw gegevensbestand naam DimDate2_export.txt gemaakte Hallo-gegevens geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-187">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="1b1d9-188">Stap 1: Hallo gegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="1b1d9-188">Step 1: Export hello data</span></span>
<span data-ttu-id="1b1d9-189">Hallo bcp-hulpprogramma gebruikt, kunt u verbinding maken en gegevens exporteren met de Hallo na opdracht vervangen Hallo waarden waar nodig:</span><span class="sxs-lookup"><span data-stu-id="1b1d9-189">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="1b1d9-190">U kunt controleren of Hallo gegevens correct zijn geëxporteerd door nieuwe Hallo-bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-190">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="1b1d9-191">Hallo-gegevens in Hallo-bestand moet overeenkomen met de Hallo onderstaande tekst:</span><span class="sxs-lookup"><span data-stu-id="1b1d9-191">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="1b1d9-192">Vervaldatum toohello aard van gedistribueerde systemen, Hallo gegevensvolgorde mogelijk niet dezelfde Hallo tussen databases van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-192">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="1b1d9-193">Een andere optie is toouse hello **queryout** functie van bcp toowrite een query uitpakken in plaats van de gehele tabel Hallo exporteren.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-193">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1b1d9-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1b1d9-194">Next steps</span></span>
<span data-ttu-id="1b1d9-195">Zie [Gegevens laden in SQL Data Warehouse][Load data into SQL Data Warehouse] voor een overzicht van het laden.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="1b1d9-196">Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="1b1d9-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
