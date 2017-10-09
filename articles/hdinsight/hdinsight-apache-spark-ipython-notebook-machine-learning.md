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
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="a1ef5-103">Apache Spark machine learning-toepassingen in Azure HDInsight bouwen</span><span class="sxs-lookup"><span data-stu-id="a1ef5-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="a1ef5-104">Meer informatie over hoe toobuild een Apache Spark machine learning-toepassing met een Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-104">Learn how toobuild an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="a1ef5-105">Dit artikel laat zien hoe toouse Jupyter-notebook met Hallo cluster toobuild Hallo en testen van deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-105">This article shows how toouse hello Jupyter notebook available with hello cluster toobuild and test this application.</span></span> <span data-ttu-id="a1ef5-106">Hallo-toepassing hello HVAC.csv voorbeeldgegevens die beschikbaar is in alle clusters standaard gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-106">hello application uses hello sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="a1ef5-107">**Vereisten:**</span><span class="sxs-lookup"><span data-stu-id="a1ef5-107">**Prerequisites:**</span></span>

<span data-ttu-id="a1ef5-108">U moet Hallo volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="a1ef5-108">You must have hello following:</span></span>

* <span data-ttu-id="a1ef5-109">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="a1ef5-110">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="a1ef5-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="a1ef5-111"><a name="data"></a>Hallo-gegevensset begrijpen</span><span class="sxs-lookup"><span data-stu-id="a1ef5-111"><a name="data"></a>Understand hello data set</span></span>
<span data-ttu-id="a1ef5-112">Laten we beginnen met het bouwen van de toepassing hello, laat het ons Hallo-structuur van Hallo gegevens waarvoor gaan we verder Hallo-toepassing en soort analyse die wordt gedaan Hallo Hallo gegevens te begrijpen.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-112">Before we start building hello application, let us understand hello structure of hello data for which we build hello application and hello kind of analysis we will do on hello data.</span></span> 

<span data-ttu-id="a1ef5-113">In dit artikel gebruiken we Hallo voorbeeld **HVAC.csv** gegevensbestand dat beschikbaar is in hello Azure Storage-account hebt gekoppeld aan Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-113">In this article, we use hello sample **HVAC.csv** data file that is available in hello Azure Storage account that you associated with hello HDInsight cluster.</span></span> <span data-ttu-id="a1ef5-114">Binnen Hallo storage-account, Hallo-bestand bevindt zich in **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-114">Within hello storage account, hello file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="a1ef5-115">Download en open Hallo CSV-bestand tooget een momentopname van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-115">Download and open hello CSV file tooget a snapshot of hello data.</span></span>  

