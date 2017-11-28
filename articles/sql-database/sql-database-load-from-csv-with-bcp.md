---
title: aaaLoad gegevens uit CSV-bestand in Azure SQL Database (bcp) | Microsoft Docs
description: Voor kleine gegevenssets gebruikt bcp tooimport gegevens in Azure SQL Database.
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="50d47-103">Gegevens vanuit een CSV-bestand laden in een Azure SQL-database (platte bestanden)</span><span class="sxs-lookup"><span data-stu-id="50d47-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="50d47-104">U kunt Hallo bcp opdrachtregelprogramma tooimport gegevens uit een CSV-bestand in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="50d47-104">You can use hello bcp command-line utility tooimport data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="50d47-105">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="50d47-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="50d47-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="50d47-106">Prerequisites</span></span>
<span data-ttu-id="50d47-107">toocomplete hello stappen in dit artikel, moet u:</span><span class="sxs-lookup"><span data-stu-id="50d47-107">toocomplete hello steps in this article, you need:</span></span>

* <span data-ttu-id="50d47-108">Een logische Azure SQL-databaseserver en -database</span><span class="sxs-lookup"><span data-stu-id="50d47-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="50d47-109">Hallo opdrachtregelprogramma bcp geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="50d47-109">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="50d47-110">Hallo sqlcmd-opdrachtregelprogramma geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="50d47-110">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="50d47-111">U kunt hulpprogramma's voor Hallo bcp en sqlcmd downloaden van Hallo [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="50d47-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="50d47-112">Gegevens in ASCII- of UTF-16-indeling</span><span class="sxs-lookup"><span data-stu-id="50d47-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="50d47-113">Als u deze zelfstudie met uw eigen gegevens probeert, moet uw gegevens toouse Hallo ASCII- of UTF-16 omdat bcp biedt geen ondersteuning voor UTF-8-codering.</span><span class="sxs-lookup"><span data-stu-id="50d47-113">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="50d47-114">1. Een doeltabel maken</span><span class="sxs-lookup"><span data-stu-id="50d47-114">1. Create a destination table</span></span>
<span data-ttu-id="50d47-115">Een tabel in SQL-Database te definiëren als Hallo doeltabel.</span><span class="sxs-lookup"><span data-stu-id="50d47-115">Define a table in SQL Database as hello destination table.</span></span> <span data-ttu-id="50d47-116">Hallo-kolommen in tabel Hallo moeten overeenkomen met toohello gegevens in elke rij van het gegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="50d47-116">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="50d47-117">toocreate een tabel, open een opdrachtprompt en sqlcmd.exe toorun Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="50d47-117">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="50d47-118">2. Een brongegevensbestand maken</span><span class="sxs-lookup"><span data-stu-id="50d47-118">2. Create a source data file</span></span>
<span data-ttu-id="50d47-119">Open Kladblok en kopieer Hallo volgende regels van gegevens naar een nieuw tekstbestand en sla dit bestand tooyour lokale tijdelijke map C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="50d47-119">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="50d47-120">Dit zijn gegevens in ASCII-indeling.</span><span class="sxs-lookup"><span data-stu-id="50d47-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="50d47-121">(Optioneel) tooexport uw eigen gegevens uit een SQL Server-database, open een opdrachtprompt en Voer Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="50d47-121">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="50d47-122">Vervang TableName, ServerName, DatabaseName, Username en Password door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="50d47-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a><span data-ttu-id="50d47-123">3. Hallo gegevens laden</span><span class="sxs-lookup"><span data-stu-id="50d47-123">3. Load hello data</span></span>
<span data-ttu-id="50d47-124">tooload hello gegevens, open een opdrachtprompt en Voer Hallo de volgende opdracht, Hallo waarden voor de servernaam, Database-naam, gebruikersnaam en wachtwoord worden vervangen door uw eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="50d47-124">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="50d47-125">Gebruik die deze opdracht tooverify Hallo gegevens correct zijn geladen</span><span class="sxs-lookup"><span data-stu-id="50d47-125">Use this command tooverify hello data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="50d47-126">Hallo resultaten er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="50d47-126">hello results should look like this:</span></span>

