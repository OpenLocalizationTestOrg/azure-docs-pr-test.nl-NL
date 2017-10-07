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
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a>Kopiëren van gegevens tussen Data Lake Store en Azure SQL database met Sqoop
Meer informatie over hoe toouse Apache Sqoop tooimport en exporteren van gegevens tussen Azure SQL Database- en Data Lake Store.

## <a name="what-is-sqoop"></a>Wat is Sqoop?
BIG data-toepassingen zijn een natuurlijke keuze voor het verwerken van ongestructureerde en semi-gestructureerde gegevens, zoals Logboeken en -bestanden. Er kan ook wel een noodzaak tooprocess gestructureerde gegevens die zijn opgeslagen in de relationele databases.

[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is een hulpprogramma waarmee u tootransfer gegevens tussen relationele databases en een big data-opslagplaats, zoals Data Lake Store. U kunt deze tooimport gegevens uit een relationele databasebeheersysteem (RDBMS) zoals Azure SQL Database in Data Lake Store. U kunt transformeert en gegevens te analyseren Hallo met big data-workloads en Hallo gegevens vervolgens exporteren naar een RDBMS. In deze zelfstudie maakt u een Azure SQL Database gebruiken als uw relationele database-tooimport/exporteren uit.

## <a name="prerequisites"></a>Vereisten
Voordat u dit artikel, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure Data Lake Store-account**. Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Azure HDInsight-cluster** met toegang tooa Data Lake Store-account. Zie [een HDInsight-cluster maken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). In dit artikel wordt ervan uitgegaan dat u een HDInsight Linux-cluster met Data Lake Store toegang hebt.
* **Azure SQL-database**. Voor instructies over het toocreate één, Zie [maken van een Azure SQL database](../sql-database/sql-database-get-started.md)

## <a name="do-you-learn-fast-with-videos"></a>Leert u snel met video's?
[Bekijk deze video](https://mix.office.com/watch/1butcdjxmu114) over het toocopy gegevens tussen Azure Storage-Blobs en Data Lake Store met DistCp.

## <a name="create-sample-tables-in-hello-azure-sql-database"></a>Maken van tabellen in hello Azure SQL Database
1. toostart, twee tabellen in hello Azure SQL Database maken. Gebruik [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) of Visual Studio tooconnect toohello Azure SQL Database en vervolgens uitvoeren Hallo query's.

    **Table1 maken**

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

    **Tabel2 maken**

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
2. In **Table1**, voorbeeldgegevens toevoegen. Laat **Table2** leeg. We het importeren van gegevens van **Table1** in Data Lake Store. Vervolgens we gegevens worden geëxporteerd van Data Lake Store in **Table2**. Hallo volgende codefragment worden uitgevoerd.

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a>Sqoop gebruik van een HDInsight-cluster met toegang tot tooData Lake Store
Een HDInsight-cluster heeft al Hallo Sqoop pakketten beschikbaar. Als u hebt Hallo HDInsight cluster toouse Data Lake Store als extra opslag geconfigureerd, kunt u Sqoop (zonder configuratiewijzigingen) tooimport/exporteren van gegevens tussen een relationele database (in dit voorbeeld wordt een Azure SQL Database) en een Data Lake Store account.

1. Voor deze zelfstudie we wordt ervan uitgegaan dat u een Linux-cluster hebt gemaakt, zodat u SSH tooconnect toohello cluster moet gebruiken. Zie [Connect tooa Linux gebaseerde HDInsight-cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).
2. Controleer of u toegang hebt tot Hallo Data Lake Store-account uit Hallo-cluster. Hallo volgende opdracht uit Hallo SSH prompt uitvoeren:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    Dit moet een lijst met bestanden/mappen in Hallo Data Lake Store-account op te geven.

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a>Gegevens importeren uit Azure SQL Database in Data Lake Store
1. Navigeer toohello directory waar Sqoop pakketten beschikbaar zijn. Dit wordt normaal gesproken worden op `/usr/hdp/<version>/sqoop/bin`.
2. Hallo gegevens importeren uit **Table1** in Hallo Data Lake Store-account. Gebruik de volgende syntaxis Hallo:

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    Houd er rekening mee dat **sql-database-server-name** aanduiding Hallo-naam van het Hallo-server waarop hello Azure SQL-database wordt uitgevoerd. **naam van een SQL-database** aanduiding Hallo werkelijke databasenaam.

    Bijvoorbeeld:


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. Controleer of deze Hallo gegevens zijn overgedragen toohello Data Lake Store-account. Hallo volgende opdracht uitvoeren:

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    U ziet Hallo na uitvoer.


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    Elke **onderdeel-m -*** bestand overeenkomt met tooa rij in de brontabel hello, **Table1**. U kunt inhoud Hallo Hallo deel - m - weergeven * tooverify bestanden.


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a>Gegevens uit Data Lake Store exporteren naar Azure SQL Database
1. Hallo gegevens exporteren uit Data Lake Store-account toohello lege tabel, **Table2**, in hello Azure SQL Database. Gebruik de volgende syntaxis Hallo.

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    Bijvoorbeeld:


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. Controleer of die gegevens Hallo geüpload toohello SQL Database-tabel. Gebruik [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) of Visual Studio tooconnect toohello Azure SQL Database en vervolgens uitvoeren Hallo query.

        SELECT * FROM TABLE2

    Dit moet Hallo na uitvoer hebben.

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a>Prestatie-overwegingen bij het gebruik van Sqoop

Zie voor prestaties afstemmen uw Sqoop taak toocopy data tooData Lake Store, [Sqoop prestaties document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).

## <a name="see-also"></a>Zie ook
* [Gegevens kopiëren van Azure Storage Blobs tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
