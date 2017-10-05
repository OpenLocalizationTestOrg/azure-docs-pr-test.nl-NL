---
title: "Kopiëren van gegevens tussen Data Lake Store en Azure SQL database met Sqoop | Microsoft Docs"
description: "Sqoop gebruiken om gegevens tussen Azure SQL Database- en Data Lake Store te kopiëren"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 53bf33f6027f1f365bd92251490d5c851fb83f8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="1dfd8-103">Kopiëren van gegevens tussen Data Lake Store en Azure SQL database met Sqoop</span><span class="sxs-lookup"><span data-stu-id="1dfd8-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="1dfd8-104">Informatie over het Apache Sqoop gebruiken om te importeren en exporteren van gegevens tussen Azure SQL Database- en Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-104">Learn how to use Apache Sqoop to import and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="1dfd8-105">Wat is Sqoop?</span><span class="sxs-lookup"><span data-stu-id="1dfd8-105">What is Sqoop?</span></span>
<span data-ttu-id="1dfd8-106">BIG data-toepassingen zijn een natuurlijke keuze voor het verwerken van ongestructureerde en semi-gestructureerde gegevens, zoals Logboeken en -bestanden.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="1dfd8-107">Er kan ook wel nodig om gestructureerde gegevens die zijn opgeslagen in de relationele databases te verwerken.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-107">However, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="1dfd8-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is een hulpprogramma waarmee gegevens worden overgebracht tussen relationele databases en een big data-opslagplaats, zoals Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed to transfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="1dfd8-109">U kunt deze gebruiken om gegevens te importeren uit een relationele databasebeheersysteem (RDBMS) zoals Azure SQL Database in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-109">You can use it to import data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="1dfd8-110">U kunt vervolgens transformeren en analyseren van de gegevens met behulp van big data-workloads en de gegevens vervolgens exporteren naar een RDBMS.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-110">You can then transform and analyze the data using big data workloads and then export the data back into an RDBMS.</span></span> <span data-ttu-id="1dfd8-111">In deze zelfstudie kunt u een Azure SQL Database als uw relationele database importeren/exporteren uit.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-111">In this tutorial, you use an Azure SQL Database as your relational database to import/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dfd8-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1dfd8-112">Prerequisites</span></span>
<span data-ttu-id="1dfd8-113">Voordat u dit artikel gaat lezen, moet u beschikken over het volgende:</span><span class="sxs-lookup"><span data-stu-id="1dfd8-113">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="1dfd8-114">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-114">**An Azure subscription**.</span></span> <span data-ttu-id="1dfd8-115">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1dfd8-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1dfd8-116">**Een Azure Data Lake Store-account**.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="1dfd8-117">Zie voor instructies over het maken van een [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1dfd8-117">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="1dfd8-118">**Azure HDInsight-cluster** met toegang tot een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-118">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="1dfd8-119">Zie [een HDInsight-cluster maken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1dfd8-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="1dfd8-120">In dit artikel wordt ervan uitgegaan dat u een HDInsight Linux-cluster met Data Lake Store toegang hebt.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="1dfd8-121">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-121">**Azure SQL Database**.</span></span> <span data-ttu-id="1dfd8-122">Zie voor instructies over het maken van een [maken van een Azure SQL database](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="1dfd8-122">For instructions on how to create one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="1dfd8-123">Leert u snel met video's?</span><span class="sxs-lookup"><span data-stu-id="1dfd8-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="1dfd8-124">[Bekijk deze video](https://mix.office.com/watch/1butcdjxmu114) voor het kopiëren van gegevens tussen Azure Storage-Blobs en Data Lake Store met DistCp.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-the-azure-sql-database"></a><span data-ttu-id="1dfd8-125">Maken van tabellen in de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1dfd8-125">Create sample tables in the Azure SQL Database</span></span>
1. <span data-ttu-id="1dfd8-126">Worden gestart met twee tabellen in de Azure SQL Database maken.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-126">To start with, create two sample tables in the Azure SQL Database.</span></span> <span data-ttu-id="1dfd8-127">Gebruik [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) of Visual Studio verbinding maken met de Azure SQL Database en voer de volgende query's.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following queries.</span></span>

    <span data-ttu-id="1dfd8-128">**Table1 maken**</span><span class="sxs-lookup"><span data-stu-id="1dfd8-128">**Create Table1**</span></span>

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    <span data-ttu-id="1dfd8-129">**Tabel2 maken**</span><span class="sxs-lookup"><span data-stu-id="1dfd8-129">**Create Table2**</span></span>

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. <span data-ttu-id="1dfd8-130">In **Table1**, voorbeeldgegevens toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="1dfd8-131">Laat **Table2** leeg.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-131">Leave **Table2** empty.</span></span> <span data-ttu-id="1dfd8-132">We het importeren van gegevens van **Table1** in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="1dfd8-133">Vervolgens we gegevens worden geëxporteerd van Data Lake Store in **Table2**.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="1dfd8-134">Voer het volgende fragment.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-134">Run the following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-to-data-lake-store"></a><span data-ttu-id="1dfd8-135">Sqoop gebruiken van een HDInsight-cluster met toegang naar Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1dfd8-135">Use Sqoop from an HDInsight cluster with access to Data Lake Store</span></span>
<span data-ttu-id="1dfd8-136">Een HDInsight-cluster heeft al het Sqoop pakketten beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-136">An HDInsight cluster already has the Sqoop packages available.</span></span> <span data-ttu-id="1dfd8-137">Als u het HDInsight-cluster voor het gebruik van Data Lake Store als extra opslag hebt geconfigureerd, kunt u Sqoop gebruiken (zonder configuratiewijzigingen) te importeren/exporteren van gegevens tussen een relationele database (in dit voorbeeld wordt een Azure SQL Database) en een Data Lake Store-account .</span><span class="sxs-lookup"><span data-stu-id="1dfd8-137">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) to import/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="1dfd8-138">Voor deze zelfstudie we wordt ervan uitgegaan dat u een Linux-cluster hebt gemaakt, dus u SSH gebruiken moet om verbinding met het cluster.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-138">For this tutorial, we assume you created a Linux cluster so you should use SSH to connect to the cluster.</span></span> <span data-ttu-id="1dfd8-139">Zie [verbinding maken met een Linux gebaseerde HDInsight-cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1dfd8-139">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="1dfd8-140">Controleer of u toegang hebt tot het Data Lake Store-account van het cluster.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-140">Verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="1dfd8-141">Voer de volgende opdracht achter de SSH-opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="1dfd8-141">Run the following command from the SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="1dfd8-142">Dit moet een lijst met bestanden/mappen in het Data Lake Store-account op te geven.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-142">This should provide a list of files/folders in the Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="1dfd8-143">Gegevens importeren uit Azure SQL Database in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1dfd8-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="1dfd8-144">Ga naar de map waar Sqoop pakketten beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-144">Navigate to the directory where Sqoop packages are available.</span></span> <span data-ttu-id="1dfd8-145">Dit wordt normaal gesproken worden op `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="1dfd8-146">De gegevens importeren uit **Table1** bij de Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-146">Import the data from **Table1** into the Data Lake Store account.</span></span> <span data-ttu-id="1dfd8-147">Gebruik de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="1dfd8-147">Use the following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="1dfd8-148">Houd er rekening mee dat **sql-database-server-name** tijdelijke aanduiding vertegenwoordigt de naam van de server waarop de Azure SQL database wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-148">Note that **sql-database-server-name** placeholder represents the name of the server where the Azure SQL database is running.</span></span> <span data-ttu-id="1dfd8-149">**naam van een SQL-database** tijdelijke aanduiding voor de werkelijke databasenaam vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-149">**sql-database-name** placeholder represents the actual database name.</span></span>

    <span data-ttu-id="1dfd8-150">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1dfd8-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="1dfd8-151">Controleer of dat de gegevens is overgebracht naar het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-151">Verify that the data has been transferred to the Data Lake Store account.</span></span> <span data-ttu-id="1dfd8-152">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="1dfd8-152">Run the following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="1dfd8-153">Hier ziet u de volgende uitvoer.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-153">You should see the following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="1dfd8-154">Elke **onderdeel-m -*** bestand komt overeen met een rij in de brontabel **Table1**.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-154">Each **part-m-*** file corresponds to a row in the source table, **Table1**.</span></span> <span data-ttu-id="1dfd8-155">U kunt de inhoud van het onderdeel - m - weergeven * bestanden om te controleren.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-155">You can view the contents of the part-m-* files to verify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="1dfd8-156">Gegevens uit Data Lake Store exporteren naar Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1dfd8-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="1dfd8-157">De gegevens van Data Lake Store-account exporteren naar de tabel leeg **Table2**, in de Azure SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-157">Export the data from Data Lake Store account to the empty table, **Table2**, in the Azure SQL Database.</span></span> <span data-ttu-id="1dfd8-158">Gebruik de volgende syntaxis.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-158">Use the following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="1dfd8-159">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1dfd8-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="1dfd8-160">Controleer of dat de gegevens is geüpload naar de SQL-databasetabel.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-160">Verify that the data was uploaded to the SQL Database table.</span></span> <span data-ttu-id="1dfd8-161">Gebruik [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) of Visual Studio verbinding maken met de Azure SQL Database en voer vervolgens de volgende query.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="1dfd8-162">Dit moet de volgende uitvoer hebben.</span><span class="sxs-lookup"><span data-stu-id="1dfd8-162">This should have the following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="1dfd8-163">Prestatie-overwegingen bij het gebruik van Sqoop</span><span class="sxs-lookup"><span data-stu-id="1dfd8-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="1dfd8-164">Zie voor prestaties afstemmen van de taak Sqoop om gegevens te kopiëren naar Data Lake Store, [Sqoop prestaties document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="1dfd8-164">For performance tuning your Sqoop job to copy data to Data Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="1dfd8-165">Zie ook</span><span class="sxs-lookup"><span data-stu-id="1dfd8-165">See also</span></span>
* [<span data-ttu-id="1dfd8-166">Gegevens kopiëren van Azure Storage-Blobs naar Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1dfd8-166">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="1dfd8-167">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="1dfd8-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="1dfd8-168">Azure Data Lake Analytics gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1dfd8-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="1dfd8-169">Azure HDInsight gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1dfd8-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
