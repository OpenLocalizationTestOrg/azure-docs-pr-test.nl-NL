---
title: aaaCopy gegevens tussen Data Lake Store en Azure SQL database met Sqoop | Microsoft Docs
description: Sqoop toocopy gegevens gebruiken tussen Azure SQL Database- en Data Lake Store
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
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="e41f8-103">Kopiëren van gegevens tussen Data Lake Store en Azure SQL database met Sqoop</span><span class="sxs-lookup"><span data-stu-id="e41f8-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="e41f8-104">Meer informatie over hoe toouse Apache Sqoop tooimport en exporteren van gegevens tussen Azure SQL Database- en Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e41f8-104">Learn how toouse Apache Sqoop tooimport and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="e41f8-105">Wat is Sqoop?</span><span class="sxs-lookup"><span data-stu-id="e41f8-105">What is Sqoop?</span></span>
<span data-ttu-id="e41f8-106">BIG data-toepassingen zijn een natuurlijke keuze voor het verwerken van ongestructureerde en semi-gestructureerde gegevens, zoals Logboeken en -bestanden.</span><span class="sxs-lookup"><span data-stu-id="e41f8-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="e41f8-107">Er kan ook wel een noodzaak tooprocess gestructureerde gegevens die zijn opgeslagen in de relationele databases.</span><span class="sxs-lookup"><span data-stu-id="e41f8-107">However, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="e41f8-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is een hulpprogramma waarmee u tootransfer gegevens tussen relationele databases en een big data-opslagplaats, zoals Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e41f8-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed tootransfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="e41f8-109">U kunt deze tooimport gegevens uit een relationele databasebeheersysteem (RDBMS) zoals Azure SQL Database in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e41f8-109">You can use it tooimport data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="e41f8-110">U kunt transformeert en gegevens te analyseren Hallo met big data-workloads en Hallo gegevens vervolgens exporteren naar een RDBMS.</span><span class="sxs-lookup"><span data-stu-id="e41f8-110">You can then transform and analyze hello data using big data workloads and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="e41f8-111">In deze zelfstudie maakt u een Azure SQL Database gebruiken als uw relationele database-tooimport/exporteren uit.</span><span class="sxs-lookup"><span data-stu-id="e41f8-111">In this tutorial, you use an Azure SQL Database as your relational database tooimport/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e41f8-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e41f8-112">Prerequisites</span></span>
<span data-ttu-id="e41f8-113">Voordat u dit artikel, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="e41f8-113">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="e41f8-114">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="e41f8-114">**An Azure subscription**.</span></span> <span data-ttu-id="e41f8-115">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e41f8-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e41f8-116">**Een Azure Data Lake Store-account**.</span><span class="sxs-lookup"><span data-stu-id="e41f8-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="e41f8-117">Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e41f8-117">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="e41f8-118">**Azure HDInsight-cluster** met toegang tooa Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="e41f8-118">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="e41f8-119">Zie [een HDInsight-cluster maken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e41f8-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="e41f8-120">In dit artikel wordt ervan uitgegaan dat u een HDInsight Linux-cluster met Data Lake Store toegang hebt.</span><span class="sxs-lookup"><span data-stu-id="e41f8-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="e41f8-121">**Azure SQL-database**.</span><span class="sxs-lookup"><span data-stu-id="e41f8-121">**Azure SQL Database**.</span></span> <span data-ttu-id="e41f8-122">Voor instructies over het toocreate één, Zie [maken van een Azure SQL database](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="e41f8-122">For instructions on how toocreate one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="e41f8-123">Leert u snel met video's?</span><span class="sxs-lookup"><span data-stu-id="e41f8-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="e41f8-124">[Bekijk deze video](https://mix.office.com/watch/1butcdjxmu114) over het toocopy gegevens tussen Azure Storage-Blobs en Data Lake Store met DistCp.</span><span class="sxs-lookup"><span data-stu-id="e41f8-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-hello-azure-sql-database"></a><span data-ttu-id="e41f8-125">Maken van tabellen in hello Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e41f8-125">Create sample tables in hello Azure SQL Database</span></span>
1. <span data-ttu-id="e41f8-126">toostart, twee tabellen in hello Azure SQL Database maken.</span><span class="sxs-lookup"><span data-stu-id="e41f8-126">toostart with, create two sample tables in hello Azure SQL Database.</span></span> <span data-ttu-id="e41f8-127">Gebruik [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) of Visual Studio tooconnect toohello Azure SQL Database en vervolgens uitvoeren Hallo query's.</span><span class="sxs-lookup"><span data-stu-id="e41f8-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following queries.</span></span>

    <span data-ttu-id="e41f8-128">**Table1 maken**</span><span class="sxs-lookup"><span data-stu-id="e41f8-128">**Create Table1**</span></span>

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

    <span data-ttu-id="e41f8-129">**Tabel2 maken**</span><span class="sxs-lookup"><span data-stu-id="e41f8-129">**Create Table2**</span></span>

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
2. <span data-ttu-id="e41f8-130">In **Table1**, voorbeeldgegevens toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e41f8-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="e41f8-131">Laat **Table2** leeg.</span><span class="sxs-lookup"><span data-stu-id="e41f8-131">Leave **Table2** empty.</span></span> <span data-ttu-id="e41f8-132">We het importeren van gegevens van **Table1** in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e41f8-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="e41f8-133">Vervolgens we gegevens worden geëxporteerd van Data Lake Store in **Table2**.</span><span class="sxs-lookup"><span data-stu-id="e41f8-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="e41f8-134">Hallo volgende codefragment worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e41f8-134">Run hello following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a><span data-ttu-id="e41f8-135">Sqoop gebruik van een HDInsight-cluster met toegang tot tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="e41f8-135">Use Sqoop from an HDInsight cluster with access tooData Lake Store</span></span>
<span data-ttu-id="e41f8-136">Een HDInsight-cluster heeft al Hallo Sqoop pakketten beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="e41f8-136">An HDInsight cluster already has hello Sqoop packages available.</span></span> <span data-ttu-id="e41f8-137">Als u hebt Hallo HDInsight cluster toouse Data Lake Store als extra opslag geconfigureerd, kunt u Sqoop (zonder configuratiewijzigingen) tooimport/exporteren van gegevens tussen een relationele database (in dit voorbeeld wordt een Azure SQL Database) en een Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="e41f8-137">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) tooimport/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="e41f8-138">Voor deze zelfstudie we wordt ervan uitgegaan dat u een Linux-cluster hebt gemaakt, zodat u SSH tooconnect toohello cluster moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e41f8-138">For this tutorial, we assume you created a Linux cluster so you should use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="e41f8-139">Zie [Connect tooa Linux gebaseerde HDInsight-cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e41f8-139">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="e41f8-140">Controleer of u toegang hebt tot Hallo Data Lake Store-account uit Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e41f8-140">Verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="e41f8-141">Hallo volgende opdracht uit Hallo SSH prompt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e41f8-141">Run hello following command from hello SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="e41f8-142">Dit moet een lijst met bestanden/mappen in Hallo Data Lake Store-account op te geven.</span><span class="sxs-lookup"><span data-stu-id="e41f8-142">This should provide a list of files/folders in hello Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="e41f8-143">Gegevens importeren uit Azure SQL Database in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e41f8-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="e41f8-144">Navigeer toohello directory waar Sqoop pakketten beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="e41f8-144">Navigate toohello directory where Sqoop packages are available.</span></span> <span data-ttu-id="e41f8-145">Dit wordt normaal gesproken worden op `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="e41f8-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="e41f8-146">Hallo gegevens importeren uit **Table1** in Hallo Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="e41f8-146">Import hello data from **Table1** into hello Data Lake Store account.</span></span> <span data-ttu-id="e41f8-147">Gebruik de volgende syntaxis Hallo:</span><span class="sxs-lookup"><span data-stu-id="e41f8-147">Use hello following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="e41f8-148">Houd er rekening mee dat **sql-database-server-name** aanduiding Hallo-naam van het Hallo-server waarop hello Azure SQL-database wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e41f8-148">Note that **sql-database-server-name** placeholder represents hello name of hello server where hello Azure SQL database is running.</span></span> <span data-ttu-id="e41f8-149">**naam van een SQL-database** aanduiding Hallo werkelijke databasenaam.</span><span class="sxs-lookup"><span data-stu-id="e41f8-149">**sql-database-name** placeholder represents hello actual database name.</span></span>

    <span data-ttu-id="e41f8-150">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e41f8-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="e41f8-151">Controleer of deze Hallo gegevens zijn overgedragen toohello Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="e41f8-151">Verify that hello data has been transferred toohello Data Lake Store account.</span></span> <span data-ttu-id="e41f8-152">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e41f8-152">Run hello following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="e41f8-153">U ziet Hallo na uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e41f8-153">You should see hello following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="e41f8-154">Elke **onderdeel-m -*** bestand overeenkomt met tooa rij in de brontabel hello, **Table1**.</span><span class="sxs-lookup"><span data-stu-id="e41f8-154">Each **part-m-*** file corresponds tooa row in hello source table, **Table1**.</span></span> <span data-ttu-id="e41f8-155">U kunt inhoud Hallo Hallo deel - m - weergeven * tooverify bestanden.</span><span class="sxs-lookup"><span data-stu-id="e41f8-155">You can view hello contents of hello part-m-* files tooverify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="e41f8-156">Gegevens uit Data Lake Store exporteren naar Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e41f8-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="e41f8-157">Hallo gegevens exporteren uit Data Lake Store-account toohello lege tabel, **Table2**, in hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e41f8-157">Export hello data from Data Lake Store account toohello empty table, **Table2**, in hello Azure SQL Database.</span></span> <span data-ttu-id="e41f8-158">Gebruik de volgende syntaxis Hallo.</span><span class="sxs-lookup"><span data-stu-id="e41f8-158">Use hello following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="e41f8-159">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e41f8-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="e41f8-160">Controleer of die gegevens Hallo geüpload toohello SQL Database-tabel.</span><span class="sxs-lookup"><span data-stu-id="e41f8-160">Verify that hello data was uploaded toohello SQL Database table.</span></span> <span data-ttu-id="e41f8-161">Gebruik [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) of Visual Studio tooconnect toohello Azure SQL Database en vervolgens uitvoeren Hallo query.</span><span class="sxs-lookup"><span data-stu-id="e41f8-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="e41f8-162">Dit moet Hallo na uitvoer hebben.</span><span class="sxs-lookup"><span data-stu-id="e41f8-162">This should have hello following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="e41f8-163">Prestatie-overwegingen bij het gebruik van Sqoop</span><span class="sxs-lookup"><span data-stu-id="e41f8-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="e41f8-164">Zie voor prestaties afstemmen uw Sqoop taak toocopy data tooData Lake Store, [Sqoop prestaties document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="e41f8-164">For performance tuning your Sqoop job toocopy data tooData Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="e41f8-165">Zie ook</span><span class="sxs-lookup"><span data-stu-id="e41f8-165">See also</span></span>
* [<span data-ttu-id="e41f8-166">Gegevens kopiëren van Azure Storage Blobs tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="e41f8-166">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="e41f8-167">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="e41f8-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="e41f8-168">Azure Data Lake Analytics gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e41f8-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="e41f8-169">Azure HDInsight gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e41f8-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
