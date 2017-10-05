---
title: Met behulp van de hulpmiddelen voor gegevensvisualisatie in Azure HDInsight Spark-BI | Microsoft Docs
description: Hulpmiddelen voor gegevensvisualisatie voor analyses met Apache Spark BI op HDInsight-clusters gebruiken
keywords: Apache spark bi, spark bi, spark gegevensvisualisatie, spark business intelligence
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 49dd161049ac442081fe6d26cf8bd3a56a2e0687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a><span data-ttu-id="935cc-104">Apache Spark BI hulpmiddelen voor gegevensvisualisatie gebruiken met Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="935cc-104">Apache Spark BI using data visualization tools with Azure HDInsight</span></span>

<span data-ttu-id="935cc-105">Informatie over het hulpmiddelen voor gegevensvisualisatie zoals Power BI en Tableau gebruiken voor het analyseren van een onbewerkte voorbeeldgegevensset met BI van Apache Spark in HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="935cc-105">Learn how to use data visualization tools such as Power BI and Tableau to analyze a raw sample data set using Apache Spark BI on HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="935cc-106">Connectiviteit met BI-tools die worden beschreven in dit artikel wordt niet ondersteund op 2.1 Spark op Azure HDInsight 3.6 Preview.</span><span class="sxs-lookup"><span data-stu-id="935cc-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="935cc-107">Alleen Spark versie 1.6 en 2.0 (HDInsight 3.4 3.5 respectievelijk) worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="935cc-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="935cc-108">Deze zelfstudie is ook beschikbaar als een Jupyter-notebook in een HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="935cc-108">This tutorial is also available as a Jupyter notebook on an HDInsight Spark cluster.</span></span> <span data-ttu-id="935cc-109">De ervaring voor de notebook kunt u de Python-codefragmenten uitvoeren vanaf de notebook zelf.</span><span class="sxs-lookup"><span data-stu-id="935cc-109">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="935cc-110">Als u de zelfstudie uit binnen een laptop, een Spark-cluster maken, een Jupyter-notebook starten (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), en voer vervolgens de notebook **gebruik BI-tools met Apache Spark in HDInsight.ipynb** onder de **Python** map.</span><span class="sxs-lookup"><span data-stu-id="935cc-110">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under the **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="935cc-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="935cc-111">Prerequisites</span></span>

* <span data-ttu-id="935cc-112">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="935cc-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="935cc-113">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="935cc-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <span data-ttu-id="935cc-114"><a name="hivetable"></a>Gegevens voorbereiden voor Spark gegevensvisualisatie</span><span class="sxs-lookup"><span data-stu-id="935cc-114"><a name="hivetable"></a>Prepare data for Spark data visualization</span></span>

