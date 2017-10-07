---
title: aaaBuild en tabellen voor het snel parallelle importeren van gegevens in een SQL-Server op een Azure VM optimaliseren | Microsoft Docs
description: Parallel bulkimporteren van gegevens met SQL-partitietabellen
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: ab748c47348ec6ca3b98ba39e27181bba5d36fc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a>Parallel bulkimporteren van gegevens met SQL-partitietabellen
Dit document wordt beschreven hoe toobuild gepartitioneerde tabellen voor het snel parallelle bulkbewerkingen voor importeren van gegevens tooa SQL Server-database. Voor grote gegevens laden per overdracht tooa SQL-database importeren van gegevens toohello SQL-database en de volgende query's kan worden verbeterd via *gepartitioneerde tabellen en weergaven*. 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a>Maak een nieuwe database en een set bestandsgroepen
* [Maak een nieuwe database](https://technet.microsoft.com/library/ms176061.aspx), als deze niet al bestaat.
* Database bestandsgroepen toohello database waarin Hallo gepartitioneerd fysieke bestanden toevoegen. Dit kan worden gedaan met [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) als de nieuwe of [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) als Hallo database al bestaat.
* Voeg een of meer bestanden (indien nodig) tooeach database bestandsgroep.
  
  > [!NOTE]
  > Geef Hallo doel bestandsgroep die gegevens voor deze partitie en Hallo fysieke database bestandsnaam of-namen bevat waar Hallo filegroup-gegevens worden opgeslagen.
  > 
  > 

Hallo volgende voorbeeld wordt een nieuwe database met drie bestandsgroepen dan Hallo primaire en logboekregistratie groepen, met een fysiek bestand in elk. Hallo-databasebestanden worden gemaakt in SQL Server Data-standaardmap met Hallo zoals geconfigureerd in Hallo SQL Server-exemplaar. Zie voor meer informatie over Hallo standaardbestandslocaties [bestandslocaties voor standaard- en benoemde exemplaren van SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);

    EXECUTE ('
        CREATE DATABASE <database_name>
         ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
         LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')

## <a name="create-a-partitioned-table"></a>Een gepartitioneerde tabel maken
Gepartitioneerde tabellen volgens toohello gegevensschema, toegewezen toohello database bestandsgroepen gemaakt in de vorige stap Hallo maken. Als er gegevens bulksgewijs geïmporteerd toohello tabel(len) gepartitioneerd, records zal worden verdeeld over Hallo bestandsgroepen volgens tooa partitieschema, zoals hieronder wordt beschreven.

**een partitietabel toocreate, moet u:**

* [Maken van een partitiefunctie](https://msdn.microsoft.com/library/ms187802.aspx) definieert een reeks waarden/grenzen toobe Hallo opgenomen in elke partitietabel afzonderlijke bijvoorbeeld toolimit partities per maand (sommige\_datetime\_veld) in Hallo jaar 2013:
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* [Maken van een partitieschema](https://msdn.microsoft.com/library/ms179854.aspx) die elk partitiebereik in Hallo partitie functie tooa fysieke bestandsgroep, zoals toegewezen:
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  tooverify hello bereiken van kracht in elke partitie volgens toohello functie/schema, Hallo volgende query worden uitgevoerd:
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* [Gepartitioneerde tabel maken](https://msdn.microsoft.com/library/ms174979.aspx)(s) op basis van tooyour gegevensschema en geef Hallo partitie schema en beperking veld gebruikt toopartition Hallo tabel, bijvoorbeeld:
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

Zie voor meer informatie [gepartitioneerde tabellen maken en indexen](https://msdn.microsoft.com/library/ms188730.aspx).

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a>Hallo gegevens voor bulksgewijs importeren voor elke afzonderlijke partitietabel
* U kunt BCP BULK INSERT of andere methoden, zoals [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/). Hallo-voorbeeld opgegeven wordt Hallo BCP methode.
* [ALTER database Hallo](https://msdn.microsoft.com/library/bb522682.aspx) toochange transactie logboekregistratie schema tooBULK_LOGGED toominimize overhead van het aan te melden, bijvoorbeeld:
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* tooexpedite gegevens te laden, start Hallo bulkbewerkingen importeren parallel. Zie voor tips over bespoedigen bulksgewijs importeren van big data in SQL Server-databases [laden van 1TB in minder dan 1 uur](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).

Hallo is volgende PowerShell-script een voorbeeld van een parallelle gegevens laden met BCP.

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # hello example assumes hello partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes hello input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set hello server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match hello number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name toobe loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"

    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir

    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }

    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }

    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }

    Get-Job

    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a>Indexen toooptimize joins en prestaties van query's maken
* Als u gegevens voor het model wordt ophaalt uit meerdere tabellen, indexen maken op Hallo join sleutels tooimprove Hallo join prestaties.
* [Maken van indexen](https://technet.microsoft.com/library/ms188783.aspx) (geclusterde of niet-geclusterde) targeting hello dezelfde bestandsgroep voor elke partitie voor bijvoorbeeld:
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  Of,
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > U kunt toocreate Hallo indexen voordat bulksgewijs Hallo gegevens importeren. Maken van een index voor het bulksgewijs importeren langzamer Hallo gegevens te laden.
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a>Geavanceerde analyses proces en de technologie in actie voorbeeld
Zie voor een overzicht van de end-to-end voorbeeld Hallo Cortana-Analytics-proces gebruik met een openbare gegevensset, [Cortana-Analytics proces in actie: met behulp van SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

