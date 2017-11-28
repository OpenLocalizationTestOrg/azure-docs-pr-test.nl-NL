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
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="85327-104">Interactieve query's uitvoeren op een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="85327-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="85327-105">In dit artikel kunt u een Jupyter-notebook interactieve Spark SQL-query's uitvoeren op een Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="85327-105">In this article, you use a Jupyter notebook to run interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="85327-106">Jupyter-notebook is een browsertoepassing die uitgebreider is dan de interactieve ervaring via de console op het Web.</span><span class="sxs-lookup"><span data-stu-id="85327-106">Jupyter notebook is a browser-based application that extends the console-based interactive experience to the Web.</span></span> <span data-ttu-id="85327-107">Zie voor meer informatie [de Jupyter-notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span><span class="sxs-lookup"><span data-stu-id="85327-107">For more information, see [The Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="85327-108">Voor deze zelfstudie maakt u de **PySpark** kernel in de Jupyter-notebook een interactieve Spark SQL-query uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="85327-108">For this tutorial, you use the **PySpark** kernel in the Jupyter notebook to run an interactive Spark SQL query.</span></span> <span data-ttu-id="85327-109">Jupyter-notebooks op HDInsight-clusters bieden ook ondersteuning voor twee andere kernels - **PySpark3** en **Spark**.</span><span class="sxs-lookup"><span data-stu-id="85327-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="85327-110">Voor meer informatie over de kernels en de voordelen van het gebruik van **PySpark**, Zie [gebruik Jupyter-notebook kernels met Apache Spark-clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="85327-110">For more information about the kernels, and the benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85327-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="85327-111">Prerequisites</span></span>

* <span data-ttu-id="85327-112">**Een Azure HDInsight Spark-cluster**.</span><span class="sxs-lookup"><span data-stu-id="85327-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="85327-113">Zie voor instructies [een Apache Spark-cluster maken in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="85327-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-to-run-interactive-queries"></a><span data-ttu-id="85327-114">Maken van een Jupyter-notebook om interactieve query's uitvoeren</span><span class="sxs-lookup"><span data-stu-id="85327-114">Create a Jupyter notebook to run interactive queries</span></span>

<span data-ttu-id="85327-115">Uitvoeren van query's, gebruiken we voorbeeldgegevens die standaard beschikbaar in de opslag die is gekoppeld aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="85327-115">To run queries, we use sample data that is by default available in the storage associated with the cluster.</span></span> <span data-ttu-id="85327-116">U moet echter eerst die gegevens laden in Spark als een dataframe.</span><span class="sxs-lookup"><span data-stu-id="85327-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="85327-117">Zodra u de dataframe hebt, kunt u query's uitvoeren op met behulp van de Jupyter-notebook.</span><span class="sxs-lookup"><span data-stu-id="85327-117">Once you have the dataframe, you can run queries on it using the Jupyter notebook.</span></span> <span data-ttu-id="85327-118">In dit gedeelte kijken hoe in:</span><span class="sxs-lookup"><span data-stu-id="85327-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="85327-119">Een verzameling voorbeeldgegevens registreren als een Spark-dataframe.</span><span class="sxs-lookup"><span data-stu-id="85327-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="85327-120">Query's uitvoeren op de dataframe.</span><span class="sxs-lookup"><span data-stu-id="85327-120">Run queries on the dataframe.</span></span>

1. <span data-ttu-id="85327-121">Open de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="85327-121">Open the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="85327-122">Als u ervoor hebt gekozen om het cluster vast te maken aan het dashboard, klikt u vanuit het dashboard op de clustertegel om de clusterblade te starten.</span><span class="sxs-lookup"><span data-stu-id="85327-122">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="85327-123">Als u het cluster niet hebt vastgemaakt aan het dashboard, klikt u in het linkerdeelvenster op **HDInsight clusters** en vervolgens op het cluster dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="85327-123">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="85327-124">Klik in **Snelkoppelingen** op **Clusterdashboards** en klik vervolgens op **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="85327-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="85327-125">Voer de beheerdersreferenties voor het cluster in als u daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="85327-125">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="85327-126">![Jupyter-notebook openen om de interactieve Spark SQL-query uit te voeren](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Jupyter-notebook openen om de interactieve Spark SQL-query uit te voeren")</span><span class="sxs-lookup"><span data-stu-id="85327-126">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="85327-127">Mogelijk kunt u de Jupyter-notebook voor uw cluster ook openen door de volgende URL in uw browser te openen.</span><span class="sxs-lookup"><span data-stu-id="85327-127">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="85327-128">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="85327-128">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="85327-129">Maak een notebook.</span><span class="sxs-lookup"><span data-stu-id="85327-129">Create a notebook.</span></span> <span data-ttu-id="85327-130">Klik op **Nieuw** en klik vervolgens op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="85327-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="85327-131">![Jupyter-notebook maken om de interactieve Spark SQL-query uit te voeren](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Jupyter-notebook maken om de interactieve Spark SQL-query uit te voeren")</span><span class="sxs-lookup"><span data-stu-id="85327-131">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="85327-132">Er wordt een nieuwe notebook gemaakt en geopend met de naam Untitled (Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="85327-132">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="85327-133">Klik bovenaan op de naam van de notebook en wijzig deze desgewenst in een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="85327-133">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="85327-134">![Een naam opgeven voor de Jupyter-notebook waarop de interactieve Spark-query wordt uitgevoerd](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Een naam opgeven voor de Jupyter-notebook waarop de interactieve Spark-query wordt uitgevoerd")</span><span class="sxs-lookup"><span data-stu-id="85327-134">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5. <span data-ttu-id="85327-135">Plak de volgende code in een lege cel en druk op **Shift+Enter** om de code uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="85327-135">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="85327-136">Met de code importeert u de typen die voor dit scenario zijn vereist:</span><span class="sxs-lookup"><span data-stu-id="85327-136">The code imports the types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="85327-137">Omdat u de notebook met behulp van de PySpark-kernel hebt gemaakt, hoeft u niet expliciet contexten te maken.</span><span class="sxs-lookup"><span data-stu-id="85327-137">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="85327-138">De Spark- en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel uitvoert.</span><span class="sxs-lookup"><span data-stu-id="85327-138">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span>

    <span data-ttu-id="85327-139">![Status van interactieve Spark SQL-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status van interactieve Spark SQL-query")</span><span class="sxs-lookup"><span data-stu-id="85327-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="85327-140">Telkens wanneer u een interactieve query in Jupyter uitvoert, toont de venstertitel van uw webbrowser de status **(Bezet)** samen met de notebooktitel.</span><span class="sxs-lookup"><span data-stu-id="85327-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="85327-141">Ook ziet u een gevulde cirkel naast de **PySpark**-tekst in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="85327-141">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="85327-142">Wanneer de taak is voltooid, verandert deze in een lege cirkel.</span><span class="sxs-lookup"><span data-stu-id="85327-142">After the job is completed, it changes to a hollow circle.</span></span>

6. <span data-ttu-id="85327-143">Voordat u de gegevens laadt in een Spark-cluster, kunt u ons een momentopname van het zoeken.</span><span class="sxs-lookup"><span data-stu-id="85327-143">Before you load the data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="85327-144">De voorbeeldgegevens gebruikt in deze zelfstudie is beschikbaar als een CSV-bestand op alle HDInsight Spark-clusters op **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="85327-144">The sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="85327-145">De gegevens worden vastgelegd variaties van de temperatuur van een gebouw.</span><span class="sxs-lookup"><span data-stu-id="85327-145">The data captures the temperature variations of a building.</span></span> <span data-ttu-id="85327-146">Hier vindt u de eerste paar rijen van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="85327-146">Here are the first few rows of the data.</span></span>

    <span data-ttu-id="85327-147">![Momentopname van gegevens voor interactieve Spark SQL-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "momentopname voor interactieve Spark SQL-query")</span><span class="sxs-lookup"><span data-stu-id="85327-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="85327-148">Maak een dataframe en een tijdelijke tabel (**hvac**) door het uitvoeren van de volgende code.</span><span class="sxs-lookup"><span data-stu-id="85327-148">Create a dataframe and a temporary table (**hvac**) by running the following code.</span></span> <span data-ttu-id="85327-149">Voor deze zelfstudie Maak we niet alle kolommen in de tijdelijke tabel in vergelijking met de kolommen in de onbewerkte gegevens van de CSV.</span><span class="sxs-lookup"><span data-stu-id="85327-149">For this tutorial, we do not create all the columns in the temporary table as compared to the columns in the raw CSV data.</span></span> 

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

7. <span data-ttu-id="85327-150">Zodra de tabel is gemaakt, interactieve query uitvoeren op de gegevens, moet u de volgende code gebruiken.</span><span class="sxs-lookup"><span data-stu-id="85327-150">Once the table is created, run interactive query on the data, use the following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="85327-151">Omdat u een PySpark-kernel gebruikt, kunt u nu rechtstreeks een interactieve SQL-query uitvoeren op de tijdelijke tabel **hvac**, die u hebt gemaakt met behulp van de `%%sql`-magic.</span><span class="sxs-lookup"><span data-stu-id="85327-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on the temporary table **hvac** that you created by using the `%%sql` magic.</span></span> <span data-ttu-id="85327-152">Voor meer informatie over de `%%sql`-magic, en andere magics die voor de PySpark-kernel beschikbaar zijn, raadpleegt u [Beschikbare kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="85327-152">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="85327-153">Standaard wordt de volgende tabelvormige uitvoer weergegeven.</span><span class="sxs-lookup"><span data-stu-id="85327-153">The following tabular output is displayed by default.</span></span>

     <span data-ttu-id="85327-154">![Tabeluitvoer van resultaat van interactieve Spark-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabeluitvoer van resultaat van interactieve Spark-query")</span><span class="sxs-lookup"><span data-stu-id="85327-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="85327-155">U kunt de resultaten ook in andere visualisaties bekijken.</span><span class="sxs-lookup"><span data-stu-id="85327-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="85327-156">Zo ziet een gebiedsgrafiek voor dezelfde uitvoer er als volgt uit.</span><span class="sxs-lookup"><span data-stu-id="85327-156">For example, an area graph for the same output would look like the following.</span></span>

    <span data-ttu-id="85327-157">![Gebiedsgrafiek van resultaat van interactieve Spark-query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Gebiedsgrafiek van resultaat van interactieve Spark-query")</span><span class="sxs-lookup"><span data-stu-id="85327-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="85327-158">Sluit de notebook af om de clusterresources vrij te geven nadat u de toepassing hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="85327-158">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="85327-159">Dit doet u door in het menu **Bestand** in de notebook te klikken op **Sluiten en stoppen**.</span><span class="sxs-lookup"><span data-stu-id="85327-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="85327-160">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="85327-160">Next step</span></span>

<span data-ttu-id="85327-161">In dit artikel hebt u geleerd hoe u interactieve query's uitvoeren in Spark met Jupyter-notebook.</span><span class="sxs-lookup"><span data-stu-id="85327-161">In this article you learned how to run interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="85327-162">Ga naar het volgende artikel om te zien hoe de gegevens die u in Spark geregistreerd in een BI-hulpprogramma voor analyse zoals Power BI en Tableau kan worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="85327-162">Advance to the next article to see how the data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="85327-163">Gebruik van de hulpmiddelen voor gegevensvisualisatie met Azure HDInsight Spark-BI</span><span class="sxs-lookup"><span data-stu-id="85327-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