<span data-ttu-id="a1ef5-116">![Momentopname van de gegevens die worden gebruikt voor Spark machine learning voorbeeld](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "momentopname van de gegevens die worden gebruikt voor Spark machine learning-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="a1ef5-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="a1ef5-117">Hallo gegevens vindt u Hallo doel temperatuur- en Hallo werkelijke temperatuur van een gebouw met HVAC-systemen die zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-117">hello data shows hello target temperature and hello actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="a1ef5-118">Stel Hallo **System** kolom vertegenwoordigt Hallo systeem-ID en Hallo **SystemAge** kolom Hallo aantal jaren Hallo HVAC-systeem is al aanwezig op Hallo gebouw vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-118">Let's assume hello **System** column represents hello system ID and hello **SystemAge** column represents hello number of years hello HVAC system has been in place at hello building.</span></span>

<span data-ttu-id="a1ef5-119">We gebruiken deze gegevens toopredict of een gebouw op Hallo doel temperatuur, basis van een systeem-ID en het systeem leeftijd hotter of colder gebaseerde zullen zijn.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-119">We use this data toopredict whether a building will be hotter or colder based on hello target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="a1ef5-120"><a name="app"></a>Schrijven van een Spark machine learning-toepassing met behulp van Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="a1ef5-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="a1ef5-121">In deze toepassing gebruiken we een Spark ML pijplijn tooperform een classificatie van het document.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-121">In this application we use a Spark ML pipeline tooperform a document classification.</span></span> <span data-ttu-id="a1ef5-122">In de pijplijn hello, we Hallo document splitsen in woorden, Hallo woorden converteren naar een numeriek functie vector en ten slotte bouwen van een voorspellingsmodel met Hallo functie vectoren en labels.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-122">In hello pipeline, we split hello document into words, convert hello words into a numerical feature vector, and finally build a prediction model using hello feature vectors and labels.</span></span> <span data-ttu-id="a1ef5-123">Volgende stappen toocreate Hallo toepassing hello uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-123">Perform hello following steps toocreate hello application.</span></span>

1. <span data-ttu-id="a1ef5-124">Van Hallo [Azure Portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt).</span><span class="sxs-lookup"><span data-stu-id="a1ef5-124">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="a1ef5-125">U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-125">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="a1ef5-126">Klik op Hallo blade Spark-cluster **Cluster-Dashboard**, en klik vervolgens op **Jupyter-Notebook**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-126">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="a1ef5-127">Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-127">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a1ef5-128">U mogelijk ook Hallo Jupyter-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-128">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="a1ef5-129">Vervang **CLUSTERNAME** met Hallo-naam van het cluster:</span><span class="sxs-lookup"><span data-stu-id="a1ef5-129">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="a1ef5-130">Maak een nieuwe notebook.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-130">Create a new notebook.</span></span> <span data-ttu-id="a1ef5-131">Klik op **Nieuw** en klik vervolgens op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="a1ef5-132">![Maken van een Jupyter-notebook bijvoorbeeld Spark machine learning](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "maken van een Jupyter-notebook voor Spark machine learning-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="a1ef5-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="a1ef5-133">Een nieuwe notebook gemaakt en geopend met de Hallo naam Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-133">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="a1ef5-134">Klik op Hallo notebook naam Hallo boven en een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-134">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="a1ef5-135">![Geef een naam laptop bijvoorbeeld Spark machine learning](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Geef een naam laptop voor Spark machine learning-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="a1ef5-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="a1ef5-136">Omdat u de notebook met behulp van Hallo PySpark-kernel hebt gemaakt, hoeft u geen toocreate contexten expliciet.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="a1ef5-137">Hallo Spark en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel Hallo uitvoert.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="a1ef5-138">U kunt starten door het Hallo-typen die vereist voor dit scenario zijn te importeren.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-138">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="a1ef5-139">Plak Hallo volgende codefragment in een lege cel en druk vervolgens op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-139">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
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
6. <span data-ttu-id="a1ef5-140">U moet nu Hallo-gegevens (hvac.csv) laden, parseren en tootrain Hallo model worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-140">You must now load hello data (hvac.csv), parse it, and use it tootrain hello model.</span></span> <span data-ttu-id="a1ef5-141">Hiervoor moet u een functie die wordt gecontroleerd of Hallo werkelijke temperatuur van Hallo gebouw groter dan Hallo doel temperatuur is definiëren.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-141">For this, you define a function that checks whether hello actual temperature of hello building is greater than hello target temperature.</span></span> <span data-ttu-id="a1ef5-142">Als de werkelijke temperatuur Hallo groter is, Hallo gebouw is hot, aangegeven door Hallo-waarde **1.0**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-142">If hello actual temperature is greater, hello building is hot, denoted by hello value **1.0**.</span></span> <span data-ttu-id="a1ef5-143">Als het Hallo werkelijke temperatuur minder, Hallo gebouw is koude, aangegeven door Hallo waarde **0,0**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-143">If hello actual temperature is lesser, hello building is cold, denoted by hello value **0.0**.</span></span> 
   
    <span data-ttu-id="a1ef5-144">Plakken Hallo volgende codefragment in een lege cel en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-144">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

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


1. <span data-ttu-id="a1ef5-145">Configureer Hallo Spark machine learning-pijplijn die uit drie fasen bestaat: tokenizer hashingTF en lr.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-145">Configure hello Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="a1ef5-146">Voor meer informatie over wat een pijplijn is en hoe het werkt Zie <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pijplijn</a>.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="a1ef5-147">Plakken Hallo volgende codefragment in een lege cel en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-147">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="a1ef5-148">Hallo pijplijn toohello training document aanpassen.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-148">Fit hello pipeline toohello training document.</span></span> <span data-ttu-id="a1ef5-149">Plakken Hallo volgende codefragment in een lege cel en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-149">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="a1ef5-150">Controleer of u Hallo training document toocheckpoint uw voortgang met Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-150">Verify hello training document toocheckpoint your progress with hello application.</span></span> <span data-ttu-id="a1ef5-151">Plakken Hallo volgende codefragment in een lege cel en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-151">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="a1ef5-152">Dit geeft Hallo vergelijkbare toohello volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a1ef5-152">This should give hello output similar toohello following:</span></span>
   
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

    <span data-ttu-id="a1ef5-153">Ga terug en controleer of de uitvoer Hallo tegen Hallo onbewerkte CSV-bestand.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-153">Go back and verify hello output against hello raw CSV file.</span></span> <span data-ttu-id="a1ef5-154">Hallo eerste rij Hallo CSV-bestand heeft bijvoorbeeld deze gegevens:</span><span class="sxs-lookup"><span data-stu-id="a1ef5-154">For example, hello first row hello CSV file has this data:</span></span>

    <span data-ttu-id="a1ef5-155">![Uitvoergegevens van de momentopname voor Spark machine learning voorbeeld](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "momentopname van de uitvoer-gegevens voor Spark machine learning-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="a1ef5-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="a1ef5-156">U ziet hoe Hallo werkelijke temperatuur is kleiner dan Hallo doel temperatuur voorstellen Hallo gebouw koude is.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-156">Notice how hello actual temperature is less than hello target temperature suggesting hello building is cold.</span></span> <span data-ttu-id="a1ef5-157">Daarom in de uitvoer training Hallo Hallo waarde voor **label** in Hallo eerste rij is **0,0**, wat betekent dat Hallo gebouw is geen hot.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-157">Hence in hello training output, hello value for **label** in hello first row is **0.0**, which means hello building is not hot.</span></span>

1. <span data-ttu-id="a1ef5-158">Bereid een gegevensset toorun Hallo getraind model tegen.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-158">Prepare a data set toorun hello trained model against.</span></span> <span data-ttu-id="a1ef5-159">toodo dus we op een systeem-ID en het systeem leeftijd zou doorgeven (aangeduid als **SystemInfo** in Hallo training uitvoer), en Hallo model wilt voorspellen of Hallo bouwen met die systeem-ID en het systeem ouder zou worden hotter (aangeduid door 1.0) of koelervoorbeeld () aangegeven door 0,0).</span><span class="sxs-lookup"><span data-stu-id="a1ef5-159">toodo so, we would pass on a system ID and system age (denoted as **SystemInfo** in hello training output), and hello model would predict whether hello building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="a1ef5-160">Plakken Hallo volgende codefragment in een lege cel en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-160">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="a1ef5-161">Ten slotte de voorspellingen op Hallo testgegevens.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-161">Finally, make predictions on hello test data.</span></span> <span data-ttu-id="a1ef5-162">Plakken Hallo volgende codefragment in een lege cel en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-162">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="a1ef5-163">U ziet een uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="a1ef5-163">You should see an output similar toohello following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="a1ef5-164">In eerste rij Hallo in Hallo voorspelling, kunt u zien dat voor een HVAC-systeem met ID 20 en system leeftijd van 25 jaar Hallo gebouw zal hot (**voorspelling = 1.0**).</span><span class="sxs-lookup"><span data-stu-id="a1ef5-164">From hello first row in hello prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, hello building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="a1ef5-165">de eerste waarde Hallo voor DenseVector (0.49999) overeenkomt met toohello voorspelling 0,0 en Hallo tweede waarde (0.5001) overeenkomt met toohello voorspelling 1.0.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-165">hello first value for DenseVector (0.49999) corresponds toohello  prediction 0.0 and hello second value (0.5001) corresponds toohello prediction 1.0.</span></span> <span data-ttu-id="a1ef5-166">In de uitvoer van Hallo ondanks de tweede waarde Hallo slechts marginaal hoger Hallo model ziet u **voorspelling = 1.0**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-166">In hello output, even though hello second value is only marginally higher, hello model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="a1ef5-167">Als u klaar bent met het uitvoeren van de toepassing hello moet afsluiten Hallo notebook toorelease Hallo resources.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-167">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="a1ef5-168">toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-168">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="a1ef5-169">Deze wordt afgesloten en sluiten Hallo notebook.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-169">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="a1ef5-170"><a name="anaconda"></a>Gebruik scikit Anaconda-bibliotheek voor Spark machine learning meer</span><span class="sxs-lookup"><span data-stu-id="a1ef5-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="a1ef5-171">Apache Spark-clusters in HDInsight bevatten Anaconda-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="a1ef5-172">Dit omvat ook Hallo **scikit-meer** -bibliotheek voor machine learning.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-172">This also includes hello **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="a1ef5-173">Hallo-bibliotheek bevat ook verschillende gegevenssets die u toobuild voorbeeldtoepassingen rechtstreeks vanuit een Jupyter-notebook kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a1ef5-173">hello library also includes various data sets that you can use toobuild sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="a1ef5-174">Voor voorbeelden van het gebruik scikit Hallo-bibliotheek Lees [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="a1ef5-174">For examples on using hello scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="a1ef5-175"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="a1ef5-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="a1ef5-176">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1ef5-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="a1ef5-177">Scenario's</span><span class="sxs-lookup"><span data-stu-id="a1ef5-177">Scenarios</span></span>
* [<span data-ttu-id="a1ef5-178">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="a1ef5-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="a1ef5-179">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="a1ef5-179">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="a1ef5-180">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="a1ef5-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="a1ef5-181">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1ef5-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="a1ef5-182">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a1ef5-182">Create and run applications</span></span>
* [<span data-ttu-id="a1ef5-183">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="a1ef5-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="a1ef5-184">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="a1ef5-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="a1ef5-185">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="a1ef5-185">Tools and extensions</span></span>
* [<span data-ttu-id="a1ef5-186">De invoegtoepassing HDInsight Tools voor toocreate IntelliJ IDEA gebruiken en het verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="a1ef5-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="a1ef5-187">De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="a1ef5-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="a1ef5-188">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1ef5-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="a1ef5-189">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1ef5-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="a1ef5-190">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="a1ef5-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="a1ef5-191">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="a1ef5-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="a1ef5-192">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="a1ef5-192">Manage resources</span></span>
* [<span data-ttu-id="a1ef5-193">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1ef5-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="a1ef5-194">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="a1ef5-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
