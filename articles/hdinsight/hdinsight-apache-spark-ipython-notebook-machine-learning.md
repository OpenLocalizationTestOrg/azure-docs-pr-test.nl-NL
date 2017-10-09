---
title: aaaBuild Apache Spark machine learning-toepassingen in Azure HDInsight | Microsoft Docs
description: Stapsgewijze instructies over hoe toobuild Apache Spark machine learning-toepassing op HDInsight Spark-clusters met behulp van Jupyter-notebook
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a>Apache Spark machine learning-toepassingen in Azure HDInsight bouwen

Meer informatie over hoe toobuild een Apache Spark machine learning-toepassing met een Spark-cluster in HDInsight. Dit artikel laat zien hoe toouse Jupyter-notebook met Hallo cluster toobuild Hallo en testen van deze toepassing. Hallo-toepassing hello HVAC.csv voorbeeldgegevens die beschikbaar is in alle clusters standaard gebruikt.

**Vereisten:**

U moet Hallo volgende hebben:

* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="data"></a>Hallo-gegevensset begrijpen
Laten we beginnen met het bouwen van de toepassing hello, laat het ons Hallo-structuur van Hallo gegevens waarvoor gaan we verder Hallo-toepassing en soort analyse die wordt gedaan Hallo Hallo gegevens te begrijpen. 

In dit artikel gebruiken we Hallo voorbeeld **HVAC.csv** gegevensbestand dat beschikbaar is in hello Azure Storage-account hebt gekoppeld aan Hallo HDInsight-cluster. Binnen Hallo storage-account, Hallo-bestand bevindt zich in **\HdiSamples\HdiSamples\SensorSampleData\hvac**. Download en open Hallo CSV-bestand tooget een momentopname van Hallo-gegevens.  

![Momentopname van de gegevens die worden gebruikt voor Spark machine learning voorbeeld](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "momentopname van de gegevens die worden gebruikt voor Spark machine learning-voorbeeld")

Hallo gegevens vindt u Hallo doel temperatuur- en Hallo werkelijke temperatuur van een gebouw met HVAC-systemen die zijn geïnstalleerd. Stel Hallo **System** kolom vertegenwoordigt Hallo systeem-ID en Hallo **SystemAge** kolom Hallo aantal jaren Hallo HVAC-systeem is al aanwezig op Hallo gebouw vertegenwoordigt.

We gebruiken deze gegevens toopredict of een gebouw op Hallo doel temperatuur, basis van een systeem-ID en het systeem leeftijd hotter of colder gebaseerde zullen zijn.

## <a name="app"></a>Schrijven van een Spark machine learning-toepassing met behulp van Spark MLlib
In deze toepassing gebruiken we een Spark ML pijplijn tooperform een classificatie van het document. In de pijplijn hello, we Hallo document splitsen in woorden, Hallo woorden converteren naar een numeriek functie vector en ten slotte bouwen van een voorspellingsmodel met Hallo functie vectoren en labels. Volgende stappen toocreate Hallo toepassing hello uitvoeren.

1. Van Hallo [Azure Portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt). U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.   
2. Klik op Hallo blade Spark-cluster **Cluster-Dashboard**, en klik vervolgens op **Jupyter-Notebook**. Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.
   
   > [!NOTE]
   > U mogelijk ook Hallo Jupyter-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken. Vervang **CLUSTERNAME** met Hallo-naam van het cluster:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. Maak een nieuwe notebook. Klik op **Nieuw** en klik vervolgens op **PySpark**.
   
    ![Maken van een Jupyter-notebook bijvoorbeeld Spark machine learning](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "maken van een Jupyter-notebook voor Spark machine learning-voorbeeld")
