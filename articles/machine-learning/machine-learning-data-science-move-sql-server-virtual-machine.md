---
title: aaaMove gegevens tooSQL Server op een virtuele machine in Azure | Microsoft Docs
description: Gegevens uit platte bestanden of van een lokale SQL Server tooSQL Server verplaatsen op de virtuele machine van Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="bed52-103">Gegevens tooSQL Server op Azure een virtuele machine verplaatsen</span><span class="sxs-lookup"><span data-stu-id="bed52-103">Move data tooSQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="bed52-104">In dit onderwerp bevat een overzicht van Hallo opties voor het verplaatsen van gegevens uit platte bestanden (TSV- of CSV-indeling) of van een lokale SQL Server tooSQL Server op Azure een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bed52-104">This topic outlines hello options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server tooSQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="bed52-105">Deze taken voor zwevend gegevens toohello cloud maken deel uit van Hallo Team gegevens wetenschappelijke processen.</span><span class="sxs-lookup"><span data-stu-id="bed52-105">These tasks for moving data toohello cloud are part of hello Team Data Science Process.</span></span>

<span data-ttu-id="bed52-106">Zie voor in dit onderwerp bevat een overzicht van Hallo opties voor verplaatsen gegevens tooan Azure SQL Database voor Machine Learning, [verplaatsen van gegevens tooan Azure SQL Database voor Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="bed52-106">For a topic that outlines hello options for moving data tooan Azure SQL Database for Machine Learning, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="bed52-107">Hallo **menu** hieronder koppelingen tootopics waarin wordt beschreven hoe gegevens in andere omgevingen doel waar Hallo gegevens kunnen worden opgeslagen en verwerkt tijdens tooingest Hallo Team gegevens wetenschap proces (TDSP).</span><span class="sxs-lookup"><span data-stu-id="bed52-107">hello **menu** below links tootopics that describe how tooingest data into other target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="bed52-108">Hallo volgende tabel ziet u Hallo opties voor verplaatsen gegevens tooSQL Server op Azure een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bed52-108">hello following table summarizes hello options for moving data tooSQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="bed52-109"><b>BRON</b></span><span class="sxs-lookup"><span data-stu-id="bed52-109"><b>SOURCE</b></span></span> | <span data-ttu-id="bed52-110"><b>BESTEMMING: SQL Server op Azure VM</b></span><span class="sxs-lookup"><span data-stu-id="bed52-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="bed52-111"><b>Plat bestand</b></span><span class="sxs-lookup"><span data-stu-id="bed52-111"><b>Flat File</b></span></span> |<span data-ttu-id="bed52-112">1. <a href="#insert-tables-bcp">Hulpprogramma voor opdrachtregelprogramma voor het bulksgewijs kopiëren (BCP)</a></span><span class="sxs-lookup"><span data-stu-id="bed52-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="bed52-113">2. <a href="#insert-tables-bulkquery">Bulksgewijs invoegen SQL-Query</a></span><span class="sxs-lookup"><span data-stu-id="bed52-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="bed52-114">3. <a href="#sql-builtin-utilities">Grafische ingebouwde hulpprogramma's in SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="bed52-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="bed52-115"><b>On-Premises SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="bed52-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="bed52-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Een Microsoft Azure VM-wizard van SQL Server-Database tooa implementeren</a></span><span class="sxs-lookup"><span data-stu-id="bed52-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="bed52-117">2. <a href="#export-flat-file">Exporteren van tooa platte bestand</a></span><span class="sxs-lookup"><span data-stu-id="bed52-117">2. <a href="#export-flat-file">Export tooa flat File </a></span></span><br> <span data-ttu-id="bed52-118">3. <a href="#sql-migration">Wizard voor migratie van SQL-Database</a></span><span class="sxs-lookup"><span data-stu-id="bed52-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="bed52-119">4. <a href="#sql-backup">Back-up van database maken en terugzetten</a></span><span class="sxs-lookup"><span data-stu-id="bed52-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="bed52-120">Let op: dit document wordt ervan uitgegaan dat de SQL-opdrachten worden uitgevoerd vanuit SQL Server Management Studio of Visual Studio Database Explorer.</span><span class="sxs-lookup"><span data-stu-id="bed52-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="bed52-121">Als alternatief kunt u [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate en plannen van een pijplijn die gegevens tooa SQL Server VM op Azure wordt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="bed52-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate and schedule a pipeline that will move data tooa SQL Server VM on Azure.</span></span> <span data-ttu-id="bed52-122">Zie voor meer informatie [kopiëren van gegevens met Azure Data Factory (Kopieeractiviteit)](../data-factory/data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="bed52-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="bed52-123"><a name="prereqs"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="bed52-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="bed52-124">Deze zelfstudie wordt ervan uitgegaan dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="bed52-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="bed52-125">Een **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="bed52-125">An **Azure subscription**.</span></span> <span data-ttu-id="bed52-126">Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bed52-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bed52-127">Een **Azure storage-account**.</span><span class="sxs-lookup"><span data-stu-id="bed52-127">An **Azure storage account**.</span></span> <span data-ttu-id="bed52-128">U wordt een Azure storage-account gebruiken voor het opslaan van Hallo gegevens in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="bed52-128">You will use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="bed52-129">Als u geen Azure storage-account hebt, raadpleegt u Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) artikel.</span><span class="sxs-lookup"><span data-stu-id="bed52-129">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="bed52-130">Nadat u Hallo storage-account hebt gemaakt, moet u tooobtain Hallo account sleutel tooaccess Hallo opslagruimte hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bed52-130">After you have created hello storage account, you will need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="bed52-131">Zie [beheren van uw toegangssleutels voor opslag](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="bed52-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="bed52-132">Ingericht **SQL Server op een virtuele machine van Azure**.</span><span class="sxs-lookup"><span data-stu-id="bed52-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="bed52-133">Zie voor instructies [instellen van een virtuele machine van Azure SQL-Server als een server IPython Notebook voor geavanceerde analyses](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="bed52-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="bed52-134">Geïnstalleerd en geconfigureerd **Azure PowerShell** lokaal.</span><span class="sxs-lookup"><span data-stu-id="bed52-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="bed52-135">Zie voor instructies [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bed52-135">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="bed52-136"><a name="filesource_to_sqlonazurevm"></a>Verplaatsen van gegevens uit een plat bestand bron tooSQL Server op een Azure VM</span><span class="sxs-lookup"><span data-stu-id="bed52-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="bed52-137">Als uw gegevens zich in een plat bestand (gerangschikt in een indeling rij/kolom), kan het verplaatste tooSQL Server VM op Azure via Hallo volgende methoden zijn:</span><span class="sxs-lookup"><span data-stu-id="bed52-137">If your data is in a flat file (arranged in a row/column format), it can be moved tooSQL Server VM on Azure via hello following methods:</span></span>

1. [<span data-ttu-id="bed52-138">Hulpprogramma voor opdrachtregelprogramma voor het bulksgewijs kopiëren (BCP)</span><span class="sxs-lookup"><span data-stu-id="bed52-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="bed52-139">Bulksgewijs invoegen SQL-Query</span><span class="sxs-lookup"><span data-stu-id="bed52-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="bed52-140">Grafische ingebouwde hulpprogramma's in SQL Server (voor importeren/exporteren, SSIS)</span><span class="sxs-lookup"><span data-stu-id="bed52-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="bed52-141"><a name="insert-tables-bcp"></a>Hulpprogramma voor opdrachtregelprogramma voor het bulksgewijs kopiëren (BCP)</span><span class="sxs-lookup"><span data-stu-id="bed52-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="bed52-142">BCP is een opdrachtregelprogramma dat is geïnstalleerd met SQL Server en één Hallo snelste manieren toomove gegevens.</span><span class="sxs-lookup"><span data-stu-id="bed52-142">BCP is a command-line utility installed with SQL Server and is one of hello quickest ways toomove data.</span></span> <span data-ttu-id="bed52-143">Voor alle drie SQL Server varianten (On-premises SQL Server, SQL Azure en SQL Server VM op Azure) werkt.</span><span class="sxs-lookup"><span data-stu-id="bed52-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="bed52-144">**Waar moet mijn gegevens voor BCP**</span><span class="sxs-lookup"><span data-stu-id="bed52-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="bed52-145">Hoewel niet vereist dat bestanden die zich op dezelfde computer als Hallo doel-SQL-Server kunt u sneller overdrachten (netwerk snelheid tegenover lokale schijf i/o-snelheid) Hallo brongegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="bed52-145">While it is not required, having files containing source data located on hello same machine as hello target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="bed52-146">U kunt verplaatsen Hallo platte bestanden met gegevens toohello machine waarop SQL Server is geïnstalleerd met behulp van verschillende kopiëren hulpprogramma's zoals [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Opslagverkenner](http://storageexplorer.com/) of windows kopiëren en plakken via Extern Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="bed52-146">You can move hello flat files containing data toohello machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="bed52-147">Zorg dat Hallo-database en Hallo tabellen zijn gemaakt op Hallo doel SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="bed52-147">Ensure that hello database and hello tables are created on hello target SQL Server database.</span></span> <span data-ttu-id="bed52-148">Hier volgt een voorbeeld van hoe toodo dat als u met Hallo `Create Database` en `Create Table` opdrachten:</span><span class="sxs-lookup"><span data-stu-id="bed52-148">Here is an example of how toodo that using hello `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="bed52-149">Hallo indelingsbestand genereren die worden beschreven Hallo-schema voor Hallo tabel door uitgifte van de volgende opdracht uit vanaf de opdrachtregel van de machine Hallo HALLO hallo waarop bcp is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bed52-149">Generate hello format file that describes hello schema for hello table by issuing hello following command from hello command-line of hello machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="bed52-150">Hallo gegevens invoegen in Hallo-database met behulp van de bcp-opdracht Hallo als volgt.</span><span class="sxs-lookup"><span data-stu-id="bed52-150">Insert hello data into hello database using hello bcp command as follows.</span></span> <span data-ttu-id="bed52-151">Ervan uitgaande dat hello SQL Server is geïnstalleerd op dezelfde machine moet dit werkt van Hallo opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="bed52-151">This should work from hello command-line assuming that hello SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="bed52-152">**BCP wordt ingevoegd optimaliseren** Raadpleeg het volgende artikel Hallo ['Richtlijnen voor het optimaliseren van bulkimport'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize dergelijke wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="bed52-152">**Optimizing BCP Inserts** Please refer hello following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize such inserts.</span></span>
>
>

### <span data-ttu-id="bed52-153"><a name="insert-tables-bulkquery-parallel"></a>Voegt parallelizing voor snellere verplaatsing van gegevens</span><span class="sxs-lookup"><span data-stu-id="bed52-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="bed52-154">Als u overstapt Hallo-gegevens te groot is, kunt u dingen sneller maken door het gelijktijdig uitvoeren van meerdere BCP opdrachten parallel in een PowerShell-Script.</span><span class="sxs-lookup"><span data-stu-id="bed52-154">If hello data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="bed52-155">**BIG data opname** toooptimize gegevens laden voor grote en zeer grote gegevenssets, partitie-uw logische en fysieke databasetabellen met meerdere tabellen voor bestandsgroepen en partitie.</span><span class="sxs-lookup"><span data-stu-id="bed52-155">**Big data Ingestion** toooptimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="bed52-156">Zie voor meer informatie over het maken en bij het laden van gegevenstabellen toopartition [parallelle Load SQL-partitietabellen](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="bed52-156">For more information about creating and loading data toopartition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="bed52-157">Hallo PowerShell-voorbeeldscript hieronder laten zien parallelle voegt met behulp van bcp:</span><span class="sxs-lookup"><span data-stu-id="bed52-157">hello sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <span data-ttu-id="bed52-158"><a name="insert-tables-bulkquery"></a>Bulksgewijs invoegen SQL-Query</span><span class="sxs-lookup"><span data-stu-id="bed52-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="bed52-159">[Bulksgewijs invoegen SQL-Query](https://msdn.microsoft.com/library/ms188365) gebruikte tooimport gegevens in de database Hallo van rij/kolom op basis van bestanden kunnen worden (Hallo ondersteund typen worden behandeld in de[voorbereiden-gegevens voor bulksgewijs wilt exporteren naar of importeren (SQL Server)](https://msdn.microsoft.com/library/ms188609)) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="bed52-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used tooimport data into hello database from row/column based files (hello supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="bed52-160">Hier volgen enkele Voorbeeldopdrachten voor Bulk Insert zijn zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="bed52-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="bed52-161">Uw gegevens analyseren en eventuele aangepaste opties instellen voordat u ervoor dat SQL Server-database hello wordt ervan uitgegaan dat dezelfde notatie voor de speciale velden zoals datums Hallo toomake importeert.</span><span class="sxs-lookup"><span data-stu-id="bed52-161">Analyze your data and set any custom options before importing toomake sure that hello SQL Server database assumes hello same format for any special fields such as dates.</span></span> <span data-ttu-id="bed52-162">Hier volgt een voorbeeld van hoe tooset Hallo datum opmaken als jaar, maand, dag (als uw gegevens bevat Hallo datum in de notatie voor jaar, maand, dag):</span><span class="sxs-lookup"><span data-stu-id="bed52-162">Here is an example of how tooset hello date format as year-month-day (if your data contains hello date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="bed52-163">Gegevens importeren met bulksgewijs importinstructies:</span><span class="sxs-lookup"><span data-stu-id="bed52-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <span data-ttu-id="bed52-164"><a name="sql-builtin-utilities"></a>Ingebouwde hulpprogramma's in SQL Server</span><span class="sxs-lookup"><span data-stu-id="bed52-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="bed52-165">U kunt SQL Server integraties Services (SSIS) tooimport gegevens in SQL Server VM op Azure uit een plat bestand.</span><span class="sxs-lookup"><span data-stu-id="bed52-165">You can use SQL Server Integrations Services (SSIS) tooimport data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="bed52-166">SSIS is beschikbaar in twee studio omgevingen.</span><span class="sxs-lookup"><span data-stu-id="bed52-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="bed52-167">Zie voor meer informatie [Integration Services (SSIS) en Studio omgevingen](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="bed52-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="bed52-168">Zie voor meer informatie over SQL Server Data Tools [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="bed52-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="bed52-169">Zie voor informatie over de Wizard importeren/exporteren hello, [Wizard SQL Server importeren en exporteren](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="bed52-169">For details on hello Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="bed52-170"><a name="sqlonprem_to_sqlonazurevm"></a>Verplaatsen van gegevens vanuit de lokale SQL Server tooSQL Server op een Azure VM</span><span class="sxs-lookup"><span data-stu-id="bed52-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="bed52-171">U kunt ook de volgende strategieën Hallo gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bed52-171">You can also use hello following migration strategies:</span></span>

1. [<span data-ttu-id="bed52-172">Een Microsoft Azure VM-wizard van SQL Server-Database tooa implementeren</span><span class="sxs-lookup"><span data-stu-id="bed52-172">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="bed52-173">TooFlat bestand exporteren</span><span class="sxs-lookup"><span data-stu-id="bed52-173">Export tooFlat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="bed52-174">Wizard voor migratie van SQL-Database</span><span class="sxs-lookup"><span data-stu-id="bed52-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="bed52-175">Back-up van database maken en terugzetten</span><span class="sxs-lookup"><span data-stu-id="bed52-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="bed52-176">We beschrijven elk van deze hieronder:</span><span class="sxs-lookup"><span data-stu-id="bed52-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a><span data-ttu-id="bed52-177">Een Microsoft Azure VM-wizard van SQL Server-Database tooa implementeren</span><span class="sxs-lookup"><span data-stu-id="bed52-177">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>
<span data-ttu-id="bed52-178">Hallo **implementeren van een Microsoft Azure VM-wizard van SQL Server-Database tooa** zijn de gegevens van een eenvoudige en de aanbevolen manier toomove van een lokale SQL Server-exemplaar tooSQL Server op een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="bed52-178">hello **Deploy a SQL Server Database tooa Microsoft Azure VM wizard** is a simple and recommended way toomove data from an on-premises SQL Server instance tooSQL Server on an Azure VM.</span></span> <span data-ttu-id="bed52-179">Zie voor gedetailleerde stappen evenals een bespreking van de alternatieven, [migreren van een database tooSQL Server op een Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="bed52-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database tooSQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="bed52-180"><a name="export-flat-file"></a>TooFlat bestand exporteren</span><span class="sxs-lookup"><span data-stu-id="bed52-180"><a name="export-flat-file"></a>Export tooFlat File</span></span>
<span data-ttu-id="bed52-181">Verschillende methoden gebruikte toobulk het exporteren van gegevens uit een On-Premises SQL Server kunnen zijn, zoals beschreven in Hallo [bulksgewijs importeren en exporteren van gegevens (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="bed52-181">Various methods can be used toobulk export data from an On-Premises SQL Server as documented in hello [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="bed52-182">Dit document wordt uitgelegd hoe Hallo bulksgewijs kopiëren programma (BCP) als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="bed52-182">This document will cover hello Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="bed52-183">Wanneer gegevens worden geëxporteerd naar een plat bestand, kan het geïmporteerde tooanother SQL server met behulp van bulkimport zijn.</span><span class="sxs-lookup"><span data-stu-id="bed52-183">Once data is exported into a flat file, it can be imported tooanother SQL server using bulk import.</span></span>

1. <span data-ttu-id="bed52-184">Hallo gegevens exporteren uit de lokale SQL Server tooa bestand Hallo bcp hulpprogramma als volgt gebruiken</span><span class="sxs-lookup"><span data-stu-id="bed52-184">Export hello data from on-premises SQL Server tooa File using hello bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="bed52-185">Hallo-database en Hallo tabel maken op virtuele machine van SQL Server op Azure met behulp van Hallo `create database` en `create table` voor Hallo tabelschema in stap 1 hebt geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="bed52-185">Create hello database and hello table on SQL Server VM on Azure using hello `create database` and `create table` for hello table schema exported in step 1.</span></span>
3. <span data-ttu-id="bed52-186">Maak een indelingsbestand voor het beschrijven van het tabelschema Hallo Hallo-gegevens worden geëxporteerd/geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="bed52-186">Create a format file for describing hello table schema of hello data being exported/imported.</span></span> <span data-ttu-id="bed52-187">Details van het indelingsbestand Hallo worden beschreven in [maken van een indelingsbestand (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="bed52-187">Details of hello format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="bed52-188">Indeling Bestandsgeneratie uitgevoerd BCP van Hallo wanneer SQL Server-computer</span><span class="sxs-lookup"><span data-stu-id="bed52-188">Format file generation when running BCP from hello SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="bed52-189">Indeling van bestand genereren met het wanneer BCP op afstand uitvoeren in een SQL-Server</span><span class="sxs-lookup"><span data-stu-id="bed52-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="bed52-190">Gebruik een van Hallo-methoden die zijn beschreven in de sectie [verplaatsen van gegevens van bestandsbron](#filesource_to_sqlonazurevm) toomove Hallo gegevens in platte bestanden tooa SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bed52-190">Use any of hello methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) toomove hello data in flat files tooa SQL Server.</span></span>

### <span data-ttu-id="bed52-191"><a name="sql-migration"></a>Wizard voor migratie van SQL-Database</span><span class="sxs-lookup"><span data-stu-id="bed52-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="bed52-192">[SQL Server-Database Migration Wizard](http://sqlazuremw.codeplex.com/) biedt een gebruiksvriendelijke manier toomove gegevens tussen twee exemplaren van SQL server.</span><span class="sxs-lookup"><span data-stu-id="bed52-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way toomove data between two SQL server instances.</span></span> <span data-ttu-id="bed52-193">Kunt u Hallo gebruiker toomap Hallo gegevensschema tussen bronnen en doeltabellen, kies kolomtypen en verschillende andere functionaliteiten.</span><span class="sxs-lookup"><span data-stu-id="bed52-193">It allows hello user toomap hello data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="bed52-194">Bulksgewijs kopiëren (BCP) wordt gebruikt onder Hallo behandelt.</span><span class="sxs-lookup"><span data-stu-id="bed52-194">It uses bulk copy (BCP) under hello covers.</span></span> <span data-ttu-id="bed52-195">Een schermopname van Hallo welkomstscherm voor Hallo SQL Database Migration wizard worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bed52-195">A screenshot of hello welcome screen for hello SQL Database Migration wizard is shown below.</span></span>  

![Wizard SQL Server-migratie][2]

### <span data-ttu-id="bed52-197"><a name="sql-backup"></a>Back-up van database maken en terugzetten</span><span class="sxs-lookup"><span data-stu-id="bed52-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="bed52-198">SQL Server ondersteunt:</span><span class="sxs-lookup"><span data-stu-id="bed52-198">SQL Server supports:</span></span>

1. <span data-ttu-id="bed52-199">[Back-up van database en de functionaliteit herstellen](https://msdn.microsoft.com/library/ms187048.aspx) (zowel tooa lokale bestand of Bacpac-export tooblob) en [laag gegevenstoepassingen](https://msdn.microsoft.com/library/ee210546.aspx) (met behulp van bacpac).</span><span class="sxs-lookup"><span data-stu-id="bed52-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both tooa local file or bacpac export tooblob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="bed52-200">Mogelijkheid toodirectly wordt SQL Server-VM's in Azure maken met een gekopieerde database of een kopie tooan bestaande Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="bed52-200">Ability toodirectly create SQL Server VMs on Azure with a copied database or copy tooan existing SQL Azure database.</span></span> <span data-ttu-id="bed52-201">Zie voor meer informatie [gebruik Hallo Database-Wizard kopiëren](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="bed52-201">For more details, see [Use hello Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="bed52-202">Een schermopname van Hallo Database back-up/terugzetten opties van SQL Server Management Studio wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bed52-202">A screenshot of hello Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![Hulpprogramma voor het SQL Server importeren][1]

## <a name="resources"></a><span data-ttu-id="bed52-204">Resources</span><span class="sxs-lookup"><span data-stu-id="bed52-204">Resources</span></span>
[<span data-ttu-id="bed52-205">Migreren van een Database tooSQL Server op een Azure VM</span><span class="sxs-lookup"><span data-stu-id="bed52-205">Migrate a Database tooSQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="bed52-206">Overzicht van SQL Server op virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="bed52-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
