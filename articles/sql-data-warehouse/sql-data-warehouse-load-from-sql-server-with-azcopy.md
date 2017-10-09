---
title: aaaLoad gegevens uit SQL Server in Azure SQL Data Warehouse (PolyBase) | Microsoft Docs
description: Gebruikt bcp tooexport gegevens uit SQL Server tooflat bestanden, AZCopy tooimport gegevens tooAzure blob storage en PolyBase tooingest Hallo gegevens in Azure SQL Data Warehouse.
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
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="27354-103">Gegevens uit SQL Server laden in Azure SQL Data Warehouse (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="27354-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="27354-104">Gebruikt bcp en AZCopy-opdrachtregelprogramma's tooload gegevens uit SQL Server tooAzure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="27354-104">Use bcp and AZCopy command-line utilities tooload data from SQL Server tooAzure blob storage.</span></span> <span data-ttu-id="27354-105">Gebruik vervolgens PolyBase of Azure Data Factory tooload Hallo gegevens in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27354-105">Then use PolyBase or Azure Data Factory tooload hello data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="27354-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="27354-106">Prerequisites</span></span>
<span data-ttu-id="27354-107">toostep voor deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="27354-107">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="27354-108">Een SQL Data Warehouse-database</span><span class="sxs-lookup"><span data-stu-id="27354-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="27354-109">Hallo bcp opdrachtregel-hulpprogramma is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="27354-109">hello bcp command line utility installed</span></span>
* <span data-ttu-id="27354-110">Hallo SQLCMD vanaf de opdrachtregel-hulpprogramma is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="27354-110">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="27354-111">U kunt hulpprogramma's voor Hallo bcp en sqlcmd downloaden van Hallo [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="27354-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="27354-112">Gegevens importeren in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="27354-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="27354-113">In deze zelfstudie maakt u een tabel maken in Azure SQL Data Warehouse en gegevens importeren in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="27354-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="27354-114">Stap 1: een tabel maken in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="27354-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="27354-115">Gebruik vanaf een opdrachtprompt sqlcmd toorun Hallo query toocreate een tabel op uw exemplaar te volgen:</span><span class="sxs-lookup"><span data-stu-id="27354-115">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="27354-116">Zie [tabel overzicht] [ Table Overview] of [syntaxis voor CREATE TABLE] [ CREATE TABLE syntax] voor meer informatie over het maken van een tabel in SQL Data Warehouse en Hallo  beschikbare opties in de component WITH Hallo.</span><span class="sxs-lookup"><span data-stu-id="27354-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="27354-117">Stap 2: een brongegevensbestand maken</span><span class="sxs-lookup"><span data-stu-id="27354-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="27354-118">Open Kladblok en kopieer Hallo volgende regels van gegevens naar een nieuw tekstbestand en sla dit bestand tooyour lokale tijdelijke map C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="27354-118">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="27354-119">Het is belangrijk tooremember die bcp.exe biedt geen ondersteuning voor UTF-8 Hallo bestandscodering.</span><span class="sxs-lookup"><span data-stu-id="27354-119">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="27354-120">Gebruik ASCII-bestanden of bestanden met de bestandscodering UTF-16 als u bcp.exe gebruikt.</span><span class="sxs-lookup"><span data-stu-id="27354-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="27354-121">Stap 3: Verbinding maken en Hallo gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="27354-121">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="27354-122">Met bcp kunt u verbinding maken en importeren van Hallo-gegevens met behulp van Hallo opdracht vervangen Hallo waarden waar nodig te volgen:</span><span class="sxs-lookup"><span data-stu-id="27354-122">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="27354-123">U kunt de gegevens zijn geladen door het uitvoeren van de volgende query met sqlcmd Hallo Hallo controleren:</span><span class="sxs-lookup"><span data-stu-id="27354-123">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="27354-124">Dit resultaat moet geven Hallo resultaten te volgen:</span><span class="sxs-lookup"><span data-stu-id="27354-124">This should return hello following results:</span></span>

| <span data-ttu-id="27354-125">DateId</span><span class="sxs-lookup"><span data-stu-id="27354-125">DateId</span></span> | <span data-ttu-id="27354-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="27354-126">CalendarQuarter</span></span> | <span data-ttu-id="27354-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="27354-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="27354-128">20150101</span><span class="sxs-lookup"><span data-stu-id="27354-128">20150101</span></span> |<span data-ttu-id="27354-129">1</span><span class="sxs-lookup"><span data-stu-id="27354-129">1</span></span> |<span data-ttu-id="27354-130">3</span><span class="sxs-lookup"><span data-stu-id="27354-130">3</span></span> |
| <span data-ttu-id="27354-131">20150201</span><span class="sxs-lookup"><span data-stu-id="27354-131">20150201</span></span> |<span data-ttu-id="27354-132">1</span><span class="sxs-lookup"><span data-stu-id="27354-132">1</span></span> |<span data-ttu-id="27354-133">3</span><span class="sxs-lookup"><span data-stu-id="27354-133">3</span></span> |
| <span data-ttu-id="27354-134">20150301</span><span class="sxs-lookup"><span data-stu-id="27354-134">20150301</span></span> |<span data-ttu-id="27354-135">1</span><span class="sxs-lookup"><span data-stu-id="27354-135">1</span></span> |<span data-ttu-id="27354-136">3</span><span class="sxs-lookup"><span data-stu-id="27354-136">3</span></span> |
| <span data-ttu-id="27354-137">20150401</span><span class="sxs-lookup"><span data-stu-id="27354-137">20150401</span></span> |<span data-ttu-id="27354-138">2</span><span class="sxs-lookup"><span data-stu-id="27354-138">2</span></span> |<span data-ttu-id="27354-139">4</span><span class="sxs-lookup"><span data-stu-id="27354-139">4</span></span> |
| <span data-ttu-id="27354-140">20150501</span><span class="sxs-lookup"><span data-stu-id="27354-140">20150501</span></span> |<span data-ttu-id="27354-141">2</span><span class="sxs-lookup"><span data-stu-id="27354-141">2</span></span> |<span data-ttu-id="27354-142">4</span><span class="sxs-lookup"><span data-stu-id="27354-142">4</span></span> |
| <span data-ttu-id="27354-143">20150601</span><span class="sxs-lookup"><span data-stu-id="27354-143">20150601</span></span> |<span data-ttu-id="27354-144">2</span><span class="sxs-lookup"><span data-stu-id="27354-144">2</span></span> |<span data-ttu-id="27354-145">4</span><span class="sxs-lookup"><span data-stu-id="27354-145">4</span></span> |
| <span data-ttu-id="27354-146">20150701</span><span class="sxs-lookup"><span data-stu-id="27354-146">20150701</span></span> |<span data-ttu-id="27354-147">3</span><span class="sxs-lookup"><span data-stu-id="27354-147">3</span></span> |<span data-ttu-id="27354-148">1</span><span class="sxs-lookup"><span data-stu-id="27354-148">1</span></span> |
| <span data-ttu-id="27354-149">20150801</span><span class="sxs-lookup"><span data-stu-id="27354-149">20150801</span></span> |<span data-ttu-id="27354-150">3</span><span class="sxs-lookup"><span data-stu-id="27354-150">3</span></span> |<span data-ttu-id="27354-151">1</span><span class="sxs-lookup"><span data-stu-id="27354-151">1</span></span> |
| <span data-ttu-id="27354-152">20150801</span><span class="sxs-lookup"><span data-stu-id="27354-152">20150801</span></span> |<span data-ttu-id="27354-153">3</span><span class="sxs-lookup"><span data-stu-id="27354-153">3</span></span> |<span data-ttu-id="27354-154">1</span><span class="sxs-lookup"><span data-stu-id="27354-154">1</span></span> |
| <span data-ttu-id="27354-155">20151001</span><span class="sxs-lookup"><span data-stu-id="27354-155">20151001</span></span> |<span data-ttu-id="27354-156">4</span><span class="sxs-lookup"><span data-stu-id="27354-156">4</span></span> |<span data-ttu-id="27354-157">2</span><span class="sxs-lookup"><span data-stu-id="27354-157">2</span></span> |
| <span data-ttu-id="27354-158">20151101</span><span class="sxs-lookup"><span data-stu-id="27354-158">20151101</span></span> |<span data-ttu-id="27354-159">4</span><span class="sxs-lookup"><span data-stu-id="27354-159">4</span></span> |<span data-ttu-id="27354-160">2</span><span class="sxs-lookup"><span data-stu-id="27354-160">2</span></span> |
| <span data-ttu-id="27354-161">20151201</span><span class="sxs-lookup"><span data-stu-id="27354-161">20151201</span></span> |<span data-ttu-id="27354-162">4</span><span class="sxs-lookup"><span data-stu-id="27354-162">4</span></span> |<span data-ttu-id="27354-163">2</span><span class="sxs-lookup"><span data-stu-id="27354-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="27354-164">Stap 4: statistieken maken voor uw zojuist geladen gegevens</span><span class="sxs-lookup"><span data-stu-id="27354-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="27354-165">Azure SQL Data Warehouse bevat nog geen functionaliteit voor het automatisch maken of bijwerken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="27354-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="27354-166">Het is belangrijk dat u statistieken voor alle kolommen van alle tabellen nadat Hallo eerst zijn geladen maakt of belangrijke wijzigingen plaatsvinden in Hallo gegevens in volgorde tooget Hallo optimale prestaties van uw query.</span><span class="sxs-lookup"><span data-stu-id="27354-166">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="27354-167">Zie voor een gedetailleerde uitleg van statistieken Hallo [statistieken] [ Statistics] onderwerp in Hallo groep onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="27354-167">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="27354-168">Hieronder vindt u een kort voorbeeld van hoe toocreate statistieken op Hallo ingediend in dit voorbeeld geladen</span><span class="sxs-lookup"><span data-stu-id="27354-168">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="27354-169">Hallo volgende CREATE STATISTICS-instructies uit een sqlcmd-opdrachtprompt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="27354-169">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="27354-170">Gegevens uit SQL Data Warehouse exporteren</span><span class="sxs-lookup"><span data-stu-id="27354-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="27354-171">In deze zelfstudie maakt u een gegevensbestand op basis van een tabel in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27354-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="27354-172">We worden tooa nieuw gegevensbestand naam DimDate2_export.txt gemaakte Hallo-gegevens geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="27354-172">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="27354-173">Stap 1: Hallo gegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="27354-173">Step 1: Export hello data</span></span>
<span data-ttu-id="27354-174">Hallo bcp-hulpprogramma gebruikt, kunt u verbinding maken en gegevens exporteren met de Hallo na opdracht vervangen Hallo waarden waar nodig:</span><span class="sxs-lookup"><span data-stu-id="27354-174">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="27354-175">U kunt controleren of Hallo gegevens correct zijn geëxporteerd door nieuwe Hallo-bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="27354-175">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="27354-176">Hallo-gegevens in Hallo-bestand moet overeenkomen met de Hallo onderstaande tekst:</span><span class="sxs-lookup"><span data-stu-id="27354-176">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="27354-177">Vervaldatum toohello aard van gedistribueerde systemen, Hallo gegevensvolgorde mogelijk niet dezelfde Hallo tussen databases van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27354-177">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="27354-178">Een andere optie is toouse hello **queryout** functie van bcp toowrite een query uitpakken in plaats van de gehele tabel Hallo exporteren.</span><span class="sxs-lookup"><span data-stu-id="27354-178">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="27354-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="27354-179">Next steps</span></span>
<span data-ttu-id="27354-180">Zie [Gegevens laden in SQL Data Warehouse][Load data into SQL Data Warehouse] voor een overzicht van het laden.</span><span class="sxs-lookup"><span data-stu-id="27354-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="27354-181">Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="27354-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