4. Een nieuwe notebook gemaakt en geopend met de Hallo naam Untitled.pynb. Klik op Hallo notebook naam Hallo boven en een beschrijvende naam.
   
    ![Geef een naam laptop bijvoorbeeld Spark machine learning](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Geef een naam laptop voor Spark machine learning-voorbeeld")
5. Omdat u de notebook met behulp van Hallo PySpark-kernel hebt gemaakt, hoeft u geen toocreate contexten expliciet. Hallo Spark en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel Hallo uitvoert. U kunt starten door het Hallo-typen die vereist voor dit scenario zijn te importeren. Plak Hallo volgende codefragment in een lege cel en druk vervolgens op **SHIFT + ENTER**. 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. U moet nu Hallo-gegevens (hvac.csv) laden, parseren en tootrain Hallo model worden gebruikt. Hiervoor moet u een functie die wordt gecontroleerd of Hallo werkelijke temperatuur van Hallo gebouw groter dan Hallo doel temperatuur is definiëren. Als de werkelijke temperatuur Hallo groter is, Hallo gebouw is hot, aangegeven door Hallo-waarde **1.0**. Als het Hallo werkelijke temperatuur minder, Hallo gebouw is koude, aangegeven door Hallo waarde **0,0**. 
   
    Plakken Hallo volgende codefragment in een lege cel en druk op **SHIFT + ENTER**.

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. Configureer Hallo Spark machine learning-pijplijn die uit drie fasen bestaat: tokenizer hashingTF en lr. Voor meer informatie over wat een pijplijn is en hoe het werkt Zie <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pijplijn</a>.
   
    Plakken Hallo volgende codefragment in een lege cel en druk op **SHIFT + ENTER**.
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. Hallo pijplijn toohello training document aanpassen. Plakken Hallo volgende codefragment in een lege cel en druk op **SHIFT + ENTER**.
   
        model = pipeline.fit(training)
3. Controleer of u Hallo training document toocheckpoint uw voortgang met Hallo-toepassing. Plakken Hallo volgende codefragment in een lege cel en druk op **SHIFT + ENTER**.
   
        training.show()
   
    Dit geeft Hallo vergelijkbare toohello volgende uitvoer:
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    Ga terug en controleer of de uitvoer Hallo tegen Hallo onbewerkte CSV-bestand. Hallo eerste rij Hallo CSV-bestand heeft bijvoorbeeld deze gegevens:

    ![Uitvoergegevens van de momentopname voor Spark machine learning voorbeeld](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "momentopname van de uitvoer-gegevens voor Spark machine learning-voorbeeld")

    U ziet hoe Hallo werkelijke temperatuur is kleiner dan Hallo doel temperatuur voorstellen Hallo gebouw koude is. Daarom in de uitvoer training Hallo Hallo waarde voor **label** in Hallo eerste rij is **0,0**, wat betekent dat Hallo gebouw is geen hot.

1. Bereid een gegevensset toorun Hallo getraind model tegen. toodo dus we op een systeem-ID en het systeem leeftijd zou doorgeven (aangeduid als **SystemInfo** in Hallo training uitvoer), en Hallo model wilt voorspellen of Hallo bouwen met die systeem-ID en het systeem ouder zou worden hotter (aangeduid door 1.0) of koelervoorbeeld () aangegeven door 0,0).
   
   Plakken Hallo volgende codefragment in een lege cel en druk op **SHIFT + ENTER**.
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. Ten slotte de voorspellingen op Hallo testgegevens. Plakken Hallo volgende codefragment in een lege cel en druk op **SHIFT + ENTER**.
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. U ziet een uitvoer vergelijkbare toohello volgende:
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   In eerste rij Hallo in Hallo voorspelling, kunt u zien dat voor een HVAC-systeem met ID 20 en system leeftijd van 25 jaar Hallo gebouw zal hot (**voorspelling = 1.0**). de eerste waarde Hallo voor DenseVector (0.49999) overeenkomt met toohello voorspelling 0,0 en Hallo tweede waarde (0.5001) overeenkomt met toohello voorspelling 1.0. In de uitvoer van Hallo ondanks de tweede waarde Hallo slechts marginaal hoger Hallo model ziet u **voorspelling = 1.0**.
4. Als u klaar bent met het uitvoeren van de toepassing hello moet afsluiten Hallo notebook toorelease Hallo resources. toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**. Deze wordt afgesloten en sluiten Hallo notebook.

## <a name="anaconda"></a>Gebruik scikit Anaconda-bibliotheek voor Spark machine learning meer
Apache Spark-clusters in HDInsight bevatten Anaconda-bibliotheken. Dit omvat ook Hallo **scikit-meer** -bibliotheek voor machine learning. Hallo-bibliotheek bevat ook verschillende gegevenssets die u toobuild voorbeeldtoepassingen rechtstreeks vanuit een Jupyter-notebook kunt gebruiken. Voor voorbeelden van het gebruik scikit Hallo-bibliotheek Lees [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).

## <a name="seealso"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Toepassingen maken en uitvoeren
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [De invoegtoepassing HDInsight Tools voor toocreate IntelliJ IDEA gebruiken en het verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