| <span data-ttu-id="50d47-127">DateId</span><span class="sxs-lookup"><span data-stu-id="50d47-127">DateId</span></span> | <span data-ttu-id="50d47-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="50d47-128">CalendarQuarter</span></span> | <span data-ttu-id="50d47-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="50d47-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50d47-130">20150101</span><span class="sxs-lookup"><span data-stu-id="50d47-130">20150101</span></span> |<span data-ttu-id="50d47-131">1</span><span class="sxs-lookup"><span data-stu-id="50d47-131">1</span></span> |<span data-ttu-id="50d47-132">3</span><span class="sxs-lookup"><span data-stu-id="50d47-132">3</span></span> |
| <span data-ttu-id="50d47-133">20150201</span><span class="sxs-lookup"><span data-stu-id="50d47-133">20150201</span></span> |<span data-ttu-id="50d47-134">1</span><span class="sxs-lookup"><span data-stu-id="50d47-134">1</span></span> |<span data-ttu-id="50d47-135">3</span><span class="sxs-lookup"><span data-stu-id="50d47-135">3</span></span> |
| <span data-ttu-id="50d47-136">20150301</span><span class="sxs-lookup"><span data-stu-id="50d47-136">20150301</span></span> |<span data-ttu-id="50d47-137">1</span><span class="sxs-lookup"><span data-stu-id="50d47-137">1</span></span> |<span data-ttu-id="50d47-138">3</span><span class="sxs-lookup"><span data-stu-id="50d47-138">3</span></span> |
| <span data-ttu-id="50d47-139">20150401</span><span class="sxs-lookup"><span data-stu-id="50d47-139">20150401</span></span> |<span data-ttu-id="50d47-140">2</span><span class="sxs-lookup"><span data-stu-id="50d47-140">2</span></span> |<span data-ttu-id="50d47-141">4</span><span class="sxs-lookup"><span data-stu-id="50d47-141">4</span></span> |
| <span data-ttu-id="50d47-142">20150501</span><span class="sxs-lookup"><span data-stu-id="50d47-142">20150501</span></span> |<span data-ttu-id="50d47-143">2</span><span class="sxs-lookup"><span data-stu-id="50d47-143">2</span></span> |<span data-ttu-id="50d47-144">4</span><span class="sxs-lookup"><span data-stu-id="50d47-144">4</span></span> |
| <span data-ttu-id="50d47-145">20150601</span><span class="sxs-lookup"><span data-stu-id="50d47-145">20150601</span></span> |<span data-ttu-id="50d47-146">2</span><span class="sxs-lookup"><span data-stu-id="50d47-146">2</span></span> |<span data-ttu-id="50d47-147">4</span><span class="sxs-lookup"><span data-stu-id="50d47-147">4</span></span> |
| <span data-ttu-id="50d47-148">20150701</span><span class="sxs-lookup"><span data-stu-id="50d47-148">20150701</span></span> |<span data-ttu-id="50d47-149">3</span><span class="sxs-lookup"><span data-stu-id="50d47-149">3</span></span> |<span data-ttu-id="50d47-150">1</span><span class="sxs-lookup"><span data-stu-id="50d47-150">1</span></span> |
| <span data-ttu-id="50d47-151">20150801</span><span class="sxs-lookup"><span data-stu-id="50d47-151">20150801</span></span> |<span data-ttu-id="50d47-152">3</span><span class="sxs-lookup"><span data-stu-id="50d47-152">3</span></span> |<span data-ttu-id="50d47-153">1</span><span class="sxs-lookup"><span data-stu-id="50d47-153">1</span></span> |
| <span data-ttu-id="50d47-154">20150801</span><span class="sxs-lookup"><span data-stu-id="50d47-154">20150801</span></span> |<span data-ttu-id="50d47-155">3</span><span class="sxs-lookup"><span data-stu-id="50d47-155">3</span></span> |<span data-ttu-id="50d47-156">1</span><span class="sxs-lookup"><span data-stu-id="50d47-156">1</span></span> |
| <span data-ttu-id="50d47-157">20151001</span><span class="sxs-lookup"><span data-stu-id="50d47-157">20151001</span></span> |<span data-ttu-id="50d47-158">4</span><span class="sxs-lookup"><span data-stu-id="50d47-158">4</span></span> |<span data-ttu-id="50d47-159">2</span><span class="sxs-lookup"><span data-stu-id="50d47-159">2</span></span> |
| <span data-ttu-id="50d47-160">20151101</span><span class="sxs-lookup"><span data-stu-id="50d47-160">20151101</span></span> |<span data-ttu-id="50d47-161">4</span><span class="sxs-lookup"><span data-stu-id="50d47-161">4</span></span> |<span data-ttu-id="50d47-162">2</span><span class="sxs-lookup"><span data-stu-id="50d47-162">2</span></span> |
| <span data-ttu-id="50d47-163">20151201</span><span class="sxs-lookup"><span data-stu-id="50d47-163">20151201</span></span> |<span data-ttu-id="50d47-164">4</span><span class="sxs-lookup"><span data-stu-id="50d47-164">4</span></span> |<span data-ttu-id="50d47-165">2</span><span class="sxs-lookup"><span data-stu-id="50d47-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="50d47-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="50d47-166">Next steps</span></span>
<span data-ttu-id="50d47-167">Zie SQL Server-database toomigrate [migratie van SQL Server-database](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="50d47-167">toomigrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
