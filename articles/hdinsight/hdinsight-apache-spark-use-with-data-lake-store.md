---
title: aaaUse Apache Spark tooanalyze gegevens in Azure Data Lake Store | Microsoft Docs
description: Spark-taken uitvoeren tooanalyze opgeslagen gegevens in Azure Data Lake Store
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a>Gebruik van HDInsight Spark-cluster tooanalyze gegevens in Data Lake Store

In deze zelfstudie gebruikt u Jupyter-notebook beschikbaar met HDInsight Spark-clusters toorun een taak die gegevens uit een Data Lake Store-account leest.

## <a name="prerequisites"></a>Vereisten

* Azure Data Lake Store-account. Volg de instructies Hallo voor [aan de slag met Azure Data Lake Store met Azure Portal Hallo](../data-lake-store/data-lake-store-get-started-portal.md).

* Azure HDInsight Spark-cluster met Data Lake Store als opslag. Volg de instructies Hallo voor [een HDInsight-cluster maken met Data Lake Store met Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    
## <a name="prepare-hello-data"></a>Hallo gegevens voorbereiden

> [!NOTE]
> U hoeft geen tooperform deze stap als u Hallo HDInsight-cluster met Data Lake Store als standaard opslag hebt gemaakt. Hallo cluster vervaardigingsproces voegt voorbeeldgegevens in Hallo Data Lake Store-account die u opgeeft tijdens het Hallo-cluster maken. Toohello sectie overslaan [gebruik HDInsight Spark-cluster met Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).
>
>

Als u een HDInsight-cluster met Data Lake Store als extra opslagruimte en Azure Storage-Blob als standaard opslag gemaakt, moet u eerst kopiëren via sommige sample data toohello Data Lake Store-account. U kunt de voorbeeldgegevens Hallo uit Azure Storage-Blob die is gekoppeld aan de HDInsight-cluster Hallo Hallo gebruiken. U kunt Hallo [ADLCopy hulpprogramma](http://aka.ms/downloadadlcopy) toodo zodat. Download en installeer Hallo hulpprogramma via Hallo-koppeling.

1. Open een opdrachtprompt en navigeer toohello directory waar AdlCopy is geïnstalleerd, doorgaans `%HOMEPATH%\Documents\adlcopy`.

2. Voer Hallo opdracht toocopy na een specifieke blob van Hallo bron container tooa Data Lake Store:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Kopiëren Hallo **HVAC.csv** voorbeeldgegevens op het bestand **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store-account. Hallo-codefragment moet eruitzien als:

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > Controleer of u bestand Hallo en padnamen zijn in de juiste geval Hallo.
   >
   >
3. U zult de vraag tooenter Hallo referenties voor hello Azure-abonnement waaronder die u een Data Lake Store-account hebt. Hier ziet u een vergelijkbare toohello volgende van uitvoer:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    Hallo-gegevensbestand (**HVAC.csv**) in een map worden gekopieerd **/hvac** in Hallo Data Lake Store-account.

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a>Een HDInsight Spark-cluster gebruiken met Data Lake Store

1. Van Hallo [Azure Portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt). U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.

2. Klik vanuit Hallo blade Spark-cluster op **snelkoppelingen**, en klik vervolgens vanuit Hallo **Cluster-Dashboard** blade klikt u op **Jupyter-Notebook**. Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.

   > [!NOTE]
   > U mogelijk ook Hallo Jupyter-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken. Vervang **CLUSTERNAME** met Hallo-naam van het cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Maak een nieuwe notebook. Klik op **Nieuw** en klik vervolgens op **PySpark**.

    ![Een nieuwe Jupyter-notebook maken](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Een nieuwe Jupyter-notebook maken")

4. Omdat u de notebook met behulp van Hallo PySpark-kernel hebt gemaakt, hoeft u geen toocreate contexten expliciet. Hallo Spark en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel Hallo uitvoert. U kunt starten door het Hallo-typen die nodig zijn voor dit scenario te importeren. toodo plakken dus Hallo volgende codefragment in een cel en druk op **SHIFT + ENTER**.

        from pyspark.sql.types import *

    Telkens wanneer u een taak in Jupyter uitvoert, de venstertitel van uw web-browser wordt weergegeven een **(bezet)** status samen met de notebooktitel Hallo. U ziet ook een gevulde cirkel volgende toohello **PySpark** tekst in de rechterbovenhoek Hallo. Nadat het Hallo-taak is voltooid, wordt dit lege cirkel tooa wijzigen.

     ![Status van een Jupyter-notebooktaak](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status van een Jupyter-notebooktaak")

5. Voorbeeldgegevens laden in een tijdelijke tabel met Hallo **HVAC.csv** bestand dat u toohello Data Lake Store-account hebt gekopieerd. Hallo-gegevens in Hallo Hallo URL patroon volgen met Data Lake Store-account, kunt u openen.

    * Als u Data Lake Store als standaard opslag hebt, zijn HVAC.csv op Hallo pad vergelijkbare toohello volgende URL:

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        Of u kunt ook een kortere indeling zoals Hallo volgende gebruiken:

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * Als u Data Lake Store als extra opslagruimte hebt, zijn HVAC.csv op Hallo-locatie waar u hebt gekopieerd, zoals:

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     Vervang in een lege cel, plakken Hallo volgende codevoorbeeld, **MYDATALAKESTORE** met uw Data Lake Store-accountnaam en druk op **SHIFT + ENTER**. Dit codevoorbeeld registreert Hallo gegevens in een tijdelijke tabel genaamd **hvac**.

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. Omdat u een PySpark-kernel gebruikt, u kunt nu rechtstreeks uitvoeren een SQL-query op de tijdelijke tabel Hallo **hvac** dat u zojuist hebt gemaakt met behulp van Hallo `%%sql` verwerkt Magic-pakket. Voor meer informatie over Hallo `%%sql` magic, evenals andere magics die beschikbaar zijn met de PySpark-kernel hello, Zie [beschikbare Kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. Zodra het Hallo-taak is voltooid, wordt standaard Hallo na uitvoer in tabelvorm weergegeven.

      ![Tabeluitvoer van het queryresultaat](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Tabeluitvoer van het queryresultaat")

     U ziet ook Hallo resulteert in een andere visualisaties. Bijvoorbeeld, een gebiedsgrafiek voor dezelfde uitvoer Hallo volgende eruit zou Hallo.

     ![Gebiedsgrafiek van het queryresultaat](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Gebiedsgrafiek van het queryresultaat")

8. Als u klaar bent met het uitvoeren van de toepassing hello moet afsluiten Hallo notebook toorelease Hallo resources. toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**. Deze wordt afgesloten en sluiten Hallo notebook.


## <a name="next-steps"></a>Volgende stappen

* [Een zelfstandige Scala toepassing toorun op Apache Spark-cluster maken](hdinsight-apache-spark-create-standalone-application.md)
* [Gebruik van HDInsight Tools voor IntelliJ toocreate Spark scala-toepassingen voor HDInsight Spark Linux-cluster in Azure Toolkit](hdinsight-apache-spark-intellij-tool-plugin.md)
* [HDInsight-hulpprogramma's gebruiken in Azure Toolkit voor Eclipse toocreate Spark scala-toepassingen voor HDInsight Spark Linux-cluster](hdinsight-apache-spark-eclipse-tool-plugin.md)
