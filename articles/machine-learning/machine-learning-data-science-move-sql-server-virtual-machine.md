---
title: Gegevens verplaatsen naar SQL Server op een virtuele machine in Azure | Microsoft Docs
description: Gegevens uit platte bestanden of verplaatsen van een lokale SQL Server met SQL Server op Azure VM.
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
ms.openlocfilehash: aa0cbba6bdb4cfdfe6ceee50c94f706aa0974924
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-sql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="8997d-103">Gegevens verplaatsen naar SQL Server op een virtuele Azure-machine</span><span class="sxs-lookup"><span data-stu-id="8997d-103">Move data to SQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="8997d-104">In dit onderwerp bevat een overzicht van de opties voor het verplaatsen van gegevens uit platte bestanden (TSV- of CSV-indeling) of van een lokale SQL Server naar SQL Server op Azure een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8997d-104">This topic outlines the options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server to SQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="8997d-105">Deze taken voor het verplaatsen van gegevens naar de cloud maken deel uit van het Team gegevens wetenschap proces.</span><span class="sxs-lookup"><span data-stu-id="8997d-105">These tasks for moving data to the cloud are part of the Team Data Science Process.</span></span>

<span data-ttu-id="8997d-106">Zie voor in dit onderwerp bevat een overzicht van de opties voor het verplaatsen van gegevens naar een Azure SQL Database voor Machine Learning, [gegevens verplaatsen naar een Azure SQL Database voor Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8997d-106">For a topic that outlines the options for moving data to an Azure SQL Database for Machine Learning, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="8997d-107">De **menu** onderstaande koppelingen naar onderwerpen waarin wordt beschreven hoe u opnemen van gegevens in andere omgevingen doel waar de gegevens kunnen worden opgeslagen en verwerkt tijdens het Team gegevens wetenschap proces (TDSP).</span><span class="sxs-lookup"><span data-stu-id="8997d-107">The **menu** below links to topics that describe how to ingest data into other target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="8997d-108">De volgende tabel geeft een overzicht van de opties voor het verplaatsen van gegevens naar SQL Server op Azure een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8997d-108">The following table summarizes the options for moving data to SQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="8997d-109"><b>BRON</b></span><span class="sxs-lookup"><span data-stu-id="8997d-109"><b>SOURCE</b></span></span> | <span data-ttu-id="8997d-110"><b>BESTEMMING: SQL Server op Azure VM</b></span><span class="sxs-lookup"><span data-stu-id="8997d-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="8997d-111"><b>Plat bestand</b></span><span class="sxs-lookup"><span data-stu-id="8997d-111"><b>Flat File</b></span></span> |<span data-ttu-id="8997d-112">1. <a href="#insert-tables-bcp">Hulpprogramma voor opdrachtregelprogramma voor het bulksgewijs kopiëren (BCP)</a></span><span class="sxs-lookup"><span data-stu-id="8997d-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="8997d-113">2. <a href="#insert-tables-bulkquery">Bulksgewijs invoegen SQL-Query</a></span><span class="sxs-lookup"><span data-stu-id="8997d-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="8997d-114">3. <a href="#sql-builtin-utilities">Grafische ingebouwde hulpprogramma's in SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="8997d-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="8997d-115"><b>On-Premises SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="8997d-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="8997d-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Implementeren van een SQL Server-Database naar een Microsoft Azure VM-wizard</a></span><span class="sxs-lookup"><span data-stu-id="8997d-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database to a Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="8997d-117">2. <a href="#export-flat-file">Exporteren naar een plat bestand</a></span><span class="sxs-lookup"><span data-stu-id="8997d-117">2. <a href="#export-flat-file">Export to a flat File </a></span></span><br> <span data-ttu-id="8997d-118">3. <a href="#sql-migration">Wizard voor migratie van SQL-Database</a></span><span class="sxs-lookup"><span data-stu-id="8997d-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="8997d-119">4. <a href="#sql-backup">Back-up van database maken en terugzetten</a></span><span class="sxs-lookup"><span data-stu-id="8997d-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="8997d-120">Let op: dit document wordt ervan uitgegaan dat de SQL-opdrachten worden uitgevoerd vanuit SQL Server Management Studio of Visual Studio Database Explorer.</span><span class="sxs-lookup"><span data-stu-id="8997d-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="8997d-121">Als alternatief kunt u [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) maken en plannen van een pijplijn die de gegevens naar een virtuele machine van SQL Server op Azure verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="8997d-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to create and schedule a pipeline that will move data to a SQL Server VM on Azure.</span></span> <span data-ttu-id="8997d-122">Zie voor meer informatie [kopiëren van gegevens met Azure Data Factory (Kopieeractiviteit)](../data-factory/data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8997d-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="8997d-123"><a name="prereqs"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="8997d-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="8997d-124">Deze zelfstudie wordt ervan uitgegaan dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="8997d-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="8997d-125">Een **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="8997d-125">An **Azure subscription**.</span></span> <span data-ttu-id="8997d-126">Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8997d-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8997d-127">Een **Azure storage-account**.</span><span class="sxs-lookup"><span data-stu-id="8997d-127">An **Azure storage account**.</span></span> <span data-ttu-id="8997d-128">U wordt een Azure storage-account gebruiken voor het opslaan van de gegevens in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8997d-128">You will use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="8997d-129">Zie het artikel [Een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) als u geen account Azure-opslagaccount hebt.</span><span class="sxs-lookup"><span data-stu-id="8997d-129">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="8997d-130">Nadat u het opslagaccount hebt gemaakt, moet u de accountsleutel gebruikt voor toegang tot de opslag verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="8997d-130">After you have created the storage account, you will need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="8997d-131">Zie [beheren van uw toegangssleutels voor opslag](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="8997d-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="8997d-132">Ingericht **SQL Server op een virtuele machine van Azure**.</span><span class="sxs-lookup"><span data-stu-id="8997d-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="8997d-133">Zie voor instructies [instellen van een virtuele machine van Azure SQL-Server als een server IPython Notebook voor geavanceerde analyses](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="8997d-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="8997d-134">Geïnstalleerd en geconfigureerd **Azure PowerShell** lokaal.</span><span class="sxs-lookup"><span data-stu-id="8997d-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="8997d-135">Zie voor instructies [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8997d-135">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="8997d-136"><a name="filesource_to_sqlonazurevm"></a>Verplaatsen van gegevens van een plat bestand-bron met SQL Server op een Azure VM</span><span class="sxs-lookup"><span data-stu-id="8997d-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source to SQL Server on an Azure VM</span></span>
<span data-ttu-id="8997d-137">Als uw gegevens zich in een plat bestand (gerangschikt in een indeling rij/kolom), kan het worden verplaatst naar SQL Server VM op Azure via de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="8997d-137">If your data is in a flat file (arranged in a row/column format), it can be moved to SQL Server VM on Azure via the following methods:</span></span>

1. [<span data-ttu-id="8997d-138">Hulpprogramma voor opdrachtregelprogramma voor het bulksgewijs kopiëren (BCP)</span><span class="sxs-lookup"><span data-stu-id="8997d-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="8997d-139">Bulksgewijs invoegen SQL-Query</span><span class="sxs-lookup"><span data-stu-id="8997d-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="8997d-140">Grafische ingebouwde hulpprogramma's in SQL Server (voor importeren/exporteren, SSIS)</span><span class="sxs-lookup"><span data-stu-id="8997d-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="8997d-141"><a name="insert-tables-bcp"></a>Hulpprogramma voor opdrachtregelprogramma voor het bulksgewijs kopiëren (BCP)</span><span class="sxs-lookup"><span data-stu-id="8997d-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="8997d-142">BCP is een opdrachtregelprogramma dat is geïnstalleerd met SQL Server en is een van de snelste manieren om gegevens te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="8997d-142">BCP is a command-line utility installed with SQL Server and is one of the quickest ways to move data.</span></span> <span data-ttu-id="8997d-143">Voor alle drie SQL Server varianten (On-premises SQL Server, SQL Azure en SQL Server VM op Azure) werkt.</span><span class="sxs-lookup"><span data-stu-id="8997d-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="8997d-144">**Waar moet mijn gegevens voor BCP**</span><span class="sxs-lookup"><span data-stu-id="8997d-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="8997d-145">Hoewel niet vereist, kunt dat bestanden met brongegevens zich op dezelfde computer als de doel-SQL-Server u sneller overdrachten (netwerk snelheid tegenover lokale schijf i/o-snelheid).</span><span class="sxs-lookup"><span data-stu-id="8997d-145">While it is not required, having files containing source data located on the same machine as the target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="8997d-146">Kunt u de platte bestanden met gegevens met de computer waarop SQL Server is geïnstalleerd met behulp van verschillende kopiëren hulpprogramma's zoals [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Opslagverkenner](http://storageexplorer.com/) of windows kopiëren en plakken via Extern bureaublad Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="8997d-146">You can move the flat files containing data to the machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="8997d-147">Zorg ervoor dat de database en de tabellen op de doel-SQL Server-database worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8997d-147">Ensure that the database and the tables are created on the target SQL Server database.</span></span> <span data-ttu-id="8997d-148">Hier volgt een voorbeeld van hoe u doet dit met behulp van de `Create Database` en `Create Table` opdrachten:</span><span class="sxs-lookup"><span data-stu-id="8997d-148">Here is an example of how to do that using the `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="8997d-149">Genereren van het indelingsbestand dat het schema voor de tabel beschrijft de volgende opdracht vanaf de opdrachtregel van de machine waarop bcp is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8997d-149">Generate the format file that describes the schema for the table by issuing the following command from the command-line of the machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="8997d-150">De gegevens invoegen in de database met behulp van de bcp-opdracht als volgt.</span><span class="sxs-lookup"><span data-stu-id="8997d-150">Insert the data into the database using the bcp command as follows.</span></span> <span data-ttu-id="8997d-151">Dit moet werken vanaf de opdrachtregel ervan uitgaande dat de SQL-Server is geïnstalleerd op dezelfde machine:</span><span class="sxs-lookup"><span data-stu-id="8997d-151">This should work from the command-line assuming that the SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="8997d-152">**BCP wordt ingevoegd optimaliseren** raadpleegt u het volgende artikel ['Richtlijnen voor het optimaliseren van bulkimport'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) dergelijke voegt optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="8997d-152">**Optimizing BCP Inserts** Please refer the following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) to optimize such inserts.</span></span>
>
>

### <span data-ttu-id="8997d-153"><a name="insert-tables-bulkquery-parallel"></a>Voegt parallelizing voor snellere verplaatsing van gegevens</span><span class="sxs-lookup"><span data-stu-id="8997d-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="8997d-154">Als de gegevens die u verplaatst groot is, kunt u dingen sneller maken door het gelijktijdig uitvoeren van meerdere BCP opdrachten parallel in een PowerShell-Script.</span><span class="sxs-lookup"><span data-stu-id="8997d-154">If the data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="8997d-155">**BIG data opname** om te optimaliseren voor grote en zeer grote gegevenssets is laden van gegevens, partitie-uw logische en fysieke databasetabellen met meerdere tabellen voor bestandsgroepen en partitie.</span><span class="sxs-lookup"><span data-stu-id="8997d-155">**Big data Ingestion** To optimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="8997d-156">Zie voor meer informatie over het maken en laden van gegevens naar partitietabellen [parallelle Load SQL-partitietabellen](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="8997d-156">For more information about creating and loading data to partition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="8997d-157">De PowerShell-voorbeeldscript hieronder laten zien parallelle voegt met behulp van bcp:</span><span class="sxs-lookup"><span data-stu-id="8997d-157">The sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for the script to execute
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


    # Wait for it all to complete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting the information back from the jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset the execution policy


### <span data-ttu-id="8997d-158"><a name="insert-tables-bulkquery"></a>Bulksgewijs invoegen SQL-Query</span><span class="sxs-lookup"><span data-stu-id="8997d-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="8997d-159">[Bulksgewijs invoegen SQL-Query](https://msdn.microsoft.com/library/ms188365) kan worden gebruikt om gegevens te importeren vanuit de rij/kolom op basis van bestanden in de database (de ondersteunde typen worden behandeld in de[voorbereiden-gegevens voor bulksgewijs wilt exporteren naar of importeren (SQL Server)](https://msdn.microsoft.com/library/ms188609)) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="8997d-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used to import data into the database from row/column based files (the supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="8997d-160">Hier volgen enkele Voorbeeldopdrachten voor Bulk Insert zijn zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="8997d-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="8997d-161">Uw gegevens analyseren en eventuele aangepaste opties instellen voordat u importeert om ervoor te zorgen dat de SQL Server-database wordt ervan uitgegaan dezelfde indeling voor de speciale velden zoals datums dat.</span><span class="sxs-lookup"><span data-stu-id="8997d-161">Analyze your data and set any custom options before importing to make sure that the SQL Server database assumes the same format for any special fields such as dates.</span></span> <span data-ttu-id="8997d-162">Hier volgt een voorbeeld van hoe de datumnotatie instellen als jaar, maand, dag (als uw gegevens de datum in de notatie voor jaar, maand, dag bevat):</span><span class="sxs-lookup"><span data-stu-id="8997d-162">Here is an example of how to set the date format as year-month-day (if your data contains the date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="8997d-163">Gegevens importeren met bulksgewijs importinstructies:</span><span class="sxs-lookup"><span data-stu-id="8997d-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be the row separator in your data
        )

### <span data-ttu-id="8997d-164"><a name="sql-builtin-utilities"></a>Ingebouwde hulpprogramma's in SQL Server</span><span class="sxs-lookup"><span data-stu-id="8997d-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="8997d-165">SQL Server integraties Services (SSIS) kunt u gegevens in SQL Server VM op Azure uit een plat bestand importeren.</span><span class="sxs-lookup"><span data-stu-id="8997d-165">You can use SQL Server Integrations Services (SSIS) to import data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="8997d-166">SSIS is beschikbaar in twee studio omgevingen.</span><span class="sxs-lookup"><span data-stu-id="8997d-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="8997d-167">Zie voor meer informatie [Integration Services (SSIS) en Studio omgevingen](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="8997d-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="8997d-168">Zie voor meer informatie over SQL Server Data Tools [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="8997d-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="8997d-169">Zie voor meer informatie over de Wizard importeren/exporteren [Wizard SQL Server importeren en exporteren](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="8997d-169">For details on the Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="8997d-170"><a name="sqlonprem_to_sqlonazurevm"></a>Verplaatsen van gegevens uit on-premises SQL Server met SQL Server op een Azure VM</span><span class="sxs-lookup"><span data-stu-id="8997d-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server to SQL Server on an Azure VM</span></span>
<span data-ttu-id="8997d-171">U kunt ook de volgende migratiestrategieën gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8997d-171">You can also use the following migration strategies:</span></span>

1. [<span data-ttu-id="8997d-172">Implementeren van een SQL Server-Database naar een Microsoft Azure VM-wizard</span><span class="sxs-lookup"><span data-stu-id="8997d-172">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="8997d-173">Exporteren naar platte bestanden</span><span class="sxs-lookup"><span data-stu-id="8997d-173">Export to Flat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="8997d-174">Wizard voor migratie van SQL-Database</span><span class="sxs-lookup"><span data-stu-id="8997d-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="8997d-175">Back-up van database maken en terugzetten</span><span class="sxs-lookup"><span data-stu-id="8997d-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="8997d-176">We beschrijven elk van deze hieronder:</span><span class="sxs-lookup"><span data-stu-id="8997d-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard"></a><span data-ttu-id="8997d-177">Implementeren van een SQL Server-Database naar een Microsoft Azure VM-wizard</span><span class="sxs-lookup"><span data-stu-id="8997d-177">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>
<span data-ttu-id="8997d-178">De **implementeren van een SQL Server-Database naar een Microsoft Azure VM-wizard** is een eenvoudige en de aanbevolen manier om gegevens te verplaatsen van een lokale SQL Server-exemplaar naar SQL Server op een Azure VM.</span><span class="sxs-lookup"><span data-stu-id="8997d-178">The **Deploy a SQL Server Database to a Microsoft Azure VM wizard** is a simple and recommended way to move data from an on-premises SQL Server instance to SQL Server on an Azure VM.</span></span> <span data-ttu-id="8997d-179">Zie voor gedetailleerde stappen evenals een bespreking van de alternatieven, [migreren van een database met SQL Server op een virtuele machine van Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="8997d-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database to SQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="8997d-180"><a name="export-flat-file"></a>Exporteren naar platte bestanden</span><span class="sxs-lookup"><span data-stu-id="8997d-180"><a name="export-flat-file"></a>Export to Flat File</span></span>
<span data-ttu-id="8997d-181">Verschillende methoden kunnen worden gebruikt voor het bulksgewijs gegevens uit een On-Premises SQL Server exporteren, zoals beschreven in de [bulksgewijs importeren en exporteren van gegevens (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="8997d-181">Various methods can be used to bulk export data from an On-Premises SQL Server as documented in the [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="8997d-182">Dit document wordt uitgelegd hoe de bulksgewijs kopiëren programma (BCP) als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8997d-182">This document will cover the Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="8997d-183">Wanneer gegevens worden geëxporteerd naar een plat bestand, kan deze worden geïmporteerd in een andere SQL-server via bulkimport.</span><span class="sxs-lookup"><span data-stu-id="8997d-183">Once data is exported into a flat file, it can be imported to another SQL server using bulk import.</span></span>

1. <span data-ttu-id="8997d-184">De gegevens uit on-premises SQL-Server te exporteren naar een bestand met het hulpprogramma bcp als volgt</span><span class="sxs-lookup"><span data-stu-id="8997d-184">Export the data from on-premises SQL Server to a File using the bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="8997d-185">De database en de tabel op SQL Server VM maken over het gebruik van Azure de `create database` en `create table` voor het tabelschema geëxporteerd in stap 1.</span><span class="sxs-lookup"><span data-stu-id="8997d-185">Create the database and the table on SQL Server VM on Azure using the `create database` and `create table` for the table schema exported in step 1.</span></span>
3. <span data-ttu-id="8997d-186">Maak een indelingsbestand voor het beschrijven van het tabelschema van de gegevens worden geëxporteerd/geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="8997d-186">Create a format file for describing the table schema of the data being exported/imported.</span></span> <span data-ttu-id="8997d-187">Details van het indelingsbestand worden beschreven in [maken van een indelingsbestand (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="8997d-187">Details of the format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="8997d-188">Indeling van Bestandsgeneratie BCP bij het uitvoeren van de SQL Server-machine</span><span class="sxs-lookup"><span data-stu-id="8997d-188">Format file generation when running BCP from the SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="8997d-189">Indeling van bestand genereren met het wanneer BCP op afstand uitvoeren in een SQL-Server</span><span class="sxs-lookup"><span data-stu-id="8997d-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="8997d-190">Gebruik een van de methoden die worden beschreven in de sectie [verplaatsen van gegevens van bestandsbron](#filesource_to_sqlonazurevm) gegevens in platte bestanden verplaatsen naar een SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8997d-190">Use any of the methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) to move the data in flat files to a SQL Server.</span></span>

### <span data-ttu-id="8997d-191"><a name="sql-migration"></a>Wizard voor migratie van SQL-Database</span><span class="sxs-lookup"><span data-stu-id="8997d-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="8997d-192">[SQL Server-Database Migration Wizard](http://sqlazuremw.codeplex.com/) biedt een gebruiksvriendelijke manier om gegevens te verplaatsen tussen twee exemplaren van SQL server.</span><span class="sxs-lookup"><span data-stu-id="8997d-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way to move data between two SQL server instances.</span></span> <span data-ttu-id="8997d-193">Dit kan de gebruiker toewijzen van het gegevensschema tussen de bronnen en doeltabellen, kiest u kolomtypen en verschillende andere functionaliteiten.</span><span class="sxs-lookup"><span data-stu-id="8997d-193">It allows the user to map the data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="8997d-194">Bulksgewijs kopiëren (BCP) onder de dekt wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8997d-194">It uses bulk copy (BCP) under the covers.</span></span> <span data-ttu-id="8997d-195">Een schermopname van het welkomstscherm voor de migratie van de SQL-Database-wizard worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8997d-195">A screenshot of the welcome screen for the SQL Database Migration wizard is shown below.</span></span>  

![Wizard SQL Server-migratie][2]

### <span data-ttu-id="8997d-197"><a name="sql-backup"></a>Back-up van database maken en terugzetten</span><span class="sxs-lookup"><span data-stu-id="8997d-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="8997d-198">SQL Server ondersteunt:</span><span class="sxs-lookup"><span data-stu-id="8997d-198">SQL Server supports:</span></span>

1. <span data-ttu-id="8997d-199">[Back-up van database en de functionaliteit herstellen](https://msdn.microsoft.com/library/ms187048.aspx) (zowel voor een lokaal bestand of Bacpac-exporteren naar blob) en [laag gegevenstoepassingen](https://msdn.microsoft.com/library/ee210546.aspx) (met behulp van bacpac).</span><span class="sxs-lookup"><span data-stu-id="8997d-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both to a local file or bacpac export to blob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="8997d-200">Mogelijkheid om SQL Server-VM's rechtstreeks in Azure maken met een gekopieerde database of kopiëren naar een bestaande Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="8997d-200">Ability to directly create SQL Server VMs on Azure with a copied database or copy to an existing SQL Azure database.</span></span> <span data-ttu-id="8997d-201">Zie voor meer informatie [de Database-Wizard kopiëren gebruiken](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="8997d-201">For more details, see [Use the Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="8997d-202">Een schermopname van de Database-back-up/terugzetten opties van SQL Server Management Studio wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8997d-202">A screenshot of the Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![Hulpprogramma voor het SQL Server importeren][1]

## <a name="resources"></a><span data-ttu-id="8997d-204">Resources</span><span class="sxs-lookup"><span data-stu-id="8997d-204">Resources</span></span>
[<span data-ttu-id="8997d-205">Een Database migreren naar SQL Server op een virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="8997d-205">Migrate a Database to SQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="8997d-206">Overzicht van SQL Server op virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="8997d-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
