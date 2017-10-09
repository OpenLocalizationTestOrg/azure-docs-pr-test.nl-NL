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
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="cdc91-104">Interactieve query's uitvoeren op een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="cdc91-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="cdc91-105">In dit artikel gebruikt u een Jupyter-notebook toorun interactieve Spark SQL-query's op basis van een Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="cdc91-105">In this article, you use a Jupyter notebook toorun interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="cdc91-106">Jupyter-notebook is een browsertoepassing die uitgebreider is dan Hallo interactieve ervaring via de console toohello Web.</span><span class="sxs-lookup"><span data-stu-id="cdc91-106">Jupyter notebook is a browser-based application that extends hello console-based interactive experience toohello Web.</span></span> <span data-ttu-id="cdc91-107">Zie voor meer informatie [hello Jupyter-notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span><span class="sxs-lookup"><span data-stu-id="cdc91-107">For more information, see [hello Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="cdc91-108">Voor deze zelfstudie maakt u Hallo **PySpark** kernel in Hallo Jupyter-notebook toorun een interactieve Spark SQL-query.</span><span class="sxs-lookup"><span data-stu-id="cdc91-108">For this tutorial, you use hello **PySpark** kernel in hello Jupyter notebook toorun an interactive Spark SQL query.</span></span> <span data-ttu-id="cdc91-109">Jupyter-notebooks op HDInsight-clusters bieden ook ondersteuning voor twee andere kernels - **PySpark3** en **Spark**.</span><span class="sxs-lookup"><span data-stu-id="cdc91-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="cdc91-110">Voor meer informatie over Hallo kernels en voordelen van het gebruik van Hallo **PySpark**, Zie [gebruik Jupyter-notebook kernels met Apache Spark-clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="cdc91-110">For more information about hello kernels, and hello benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdc91-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cdc91-111">Prerequisites</span></span>

* <span data-ttu-id="cdc91-112">**Een Azure HDInsight Spark-cluster**.</span><span class="sxs-lookup"><span data-stu-id="cdc91-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="cdc91-113">Zie voor instructies [een Apache Spark-cluster maken in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="cdc91-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a><span data-ttu-id="cdc91-114">Een Jupyter-notebook toorun interactieve query's maken</span><span class="sxs-lookup"><span data-stu-id="cdc91-114">Create a Jupyter notebook toorun interactive queries</span></span>

<span data-ttu-id="cdc91-115">toorun query's, gebruiken we voorbeeldgegevens die standaard beschikbaar in Hallo opslag die is gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cdc91-115">toorun queries, we use sample data that is by default available in hello storage associated with hello cluster.</span></span> <span data-ttu-id="cdc91-116">U moet echter eerst die gegevens laden in Spark als een dataframe.</span><span class="sxs-lookup"><span data-stu-id="cdc91-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="cdc91-117">Zodra u Hallo dataframe hebt, kunt u query's uitvoeren op Hallo Jupyter-notebook met.</span><span class="sxs-lookup"><span data-stu-id="cdc91-117">Once you have hello dataframe, you can run queries on it using hello Jupyter notebook.</span></span> <span data-ttu-id="cdc91-118">In dit gedeelte kijken hoe in:</span><span class="sxs-lookup"><span data-stu-id="cdc91-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="cdc91-119">Een verzameling voorbeeldgegevens registreren als een Spark-dataframe.</span><span class="sxs-lookup"><span data-stu-id="cdc91-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="cdc91-120">Query's uitvoeren op Hallo dataframe.</span><span class="sxs-lookup"><span data-stu-id="cdc91-120">Run queries on hello dataframe.</span></span>

1. <span data-ttu-id="cdc91-121">Open Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cdc91-121">Open hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="cdc91-122">Als u toopin Hallo cluster toohello-dashboard hebt gekozen, klikt u op Hallo cluster tegel Hallo dashboard toolaunch Hallo cluster blade.</span><span class="sxs-lookup"><span data-stu-id="cdc91-122">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="cdc91-123">Als u niet Hallo cluster toohello dashboard in het linkerdeelvenster hello vastmaken, klikt u op **HDInsight-clusters**, en klik vervolgens op Hallo cluster die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cdc91-123">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="cdc91-124">Klik in **Snelkoppelingen** op **Clusterdashboards** en klik vervolgens op **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="cdc91-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="cdc91-125">Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cdc91-125">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="cdc91-126">![Open Jupyter-notebook toorun interactieve Spark SQL-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter-notebook toorun interactieve Spark SQL-query")</span><span class="sxs-lookup"><span data-stu-id="cdc91-126">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="cdc91-127">Hallo Jupyter-notebook zijn ook toegankelijk voor uw cluster door openen Hallo URL te volgen in uw browser.</span><span class="sxs-lookup"><span data-stu-id="cdc91-127">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="cdc91-128">Vervang **CLUSTERNAME** met Hallo-naam van het cluster:</span><span class="sxs-lookup"><span data-stu-id="cdc91-128">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="cdc91-129">Maak een notebook.</span><span class="sxs-lookup"><span data-stu-id="cdc91-129">Create a notebook.</span></span> <span data-ttu-id="cdc91-130">Klik op **Nieuw** en klik vervolgens op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="cdc91-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="cdc91-131">![Maken van een Jupyter-notebook toorun interactieve Spark SQL-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "maken van een Jupyter-notebook toorun interactieve Spark SQL-query")</span><span class="sxs-lookup"><span data-stu-id="cdc91-131">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="cdc91-132">Een nieuwe notebook gemaakt en geopend met de naam van de Hallo Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="cdc91-132">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="cdc91-133">Klik op Hallo notebook naam Hallo boven en een beschrijvende naam invoeren als u wilt.</span><span class="sxs-lookup"><span data-stu-id="cdc91-133">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="cdc91-134">![Geef een naam op voor Hallo Jupter notebook toorun interactieve Spark query van](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "voor Hallo Jupter notebook toorun interactieve Spark query van een naam opgeven")</span><span class="sxs-lookup"><span data-stu-id="cdc91-134">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5. <span data-ttu-id="cdc91-135">Plakken Hallo volgende code in een lege cel en druk vervolgens op **SHIFT + ENTER** toorun Hallo code.</span><span class="sxs-lookup"><span data-stu-id="cdc91-135">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="cdc91-136">Hallo code invoer Hallo-typen die nodig zijn voor dit scenario:</span><span class="sxs-lookup"><span data-stu-id="cdc91-136">hello code imports hello types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="cdc91-137">Omdat u de notebook met behulp van Hallo PySpark-kernel hebt gemaakt, hoeft u geen toocreate contexten expliciet.</span><span class="sxs-lookup"><span data-stu-id="cdc91-137">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="cdc91-138">Hallo Spark en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel Hallo uitvoert.</span><span class="sxs-lookup"><span data-stu-id="cdc91-138">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span>

    <span data-ttu-id="cdc91-139">![Status van interactieve Spark SQL-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status van interactieve Spark SQL-query")</span><span class="sxs-lookup"><span data-stu-id="cdc91-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="cdc91-140">Telkens wanneer u een interactieve query in Jupyter uitvoert, ziet u de venstertitel van uw web-browser een **(bezet)** status samen met de notebooktitel Hallo.</span><span class="sxs-lookup"><span data-stu-id="cdc91-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="cdc91-141">U ziet ook een gevulde cirkel volgende toohello **PySpark** tekst in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="cdc91-141">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="cdc91-142">Nadat het Hallo-taak is voltooid, verandert deze tooa lege cirkel.</span><span class="sxs-lookup"><span data-stu-id="cdc91-142">After hello job is completed, it changes tooa hollow circle.</span></span>

6. <span data-ttu-id="cdc91-143">Voordat u Hallo gegevens laden in een Spark-cluster, kunt u ons een momentopname van het zoeken.</span><span class="sxs-lookup"><span data-stu-id="cdc91-143">Before you load hello data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="cdc91-144">Hallo voorbeeldgegevens gebruikt in deze zelfstudie is beschikbaar als een CSV-bestand op alle HDInsight Spark-clusters op **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="cdc91-144">hello sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="cdc91-145">Hallo-gegevens worden vastgelegd Hallo temperatuur variaties van een gebouw.</span><span class="sxs-lookup"><span data-stu-id="cdc91-145">hello data captures hello temperature variations of a building.</span></span> <span data-ttu-id="cdc91-146">Hier volgen Hallo eerste paar rijen van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="cdc91-146">Here are hello first few rows of hello data.</span></span>

    <span data-ttu-id="cdc91-147">![Momentopname van gegevens voor interactieve Spark SQL-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "momentopname voor interactieve Spark SQL-query")</span><span class="sxs-lookup"><span data-stu-id="cdc91-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="cdc91-148">Maak een dataframe en een tijdelijke tabel (**hvac**) door het uitvoeren van de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="cdc91-148">Create a dataframe and a temporary table (**hvac**) by running hello following code.</span></span> <span data-ttu-id="cdc91-149">Voor deze zelfstudie maken we geen alle Hallo kolommen in de tijdelijke tabel Hallo als vergeleken toohello kolommen in Hallo onbewerkte CSV-gegevens.</span><span class="sxs-lookup"><span data-stu-id="cdc91-149">For this tutorial, we do not create all hello columns in hello temporary table as compared toohello columns in hello raw CSV data.</span></span> 

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

7. <span data-ttu-id="cdc91-150">Zodra Hallo-tabel is gemaakt, interactieve query uitvoeren op Hallo van gegevens, gebruikt u Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="cdc91-150">Once hello table is created, run interactive query on hello data, use hello following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="cdc91-151">Omdat u een PySpark-kernel gebruikt, u kunt nu rechtstreeks een interactieve SQL query uitvoeren op de tijdelijke tabel Hallo **hvac** dat u hebt gemaakt met behulp van Hallo `%%sql` verwerkt Magic-pakket.</span><span class="sxs-lookup"><span data-stu-id="cdc91-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on hello temporary table **hvac** that you created by using hello `%%sql` magic.</span></span> <span data-ttu-id="cdc91-152">Voor meer informatie over Hallo `%%sql` magic en andere magics die beschikbaar zijn met de PySpark-kernel hello, Zie [beschikbare Kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="cdc91-152">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="cdc91-153">Hallo na uitvoer in tabelvorm wordt standaard weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cdc91-153">hello following tabular output is displayed by default.</span></span>

     <span data-ttu-id="cdc91-154">![Tabeluitvoer van resultaat van interactieve Spark-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabeluitvoer van resultaat van interactieve Spark-query")</span><span class="sxs-lookup"><span data-stu-id="cdc91-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="cdc91-155">U ziet ook Hallo resulteert in een andere visualisaties.</span><span class="sxs-lookup"><span data-stu-id="cdc91-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="cdc91-156">Bijvoorbeeld, een gebiedsgrafiek voor dezelfde uitvoer Hallo volgende eruit zou Hallo.</span><span class="sxs-lookup"><span data-stu-id="cdc91-156">For example, an area graph for hello same output would look like hello following.</span></span>

    <span data-ttu-id="cdc91-157">![Gebiedsgrafiek van resultaat van interactieve Spark-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Gebiedsgrafiek van resultaat van interactieve Spark-query")</span><span class="sxs-lookup"><span data-stu-id="cdc91-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="cdc91-158">Hallo-notebook toorelease Hallo-clusterbronnen afgesloten nadat u klaar bent met het uitvoeren van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="cdc91-158">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="cdc91-159">toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**.</span><span class="sxs-lookup"><span data-stu-id="cdc91-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="cdc91-160">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="cdc91-160">Next step</span></span>

<span data-ttu-id="cdc91-161">In dit artikel u leert hoe toorun interactieve query's in Spark met Jupyter-notebook.</span><span class="sxs-lookup"><span data-stu-id="cdc91-161">In this article you learned how toorun interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="cdc91-162">Ga toohello volgende artikel toosee hoe u geregistreerd in Spark Hallo-gegevens kunnen worden opgehaald in een BI-hulpprogramma voor analyse zoals Power BI en Tableau.</span><span class="sxs-lookup"><span data-stu-id="cdc91-162">Advance toohello next article toosee how hello data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="cdc91-163">Gebruik van de hulpmiddelen voor gegevensvisualisatie met Azure HDInsight Spark-BI</span><span class="sxs-lookup"><span data-stu-id="cdc91-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




