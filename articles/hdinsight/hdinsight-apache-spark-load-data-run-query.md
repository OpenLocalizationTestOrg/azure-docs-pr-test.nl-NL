---
title: aaaRun interactieve query's in een Azure HDInsight Spark-cluster | Microsoft Docs
description: HDInsight Spark Quick Start op hoe toocreate een Apache Spark-cluster in HDInsight.
keywords: spark-snelstartgids,interactieve spark,interactieve query,hdinsight spark,azure spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a>Interactieve query's uitvoeren op een HDInsight Spark-cluster

In dit artikel gebruikt u een Jupyter-notebook toorun interactieve Spark SQL-query's op basis van een Spark-cluster. Jupyter-notebook is een browsertoepassing die uitgebreider is dan Hallo interactieve ervaring via de console toohello Web. Zie voor meer informatie [hello Jupyter-notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).

Voor deze zelfstudie maakt u Hallo **PySpark** kernel in Hallo Jupyter-notebook toorun een interactieve Spark SQL-query. Jupyter-notebooks op HDInsight-clusters bieden ook ondersteuning voor twee andere kernels - **PySpark3** en **Spark**. Voor meer informatie over Hallo kernels en voordelen van het gebruik van Hallo **PySpark**, Zie [gebruik Jupyter-notebook kernels met Apache Spark-clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Vereisten

* **Een Azure HDInsight Spark-cluster**. Zie voor instructies [een Apache Spark-cluster maken in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a>Een Jupyter-notebook toorun interactieve query's maken

toorun query's, gebruiken we voorbeeldgegevens die standaard beschikbaar in Hallo opslag die is gekoppeld aan het Hallo-cluster. U moet echter eerst die gegevens laden in Spark als een dataframe. Zodra u Hallo dataframe hebt, kunt u query's uitvoeren op Hallo Jupyter-notebook met. In dit gedeelte kijken hoe in:

* Een verzameling voorbeeldgegevens registreren als een Spark-dataframe.
* Query's uitvoeren op Hallo dataframe.

1. Open Hallo [Azure-portal](https://portal.azure.com/). Als u toopin Hallo cluster toohello-dashboard hebt gekozen, klikt u op Hallo cluster tegel Hallo dashboard toolaunch Hallo cluster blade.

    Als u niet Hallo cluster toohello dashboard in het linkerdeelvenster hello vastmaken, klikt u op **HDInsight-clusters**, en klik vervolgens op Hallo cluster die u hebt gemaakt.

3. Klik in **Snelkoppelingen** op **Clusterdashboards** en klik vervolgens op **Jupyter Notebook**. Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.

   ![Open Jupyter-notebook toorun interactieve Spark SQL-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter-notebook toorun interactieve Spark SQL-query")

   > [!NOTE]
   > Hallo Jupyter-notebook zijn ook toegankelijk voor uw cluster door openen Hallo URL te volgen in uw browser. Vervang **CLUSTERNAME** met Hallo-naam van het cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Maak een notebook. Klik op **Nieuw** en klik vervolgens op **PySpark**.

   ![Maken van een Jupyter-notebook toorun interactieve Spark SQL-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "maken van een Jupyter-notebook toorun interactieve Spark SQL-query")

   Een nieuwe notebook gemaakt en geopend met de naam van de Hallo Untitled(Untitled.pynb).

4. Klik op Hallo notebook naam Hallo boven en een beschrijvende naam invoeren als u wilt.

    ![Geef een naam op voor Hallo Jupter notebook toorun interactieve Spark query van](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "voor Hallo Jupter notebook toorun interactieve Spark query van een naam opgeven")

5. Plakken Hallo volgende code in een lege cel en druk vervolgens op **SHIFT + ENTER** toorun Hallo code. Hallo code invoer Hallo-typen die nodig zijn voor dit scenario:

        from pyspark.sql.types import *

    Omdat u de notebook met behulp van Hallo PySpark-kernel hebt gemaakt, hoeft u geen toocreate contexten expliciet. Hallo Spark en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel Hallo uitvoert.

    ![Status van interactieve Spark SQL-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status van interactieve Spark SQL-query")

    Telkens wanneer u een interactieve query in Jupyter uitvoert, ziet u de venstertitel van uw web-browser een **(bezet)** status samen met de notebooktitel Hallo. U ziet ook een gevulde cirkel volgende toohello **PySpark** tekst in de rechterbovenhoek Hallo. Nadat het Hallo-taak is voltooid, verandert deze tooa lege cirkel.

6. Voordat u Hallo gegevens laden in een Spark-cluster, kunt u ons een momentopname van het zoeken. Hallo voorbeeldgegevens gebruikt in deze zelfstudie is beschikbaar als een CSV-bestand op alle HDInsight Spark-clusters op **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**. Hallo-gegevens worden vastgelegd Hallo temperatuur variaties van een gebouw. Hier volgen Hallo eerste paar rijen van Hallo-gegevens.

    ![Momentopname van gegevens voor interactieve Spark SQL-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "momentopname voor interactieve Spark SQL-query")

6. Maak een dataframe en een tijdelijke tabel (**hvac**) door het uitvoeren van de volgende code Hallo. Voor deze zelfstudie maken we geen alle Hallo kolommen in de tijdelijke tabel Hallo als vergeleken toohello kolommen in Hallo onbewerkte CSV-gegevens. 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Zodra Hallo-tabel is gemaakt, interactieve query uitvoeren op Hallo van gegevens, gebruikt u Hallo code te volgen.

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   Omdat u een PySpark-kernel gebruikt, u kunt nu rechtstreeks een interactieve SQL query uitvoeren op de tijdelijke tabel Hallo **hvac** dat u hebt gemaakt met behulp van Hallo `%%sql` verwerkt Magic-pakket. Voor meer informatie over Hallo `%%sql` magic en andere magics die beschikbaar zijn met de PySpark-kernel hello, Zie [beschikbare Kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

   Hallo na uitvoer in tabelvorm wordt standaard weergegeven.

     ![Tabeluitvoer van resultaat van interactieve Spark-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabeluitvoer van resultaat van interactieve Spark-query")

    U ziet ook Hallo resulteert in een andere visualisaties. Bijvoorbeeld, een gebiedsgrafiek voor dezelfde uitvoer Hallo volgende eruit zou Hallo.

    ![Gebiedsgrafiek van resultaat van interactieve Spark-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Gebiedsgrafiek van resultaat van interactieve Spark-query")

9. Hallo-notebook toorelease Hallo-clusterbronnen afgesloten nadat u klaar bent met het uitvoeren van de toepassing hello. toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**.

## <a name="next-step"></a>Volgende stap

In dit artikel u leert hoe toorun interactieve query's in Spark met Jupyter-notebook. Ga toohello volgende artikel toosee hoe u geregistreerd in Spark Hallo-gegevens kunnen worden opgehaald in een BI-hulpprogramma voor analyse zoals Power BI en Tableau. 

> [!div class="nextstepaction"]
>[Gebruik van de hulpmiddelen voor gegevensvisualisatie met Azure HDInsight Spark-BI](hdinsight-apache-spark-use-bi-tools.md)