<span data-ttu-id="935cc-115">In deze sectie gebruiken we de [Jupyter](https://jupyter.org) laptop van een HDInsight Spark-cluster aan taken uitvoeren die uw onbewerkte voorbeeldgegevens en deze opslaan in een tabel.</span><span class="sxs-lookup"><span data-stu-id="935cc-115">In this section, we use the [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster to run jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="935cc-116">De voorbeeldgegevens is een CSV-bestand (hvac.csv) beschikbaar in alle clusters standaard.</span><span class="sxs-lookup"><span data-stu-id="935cc-116">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span> <span data-ttu-id="935cc-117">Wanneer uw gegevens wordt opgeslagen als een tabel, in de volgende sectie gebruiken we BI-tools verbinding maken met de tabel en gegevensvisualisaties uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="935cc-117">Once your data is saved as a table, in the next section we use BI tools to connect to the table and perform data visualizations.</span></span>

> [!NOTE]
> <span data-ttu-id="935cc-118">Als u de stappen in dit artikel uitvoeren wilt na het voltooien van de instructies in [interactieve query's uitvoeren op een HDInsight Spark-cluster](hdinsight-apache-spark-load-data-run-query.md), kunt u doorgaan naar stap 8 hieronder.</span><span class="sxs-lookup"><span data-stu-id="935cc-118">If you are performing the steps in this article after completing the instructions in [Run interactive queries on an HDInsight Spark cluster](hdinsight-apache-spark-load-data-run-query.md), you can skip to Step 8 below.</span></span>
>

1. <span data-ttu-id="935cc-119">Klik vanaf het Startboard in [Azure Portal](https://portal.azure.com/) op de tegel voor uw Spark-cluster (als u deze aan het Startboard hebt vastgemaakt).</span><span class="sxs-lookup"><span data-stu-id="935cc-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="935cc-120">U kunt ook naar uw cluster navigeren onder **Bladeren** > **HDInsight-clusters**.</span><span class="sxs-lookup"><span data-stu-id="935cc-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="935cc-121">Klik vanuit de blade Spark-cluster op **Cluster-dashboard** en vervolgens op **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="935cc-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="935cc-122">Voer de beheerdersreferenties voor het cluster in als u daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="935cc-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="935cc-123">Mogelijk bereikt u de Jupyter-notebook voor uw cluster ook door de volgende URL in uw browser te openen.</span><span class="sxs-lookup"><span data-stu-id="935cc-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="935cc-124">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="935cc-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="935cc-125">Maak een notebook.</span><span class="sxs-lookup"><span data-stu-id="935cc-125">Create a notebook.</span></span> <span data-ttu-id="935cc-126">Klik op **Nieuw** en klik vervolgens op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="935cc-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="935cc-127">![Een Jupyter-notebook maken voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "een Jupyter-notebook maken voor Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="935cc-127">![Create a Jupyter notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Create a Jupyter notebook for Apache Spark BI")</span></span>

4. <span data-ttu-id="935cc-128">Er wordt een nieuwe notebook gemaakt en geopend met de naam Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="935cc-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="935cc-129">Klik bovenaan op de naam van de notebook en wijzig deze in een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="935cc-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="935cc-130">![Geef een naam voor de notebook voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Geef een naam voor de notebook voor Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="935cc-130">![Provide a name for the notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Provide a name for the notebook for Apache Spark BI")</span></span>

5. <span data-ttu-id="935cc-131">Omdat u de notebook met behulp van de PySpark-kernel hebt gemaakt, hoeft u niet expliciet contexten te maken.</span><span class="sxs-lookup"><span data-stu-id="935cc-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="935cc-132">De Spark- en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel uitvoert.</span><span class="sxs-lookup"><span data-stu-id="935cc-132">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="935cc-133">Als eerste stap importeert u de typen die voor dit scenario zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="935cc-133">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="935cc-134">Om dit te doen, plaatst u de cursor in de cel en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="935cc-134">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="935cc-135">Laad voorbeeldgegevens in een tijdelijke tabel.</span><span class="sxs-lookup"><span data-stu-id="935cc-135">Load sample data into a temporary table.</span></span> <span data-ttu-id="935cc-136">Wanneer u een Spark-cluster in HDInsight maakt, wordt het voorbeeldgegevensbestand, **hvac.csv**, gekopieerd naar het bijbehorende opslagaccount onder **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="935cc-136">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="935cc-137">Plak het volgende codefragment en druk op in een lege cel **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="935cc-137">In an empty cell, paste the following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="935cc-138">In dit fragment registreert de gegevens in een tabel met de naam **hvac**.</span><span class="sxs-lookup"><span data-stu-id="935cc-138">This snippet registers the data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. <span data-ttu-id="935cc-139">Controleer of de tabel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="935cc-139">Verify that the table was successfully created.</span></span> <span data-ttu-id="935cc-140">U kunt de `%%sql` magic uitvoeren van Hive rechtstreeks query's.</span><span class="sxs-lookup"><span data-stu-id="935cc-140">You can use the `%%sql` magic to run Hive queries directly.</span></span> <span data-ttu-id="935cc-141">Voor meer informatie over de `%%sql`-magic, en andere magics die voor de PySpark-kernel beschikbaar zijn, raadpleegt u [Beschikbare kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="935cc-141">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="935cc-142">Ziet u uitvoer zoals hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="935cc-142">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="935cc-143">Alleen de tabellen die zijn false onder de **isTemporary** kolom hive-tabellen die zijn opgeslagen in de metastore en toegankelijk is vanaf de BI-hulpprogramma's zijn.</span><span class="sxs-lookup"><span data-stu-id="935cc-143">Only the tables that have false under the **isTemporary** column are hive tables that are stored in the metastore and can be accessed from the BI tools.</span></span> <span data-ttu-id="935cc-144">In deze zelfstudie we verbinding maken met de **hvac** tabel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="935cc-144">In this tutorial, we connect to the **hvac** table we created.</span></span>

8. <span data-ttu-id="935cc-145">Controleer of de tabel bevat de gewenste gegevens.</span><span class="sxs-lookup"><span data-stu-id="935cc-145">Verify that the table contains the intended data.</span></span> <span data-ttu-id="935cc-146">Kopieer het volgende codefragment en druk op in een lege cel in de notebook **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="935cc-146">In an empty cell in the notebook, copy the following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="935cc-147">Sluit de notebook om resources vrij te geven.</span><span class="sxs-lookup"><span data-stu-id="935cc-147">Shut down the notebook to release the resources.</span></span> <span data-ttu-id="935cc-148">Dit doet u door in het menu **Bestand** in de notebook te klikken op **Sluiten en stoppen**.</span><span class="sxs-lookup"><span data-stu-id="935cc-148">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <span data-ttu-id="935cc-149"><a name="powerbi"></a>Gebruik Power BI voor Spark gegevensvisualisatie</span><span class="sxs-lookup"><span data-stu-id="935cc-149"><a name="powerbi"></a>Use Power BI for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="935cc-150">Deze sectie geldt alleen voor Spark 1.6 op HDInsight 3.4 en Spark 2.0 op HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="935cc-150">This section is applicable only for Spark 1.6 on HDInsight 3.4 and Spark 2.0 on HDInsight 3.5.</span></span>
>
>

<span data-ttu-id="935cc-151">Wanneer u de gegevens hebt opgeslagen als een tabel, kunt u Power BI verbinding maken met de gegevens en visualiseren om te maken van rapporten, dashboards, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="935cc-151">Once you have saved the data as a table, you can use Power BI to connect to the data and visualize it to create reports, dashboards, etc.</span></span>

1. <span data-ttu-id="935cc-152">Zorg ervoor dat u hebt toegang tot Power BI.</span><span class="sxs-lookup"><span data-stu-id="935cc-152">Make sure you have access to Power BI.</span></span> <span data-ttu-id="935cc-153">U krijgt een abonnement gratis preview van Power BI van [http://www.powerbi.com/](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="935cc-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="935cc-154">Aanmelden bij [Power BI](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="935cc-154">Sign in to [Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="935cc-155">Klik onder aan het linkerdeelvenster op **gegevens ophalen**.</span><span class="sxs-lookup"><span data-stu-id="935cc-155">From the bottom of the left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="935cc-156">Op de **gegevens ophalen** pagina onder **importeren of verbinding maken met gegevens**, voor **Databases**, klikt u op **ophalen**.</span><span class="sxs-lookup"><span data-stu-id="935cc-156">On the **Get Data** page, under **Import or Connect to Data**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="935cc-157">![Ophalen van gegevens in Power BI voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "gegevens in Power BI voor Apache Spark BI ophalen")</span><span class="sxs-lookup"><span data-stu-id="935cc-157">![Get data into Power BI for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI for Apache Spark BI")</span></span>

5. <span data-ttu-id="935cc-158">Klik op het volgende scherm **Spark op Azure HDInsight** en klik vervolgens op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="935cc-158">On the next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="935cc-159">Wanneer u wordt gevraagd, typt u de cluster-URL (`mysparkcluster.azurehdinsight.net`) en de referenties voor verbinding met het cluster.</span><span class="sxs-lookup"><span data-stu-id="935cc-159">When prompted, enter the cluster URL (`mysparkcluster.azurehdinsight.net`) and the credentials to connect to the cluster.</span></span>

    <span data-ttu-id="935cc-160">![Verbinding maken met Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "verbinding maken met Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="935cc-160">![Connect to Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connect to Apache Spark BI")</span></span>

    <span data-ttu-id="935cc-161">Nadat de verbinding is gemaakt, begint Power BI importeren van gegevens uit het Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="935cc-161">After the connection is established, Power BI starts importing data from the Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="935cc-162">Power BI kunt u de gegevens importeren en voegt een **Spark** gegevensset onder de **gegevenssets** kop.</span><span class="sxs-lookup"><span data-stu-id="935cc-162">Power BI imports the data and adds a **Spark** dataset under the **Datasets** heading.</span></span> <span data-ttu-id="935cc-163">Klik op de gegevensset te openen van een nieuw werkblad om de gegevens.</span><span class="sxs-lookup"><span data-stu-id="935cc-163">Click the data set to open a new worksheet to visualize the data.</span></span> <span data-ttu-id="935cc-164">U kunt ook het werkblad opslaan als een rapport.</span><span class="sxs-lookup"><span data-stu-id="935cc-164">You can also save the worksheet as a report.</span></span> <span data-ttu-id="935cc-165">Opslaan van een werkblad van de **bestand** menu, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="935cc-165">To save a worksheet, from the **File** menu, click **Save**.</span></span>

    <span data-ttu-id="935cc-166">![Apache Spark BI-tegel in Power BI-dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI-tegel in Power BI-dashboard")</span><span class="sxs-lookup"><span data-stu-id="935cc-166">![Apache Spark BI tile on Power BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="935cc-167">U ziet dat de **velden** lijst op de juiste lijsten met de **hvac** tabel die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="935cc-167">Notice that the **Fields** list on the right lists the **hvac** table you created earlier.</span></span> <span data-ttu-id="935cc-168">Vouw in de tabel als de velden in de tabel wilt zien als u eerder in de notebook hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="935cc-168">Expand the table to see the fields in the table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="935cc-169">![Lijst met tabellen op Apache Spark BI-dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "lijst tabellen op de Apache Spark BI-dashboard")</span><span class="sxs-lookup"><span data-stu-id="935cc-169">![List tables on Apache Spark BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "List tables on Apache Spark BI dashboard")</span></span>

8. <span data-ttu-id="935cc-170">Bouw een visualisatie in om het verschil tussen de doel-temperatuur- en werkelijke temperatuur voor elk gebouw weergeven.</span><span class="sxs-lookup"><span data-stu-id="935cc-170">Build a visualization to show the variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="935cc-171">Selecteer om de gegevens wilt, **vlakdiagram** (weergegeven in rood kader).</span><span class="sxs-lookup"><span data-stu-id="935cc-171">To visualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="935cc-172">Voor het definiëren van de as, slepen en neerzetten de **BuildingID** veld onder **as**, en **ActualTemp**/**TargetTemp** velden onder **waarde**.</span><span class="sxs-lookup"><span data-stu-id="935cc-172">To define the axis, drag-and-drop the **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="935cc-173">![Spark maken met behulp van Apache Spark BI gegevensvisualisaties](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "gegevensvisualisaties Spark maken met behulp van Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="935cc-173">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

9. <span data-ttu-id="935cc-174">Standaard bevat de visualisatie het totaal voor **ActualTemp** en **TargetTemp**.</span><span class="sxs-lookup"><span data-stu-id="935cc-174">By default the visualization shows the sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="935cc-175">Voor zowel de velden in de vervolgkeuzelijst selecteert **gemiddelde** ophalen van een gemiddelde van het werkelijke en doel temperaturen voor beide gebouwen.</span><span class="sxs-lookup"><span data-stu-id="935cc-175">For both the fields, from the drop-down, select **Average** to get an average of actual and target temperatures for both buildings.</span></span>

    <span data-ttu-id="935cc-176">![Spark maken met behulp van Apache Spark BI gegevensvisualisaties](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "gegevensvisualisaties Spark maken met behulp van Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="935cc-176">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

10. <span data-ttu-id="935cc-177">Uw gegevensvisualisatie moet vergelijkbaar zijn met die in de schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="935cc-177">Your data visualization should be similar to the one in the screenshot.</span></span> <span data-ttu-id="935cc-178">Plaats de cursor op de visualisatie knopinfo met relevante gegevens ophalen.</span><span class="sxs-lookup"><span data-stu-id="935cc-178">Move your cursor over the visualization to get tool tips with relevant data.</span></span>

    <span data-ttu-id="935cc-179">![Spark maken met behulp van Apache Spark BI gegevensvisualisaties](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "gegevensvisualisaties Spark maken met behulp van Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="935cc-179">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

11. <span data-ttu-id="935cc-180">Klik op **opslaan** in het menu bovenaan en geef de rapportnaam van een.</span><span class="sxs-lookup"><span data-stu-id="935cc-180">Click **Save** from the top menu and provide a report name.</span></span> <span data-ttu-id="935cc-181">U kunt ook het visuele element vastmaken.</span><span class="sxs-lookup"><span data-stu-id="935cc-181">You can also pin the visual.</span></span> <span data-ttu-id="935cc-182">Wanneer u een visualisatie vastmaken, wordt opgeslagen op uw dashboard zodat u de laatste waarde in een oogopslag kunt bijhouden.</span><span class="sxs-lookup"><span data-stu-id="935cc-182">When you pin a visualization, it is stored on your dashboard so you can track the latest value at a glance.</span></span>

   <span data-ttu-id="935cc-183">U kunt zoveel visualisaties als u voor dezelfde gegevensset wilt en aan het dashboard voor een overzicht van uw gegevens vastmaken kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="935cc-183">You can add as many visualizations as you want for the same dataset and pin them to the dashboard for a snapshot of your data.</span></span> <span data-ttu-id="935cc-184">Bovendien Spark-clusters in HDInsight zijn verbonden met Power BI met direct connect.</span><span class="sxs-lookup"><span data-stu-id="935cc-184">Also, Spark clusters on HDInsight are connected to Power BI with direct connect.</span></span> <span data-ttu-id="935cc-185">Dit zorgt ervoor dat Power BI altijd de meest recente gegevens van uw cluster heeft zodat u niet wilt vernieuwingen plannen voor de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="935cc-185">This ensures that Power BI always has the most up-to-date data from your cluster so you do not need to schedule refreshes for the dataset.</span></span>

## <span data-ttu-id="935cc-186"><a name="tableau"></a>Tableau bureaublad gebruiken voor Spark gegevensvisualisatie</span><span class="sxs-lookup"><span data-stu-id="935cc-186"><a name="tableau"></a>Use Tableau Desktop for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="935cc-187">Deze sectie geldt alleen voor 1.5.2 Spark-clusters die zijn gemaakt in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="935cc-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="935cc-188">Installeer [Tableau bureaublad](http://www.tableau.com/products/desktop) op de computer waarop u deze zelfstudie voor Apache Spark BI uitvoert.</span><span class="sxs-lookup"><span data-stu-id="935cc-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on the computer where you are running this Apache Spark BI tutorial.</span></span>

2. <span data-ttu-id="935cc-189">Zorg ervoor dat deze computer ook Microsoft Spark ODBC-stuurprogramma geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="935cc-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="935cc-190">U kunt het stuurprogramma van [hier](http://go.microsoft.com/fwlink/?LinkId=616229).</span><span class="sxs-lookup"><span data-stu-id="935cc-190">You can install the driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="935cc-191">Start Tableau bureaublad.</span><span class="sxs-lookup"><span data-stu-id="935cc-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="935cc-192">Klik in het linkerdeelvenster, uit de lijst met de server verbinding wil maken, klikt u op **Spark SQL**.</span><span class="sxs-lookup"><span data-stu-id="935cc-192">In the left pane, from the list of server to connect to, click **Spark SQL**.</span></span> <span data-ttu-id="935cc-193">Als Spark SQL niet wordt weergegeven in het linkerdeelvenster standaard, kunt u deze vinden door te klikken op **meer Servers**.</span><span class="sxs-lookup"><span data-stu-id="935cc-193">If Spark SQL is not listed by default in the left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="935cc-194">Geef de waarden in het dialoogvenster Spark SQL-verbinding zoals weergegeven in de schermafbeelding en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="935cc-194">In the Spark SQL connection dialog box, provide the values as shown in the screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="935cc-195">![Verbinding maken met een cluster voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "verbinding maken met een cluster voor Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="935cc-195">![Connect to a cluster for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect to a cluster for Apache Spark BI")</span></span>

    <span data-ttu-id="935cc-196">De vervolgkeuzelijsten verificatie **Microsoft Azure HDInsight-Service** als optie alleen als u hebt geïnstalleerd het [ODBC-stuurprogramma van Microsoft Spark](http://go.microsoft.com/fwlink/?LinkId=616229) op de computer.</span><span class="sxs-lookup"><span data-stu-id="935cc-196">The authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed the [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on the computer.</span></span>
3. <span data-ttu-id="935cc-197">Op het volgende scherm van de **Schema** omlaag, klik op de **vinden** pictogram en klik vervolgens op **standaard**.</span><span class="sxs-lookup"><span data-stu-id="935cc-197">On the next screen, from the **Schema** drop-down, click the **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="935cc-198">![Schema voor Apache Spark BI vinden](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "schema voor Apache Spark BI zoeken")</span><span class="sxs-lookup"><span data-stu-id="935cc-198">![Find schema for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")</span></span>
4. <span data-ttu-id="935cc-199">Voor de **tabel** veld, klikt u op de **vinden** pictogram opnieuw naar de lijst met alle Hive-tabellen die beschikbaar zijn in het cluster.</span><span class="sxs-lookup"><span data-stu-id="935cc-199">For the **Table** field, click the **Find** icon again to list all the Hive tables available in the cluster.</span></span> <span data-ttu-id="935cc-200">U ziet de **hvac** tabel die u eerder met de notebook gemaakt.</span><span class="sxs-lookup"><span data-stu-id="935cc-200">You should see the **hvac** table you created earlier using the notebook.</span></span>

    <span data-ttu-id="935cc-201">![Tabel niet vinden voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "tabel voor Apache Spark BI zoeken")</span><span class="sxs-lookup"><span data-stu-id="935cc-201">![Find table for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")</span></span>
5. <span data-ttu-id="935cc-202">Slepen en neerzetten van de tabel aan het eerste vak aan de rechterkant.</span><span class="sxs-lookup"><span data-stu-id="935cc-202">Drag and drop the table to the top box on the right.</span></span> <span data-ttu-id="935cc-203">Tableau de gegevens worden geïmporteerd en geeft u het schema weer als gemarkeerde door een rood kader.</span><span class="sxs-lookup"><span data-stu-id="935cc-203">Tableau imports the data and displays the schema as highlighted by the red box.</span></span>

    <span data-ttu-id="935cc-204">![Tabellen toevoegen aan Tableau voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "tabellen toevoegen aan Tableau voor Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="935cc-204">![Add tables to Tableau for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables to Tableau for Apache Spark BI")</span></span>
6. <span data-ttu-id="935cc-205">Klik op de **Sheet1** tabblad linksonder.</span><span class="sxs-lookup"><span data-stu-id="935cc-205">Click the **Sheet1** tab at the bottom left.</span></span> <span data-ttu-id="935cc-206">Controleer een visualisatie waarin de gemiddelde doel en de werkelijke temperaturen voor alle gebouwen voor elke datum.</span><span class="sxs-lookup"><span data-stu-id="935cc-206">Make a visualization that shows the average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="935cc-207">Sleep **datum** en **bouwen ID** naar **kolommen** en **werkelijke Temp**/**Temp doel** naar **rijen**.</span><span class="sxs-lookup"><span data-stu-id="935cc-207">Drag **Date** and **Building ID** to **Columns** and **Actual Temp**/**Target Temp** to **Rows**.</span></span> <span data-ttu-id="935cc-208">Onder **aanhalingstekens**, selecteer **gebied** voor het gebruik van een map gebied voor gegevensvisualisatie Spark.</span><span class="sxs-lookup"><span data-stu-id="935cc-208">Under **Marks**, select **Area** to use an area map for Spark data visualization.</span></span>

     <span data-ttu-id="935cc-209">![Toevoegen van velden voor Spark gegevensvisualisatie](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "velden voor Spark gegevensvisualisatie toevoegen")</span><span class="sxs-lookup"><span data-stu-id="935cc-209">![Add fields for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")</span></span>
7. <span data-ttu-id="935cc-210">Standaard de temperatuur velden worden weergegeven als de statistische functie.</span><span class="sxs-lookup"><span data-stu-id="935cc-210">By default, the temperature fields are shown as aggregate.</span></span> <span data-ttu-id="935cc-211">Als u weergeven van de gemiddelde temperatuur in plaats daarvan wilt, u kunt dit doen in de vervolgkeuzelijst, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="935cc-211">If you want to show the average temperatures instead, you can do so from the drop-down, as shown below.</span></span>

    <span data-ttu-id="935cc-212">![Gemiddelde temperatuur voor Spark gegevensvisualisatie nemen](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "gemiddelde temperatuur voor Spark gegevensvisualisatie duren")</span><span class="sxs-lookup"><span data-stu-id="935cc-212">![Take average of temperature for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")</span></span>

8. <span data-ttu-id="935cc-213">U kunt ook super-opleggen één temperatuur toewijzing via de andere met een beter idee van verschil tussen het doel en de werkelijke temperaturen krijgen.</span><span class="sxs-lookup"><span data-stu-id="935cc-213">You can also super-impose one temperature map over the other to get a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="935cc-214">Beweeg de muisaanwijzer naar de hoek van de lagere gebied kaart totdat u de ingang shape gemarkeerd in een rode cirkel ziet.</span><span class="sxs-lookup"><span data-stu-id="935cc-214">Move the mouse to the corner of the lower area map till you see the handle shape highlighted in a red circle.</span></span> <span data-ttu-id="935cc-215">Sleep de kaart naar de andere kaart bovenaan en de muisknop loslaat, wanneer u de vorm die is gemarkeerd in rode rechthoek ziet.</span><span class="sxs-lookup"><span data-stu-id="935cc-215">Drag the map to the other map on the top and release the mouse when you see the shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="935cc-216">![Samenvoegen van kaarten voor Spark gegevensvisualisatie](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "samenvoegen toegewezen voor Spark gegevensvisualisatie")</span><span class="sxs-lookup"><span data-stu-id="935cc-216">![Merge maps for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")</span></span>

     <span data-ttu-id="935cc-217">De weergave van uw gegevens moet wijzigen, zoals weergegeven in de schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="935cc-217">Your data visualization should change as shown in the screenshot:</span></span>

    <span data-ttu-id="935cc-218">![Tableau uitvoer voor Spark gegevensvisualisatie](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau uitvoer voor Spark gegevensvisualisatie")</span><span class="sxs-lookup"><span data-stu-id="935cc-218">![Tableau output for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")</span></span>
9. <span data-ttu-id="935cc-219">Klik op **opslaan** om op te slaan van het werkblad.</span><span class="sxs-lookup"><span data-stu-id="935cc-219">Click **Save** to save the worksheet.</span></span> <span data-ttu-id="935cc-220">U kunt dashboards maken en een of meer bladen aan toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="935cc-220">You can create dashboards and add one or more sheets to it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="935cc-221">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="935cc-221">Next steps</span></span>

<span data-ttu-id="935cc-222">Tot nu toe hebt u geleerd hoe u een cluster maakt, Spark gegevensframes query uitvoeren op gegevens maken en vervolgens toegang tot die gegevens vanuit BI-tools.</span><span class="sxs-lookup"><span data-stu-id="935cc-222">So far you learned how to create a cluster, create Spark data frames to query data, and then access that data from BI tools.</span></span> <span data-ttu-id="935cc-223">U kunt nu instructies voor het beheren van de clusterbronnen en taken die worden uitgevoerd in een HDInsight Spark-cluster voor foutopsporing bekijken.</span><span class="sxs-lookup"><span data-stu-id="935cc-223">You can now look at instructions on how to manage the cluster resources and debug jobs that are running in an HDInsight Spark cluster.</span></span>

* [<span data-ttu-id="935cc-224">Resources beheren voor het Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="935cc-224">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="935cc-225">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="935cc-225">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

