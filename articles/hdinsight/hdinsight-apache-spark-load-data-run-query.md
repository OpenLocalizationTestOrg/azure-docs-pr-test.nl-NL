---
title: Interactieve query's uitvoeren op een Azure HDInsight Spark-cluster | Microsoft Docs
description: HDInsight Spark-snelstartgids over het maken van een Apache Spark-cluster in HDInsight.
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
ms.openlocfilehash: ada1c3d1482c68834dbbf5eabbd045a7e0c01f9f
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a>Interactieve query's uitvoeren op een HDInsight Spark-cluster

In dit artikel kunt u een Jupyter-notebook interactieve Spark SQL-query's uitvoeren op een Spark-cluster. Jupyter-notebook is een browsertoepassing die uitgebreider is dan de interactieve ervaring via de console op het Web. Zie voor meer informatie [de Jupyter-notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).

Voor deze zelfstudie maakt u de **PySpark** kernel in de Jupyter-notebook een interactieve Spark SQL-query uit te voeren. Jupyter-notebooks op HDInsight-clusters bieden ook ondersteuning voor twee andere kernels - **PySpark3** en **Spark**. Voor meer informatie over de kernels en de voordelen van het gebruik van **PySpark**, Zie [gebruik Jupyter-notebook kernels met Apache Spark-clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Vereisten

* **Een Azure HDInsight Spark-cluster**. Zie voor instructies [een Apache Spark-cluster maken in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-to-run-interactive-queries"></a>Maken van een Jupyter-notebook om interactieve query's uitvoeren

Uitvoeren van query's, gebruiken we voorbeeldgegevens die standaard beschikbaar in de opslag die is gekoppeld aan het cluster. U moet echter eerst die gegevens laden in Spark als een dataframe. Zodra u de dataframe hebt, kunt u query's uitvoeren op met behulp van de Jupyter-notebook. In dit gedeelte kijken hoe in:

* Een verzameling voorbeeldgegevens registreren als een Spark-dataframe.
* Query's uitvoeren op de dataframe.

1. Open de [Azure Portal](https://portal.azure.com/). Als u ervoor hebt gekozen om het cluster vast te maken aan het dashboard, klikt u vanuit het dashboard op de clustertegel om de clusterblade te starten.

    Als u het cluster niet hebt vastgemaakt aan het dashboard, klikt u in het linkerdeelvenster op **HDInsight clusters** en vervolgens op het cluster dat u hebt gemaakt.

3. Klik in **Snelkoppelingen** op **Clusterdashboards** en klik vervolgens op **Jupyter Notebook**. Voer de beheerdersreferenties voor het cluster in als u daarom wordt gevraagd.

   ![Jupyter-notebook openen om de interactieve Spark SQL-query uit te voeren](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Jupyter-notebook openen om de interactieve Spark SQL-query uit te voeren")

   > [!NOTE]
   > Mogelijk kunt u de Jupyter-notebook voor uw cluster ook openen door de volgende URL in uw browser te openen. Vervang **CLUSTERNAME** door de naam van uw cluster.
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Maak een notebook. Klik op **Nieuw** en klik vervolgens op **PySpark**.

   ![Jupyter-notebook maken om de interactieve Spark SQL-query uit te voeren](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Jupyter-notebook maken om de interactieve Spark SQL-query uit te voeren")

   Er wordt een nieuwe notebook gemaakt en geopend met de naam Untitled (Untitled.pynb).

4. Klik bovenaan op de naam van de notebook en wijzig deze desgewenst in een beschrijvende naam.

    ![Een naam opgeven voor de Jupyter-notebook waarop de interactieve Spark-query wordt uitgevoerd](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Een naam opgeven voor de Jupyter-notebook waarop de interactieve Spark-query wordt uitgevoerd")

5. Plak de volgende code in een lege cel en druk op **Shift+Enter** om de code uit te voeren. Met de code importeert u de typen die voor dit scenario zijn vereist:

        from pyspark.sql.types import *

    Omdat u de notebook met behulp van de PySpark-kernel hebt gemaakt, hoeft u niet expliciet contexten te maken. De Spark- en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel uitvoert.

    ![Status van interactieve Spark SQL-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status van interactieve Spark SQL-query")

    Telkens wanneer u een interactieve query in Jupyter uitvoert, toont de venstertitel van uw webbrowser de status **(Bezet)** samen met de notebooktitel. Ook ziet u een gevulde cirkel naast de **PySpark**-tekst in de rechterbovenhoek. Wanneer de taak is voltooid, verandert deze in een lege cirkel.

6. Voordat u de gegevens laadt in een Spark-cluster, kunt u ons een momentopname van het zoeken. De voorbeeldgegevens gebruikt in deze zelfstudie is beschikbaar als een CSV-bestand op alle HDInsight Spark-clusters op **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**. De gegevens worden vastgelegd variaties van de temperatuur van een gebouw. Hier vindt u de eerste paar rijen van de gegevens.

    ![Momentopname van gegevens voor interactieve Spark SQL-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "momentopname voor interactieve Spark SQL-query")

6. Maak een dataframe en een tijdelijke tabel (**hvac**) door het uitvoeren van de volgende code. Voor deze zelfstudie Maak we niet alle kolommen in de tijdelijke tabel in vergelijking met de kolommen in de onbewerkte gegevens van de CSV. 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse the data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer the schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Zodra de tabel is gemaakt, interactieve query uitvoeren op de gegevens, moet u de volgende code gebruiken.

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   Omdat u een PySpark-kernel gebruikt, kunt u nu rechtstreeks een interactieve SQL-query uitvoeren op de tijdelijke tabel **hvac**, die u hebt gemaakt met behulp van de `%%sql`-magic. Voor meer informatie over de `%%sql`-magic, en andere magics die voor de PySpark-kernel beschikbaar zijn, raadpleegt u [Beschikbare kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

   Standaard wordt de volgende tabelvormige uitvoer weergegeven.

     ![Tabeluitvoer van resultaat van interactieve Spark-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabeluitvoer van resultaat van interactieve Spark-query")

    U kunt de resultaten ook in andere visualisaties bekijken. Zo ziet een gebiedsgrafiek voor dezelfde uitvoer er als volgt uit.

    ![Gebiedsgrafiek van resultaat van interactieve Spark-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Gebiedsgrafiek van resultaat van interactieve Spark-query")

9. Sluit de notebook af om de clusterresources vrij te geven nadat u de toepassing hebt uitgevoerd. Dit doet u door in het menu **Bestand** in de notebook te klikken op **Sluiten en stoppen**.

## <a name="next-step"></a>Volgende stap

In dit artikel hebt u geleerd hoe u interactieve query's uitvoeren in Spark met Jupyter-notebook. Ga naar het volgende artikel om te zien hoe de gegevens die u in Spark geregistreerd in een BI-hulpprogramma voor analyse zoals Power BI en Tableau kan worden opgevraagd. 

> [!div class="nextstepaction"]
>[Gebruik van de hulpmiddelen voor gegevensvisualisatie met Azure HDInsight Spark-BI](hdinsight-apache-spark-use-bi-tools.md)




