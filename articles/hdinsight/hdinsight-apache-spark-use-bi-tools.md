---
title: aaaSpark BI hulpmiddelen voor gegevensvisualisatie met op Azure HDInsight | Microsoft Docs
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
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a><span data-ttu-id="80186-104">Apache Spark BI hulpmiddelen voor gegevensvisualisatie gebruiken met Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="80186-104">Apache Spark BI using data visualization tools with Azure HDInsight</span></span>

<span data-ttu-id="80186-105">Meer informatie over hoe toouse gegevensvisualisatie hulpmiddelen zoals Power BI en Tableau tooanalyze een onbewerkte voorbeeldgegevensset met BI van Apache Spark in HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="80186-105">Learn how toouse data visualization tools such as Power BI and Tableau tooanalyze a raw sample data set using Apache Spark BI on HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="80186-106">Connectiviteit met BI-tools die worden beschreven in dit artikel wordt niet ondersteund op 2.1 Spark op Azure HDInsight 3.6 Preview.</span><span class="sxs-lookup"><span data-stu-id="80186-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="80186-107">Alleen Spark versie 1.6 en 2.0 (HDInsight 3.4 3.5 respectievelijk) worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="80186-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="80186-108">Deze zelfstudie is ook beschikbaar als een Jupyter-notebook in een HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="80186-108">This tutorial is also available as a Jupyter notebook on an HDInsight Spark cluster.</span></span> <span data-ttu-id="80186-109">Hallo-notebook ervaring kunt u Hallo Python codefragmenten uit Hallo laptop zelf uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="80186-109">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="80186-110">tooperform hello zelfstudie uit binnen een laptop, een Spark-cluster maken, een Jupyter-notebook starten (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), en voer vervolgens de notebook Hallo **gebruik BI-tools met Apache Spark in HDInsight.ipynb** onder Hallo **Python**  map.</span><span class="sxs-lookup"><span data-stu-id="80186-110">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under hello **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80186-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="80186-111">Prerequisites</span></span>

* <span data-ttu-id="80186-112">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80186-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="80186-113">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="80186-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <span data-ttu-id="80186-114"><a name="hivetable"></a>Gegevens voorbereiden voor Spark gegevensvisualisatie</span><span class="sxs-lookup"><span data-stu-id="80186-114"><a name="hivetable"></a>Prepare data for Spark data visualization</span></span>

<span data-ttu-id="80186-115">In deze sectie gebruiken we Hallo [Jupyter](https://jupyter.org) laptop van een HDInsight Spark-cluster toorun taken die uw onbewerkte voorbeeldgegevens en deze opslaan in een tabel.</span><span class="sxs-lookup"><span data-stu-id="80186-115">In this section, we use hello [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster toorun jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="80186-116">Hallo voorbeeldgegevens is een CSV-bestand (hvac.csv) beschikbaar in alle clusters standaard.</span><span class="sxs-lookup"><span data-stu-id="80186-116">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span> <span data-ttu-id="80186-117">Wanneer uw gegevens wordt opgeslagen als een tabel, in de volgende sectie Hallo we gebruik BI extra tooconnect toohello tabel en gegevensvisualisaties uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="80186-117">Once your data is saved as a table, in hello next section we use BI tools tooconnect toohello table and perform data visualizations.</span></span>

> [!NOTE]
> <span data-ttu-id="80186-118">Als u uitvoert Hallo stappen in dit artikel na het voltooien van de instructies in Hallo [interactieve query's uitvoeren op een HDInsight Spark-cluster](hdinsight-apache-spark-load-data-run-query.md), kunt u tooStep 8 hieronder overslaan.</span><span class="sxs-lookup"><span data-stu-id="80186-118">If you are performing hello steps in this article after completing hello instructions in [Run interactive queries on an HDInsight Spark cluster](hdinsight-apache-spark-load-data-run-query.md), you can skip tooStep 8 below.</span></span>
>

1. <span data-ttu-id="80186-119">Van Hallo [Azure-portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt).</span><span class="sxs-lookup"><span data-stu-id="80186-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="80186-120">U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.</span><span class="sxs-lookup"><span data-stu-id="80186-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="80186-121">Klik op Hallo blade Spark-cluster **Cluster-Dashboard**, en klik vervolgens op **Jupyter-Notebook**.</span><span class="sxs-lookup"><span data-stu-id="80186-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="80186-122">Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="80186-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="80186-123">U mogelijk ook Hallo Jupyter-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="80186-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="80186-124">Vervang **CLUSTERNAME** met Hallo-naam van het cluster:</span><span class="sxs-lookup"><span data-stu-id="80186-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="80186-125">Maak een notebook.</span><span class="sxs-lookup"><span data-stu-id="80186-125">Create a notebook.</span></span> <span data-ttu-id="80186-126">Klik op **Nieuw** en klik vervolgens op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="80186-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="80186-127">![Een Jupyter-notebook maken voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "een Jupyter-notebook maken voor Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="80186-127">![Create a Jupyter notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Create a Jupyter notebook for Apache Spark BI")</span></span>

4. <span data-ttu-id="80186-128">Een nieuwe notebook gemaakt en geopend met de Hallo naam Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="80186-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="80186-129">Klik op Hallo notebook naam Hallo boven en een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="80186-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="80186-130">![Geef een naam voor de notebook Hallo voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Geef een naam voor de notebook Hallo voor Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="80186-130">![Provide a name for hello notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Provide a name for hello notebook for Apache Spark BI")</span></span>

5. <span data-ttu-id="80186-131">Omdat u de notebook met behulp van Hallo PySpark-kernel hebt gemaakt, hoeft u geen toocreate contexten expliciet.</span><span class="sxs-lookup"><span data-stu-id="80186-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="80186-132">Hallo Spark en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel Hallo uitvoert.</span><span class="sxs-lookup"><span data-stu-id="80186-132">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="80186-133">U kunt starten door het Hallo-typen die nodig zijn voor dit scenario te importeren.</span><span class="sxs-lookup"><span data-stu-id="80186-133">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="80186-134">Hallo cursor toodo dus plaats in Hallo cel en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="80186-134">toodo so, place hello cursor in hello cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="80186-135">Laad voorbeeldgegevens in een tijdelijke tabel.</span><span class="sxs-lookup"><span data-stu-id="80186-135">Load sample data into a temporary table.</span></span> <span data-ttu-id="80186-136">Wanneer u een Spark-cluster in HDInsight, Hallo voorbeeldgegevensbestand, maakt **hvac.csv**, is het opslagaccount gekopieerde toohello gekoppeld onder **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="80186-136">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="80186-137">In een lege cel, plak Hallo volgende codefragment en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="80186-137">In an empty cell, paste hello following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="80186-138">In dit fragment Hallo gegevens geregistreerd in een tabel met de naam **hvac**.</span><span class="sxs-lookup"><span data-stu-id="80186-138">This snippet registers hello data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. <span data-ttu-id="80186-139">Controleer of dat deze Hallo-tabel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="80186-139">Verify that hello table was successfully created.</span></span> <span data-ttu-id="80186-140">U kunt Hallo `%%sql` toorun Hive-query's rechtstreeks magic.</span><span class="sxs-lookup"><span data-stu-id="80186-140">You can use hello `%%sql` magic toorun Hive queries directly.</span></span> <span data-ttu-id="80186-141">Voor meer informatie over Hallo `%%sql` magic en andere magics die beschikbaar zijn met de PySpark-kernel hello, Zie [beschikbare Kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="80186-141">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="80186-142">Ziet u uitvoer zoals hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="80186-142">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="80186-143">Alleen Hallo tabellen waarvoor false onder Hallo **isTemporary** kolom hive-tabellen die zijn opgeslagen in het Hallo-metastore en toegankelijk zijn vanuit Hallo BI-hulpprogramma's zijn.</span><span class="sxs-lookup"><span data-stu-id="80186-143">Only hello tables that have false under hello **isTemporary** column are hive tables that are stored in hello metastore and can be accessed from hello BI tools.</span></span> <span data-ttu-id="80186-144">In deze zelfstudie we verbinding maken met toohello **hvac** tabel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="80186-144">In this tutorial, we connect toohello **hvac** table we created.</span></span>

8. <span data-ttu-id="80186-145">Controleren of dat deze tabel Hallo Hallo bedoeld gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="80186-145">Verify that hello table contains hello intended data.</span></span> <span data-ttu-id="80186-146">Kopieer in een lege cel in de notebook Hallo Hallo volgende codefragment en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="80186-146">In an empty cell in hello notebook, copy hello following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="80186-147">Hallo-notebook toorelease Hallo resources afgesloten.</span><span class="sxs-lookup"><span data-stu-id="80186-147">Shut down hello notebook toorelease hello resources.</span></span> <span data-ttu-id="80186-148">toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**.</span><span class="sxs-lookup"><span data-stu-id="80186-148">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <span data-ttu-id="80186-149"><a name="powerbi"></a>Gebruik Power BI voor Spark gegevensvisualisatie</span><span class="sxs-lookup"><span data-stu-id="80186-149"><a name="powerbi"></a>Use Power BI for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="80186-150">Deze sectie geldt alleen voor Spark 1.6 op HDInsight 3.4 en Spark 2.0 op HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="80186-150">This section is applicable only for Spark 1.6 on HDInsight 3.4 and Spark 2.0 on HDInsight 3.5.</span></span>
>
>

<span data-ttu-id="80186-151">Wanneer u Hallo gegevens hebt opgeslagen als een tabel, kunt u Power BI tooconnect toohello gegevens gebruiken en deze toocreate rapporten, visualiseren dashboards, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="80186-151">Once you have saved hello data as a table, you can use Power BI tooconnect toohello data and visualize it toocreate reports, dashboards, etc.</span></span>

1. <span data-ttu-id="80186-152">Zorg ervoor dat u hebt toegang tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="80186-152">Make sure you have access tooPower BI.</span></span> <span data-ttu-id="80186-153">U krijgt een abonnement gratis preview van Power BI van [http://www.powerbi.com/](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="80186-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="80186-154">Aanmelden te[Power BI](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="80186-154">Sign in too[Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="80186-155">Hallo onder aan het linkerdeelvenster hello, klik op **gegevens ophalen**.</span><span class="sxs-lookup"><span data-stu-id="80186-155">From hello bottom of hello left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="80186-156">Op Hallo **gegevens ophalen** pagina onder **importeren of verbinding maken tooData**, voor **Databases**, klikt u op **ophalen**.</span><span class="sxs-lookup"><span data-stu-id="80186-156">On hello **Get Data** page, under **Import or Connect tooData**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="80186-157">![Ophalen van gegevens in Power BI voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "gegevens in Power BI voor Apache Spark BI ophalen")</span><span class="sxs-lookup"><span data-stu-id="80186-157">![Get data into Power BI for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI for Apache Spark BI")</span></span>

5. <span data-ttu-id="80186-158">Klik op volgende welkomstscherm **Spark op Azure HDInsight** en klik vervolgens op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="80186-158">On hello next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="80186-159">Voer desgevraagd Hallo cluster-URL (`mysparkcluster.azurehdinsight.net`) en Hallo referenties tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="80186-159">When prompted, enter hello cluster URL (`mysparkcluster.azurehdinsight.net`) and hello credentials tooconnect toohello cluster.</span></span>

    <span data-ttu-id="80186-160">![Verbinding maken met tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "tooApache Spark BI verbinding")</span><span class="sxs-lookup"><span data-stu-id="80186-160">![Connect tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connect tooApache Spark BI")</span></span>

    <span data-ttu-id="80186-161">Na het Hallo-verbinding tot stand is gebracht, wordt in Power BI start importeren van gegevens uit Hallo Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80186-161">After hello connection is established, Power BI starts importing data from hello Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="80186-162">Power BI Hallo gegevens worden geïmporteerd en voegt een **Spark** gegevensset onder Hallo **gegevenssets** kop.</span><span class="sxs-lookup"><span data-stu-id="80186-162">Power BI imports hello data and adds a **Spark** dataset under hello **Datasets** heading.</span></span> <span data-ttu-id="80186-163">Klik op Hallo gegevensset tooopen een nieuw werkblad toovisualize Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="80186-163">Click hello data set tooopen a new worksheet toovisualize hello data.</span></span> <span data-ttu-id="80186-164">U kunt ook Hallo werkblad opslaan als een rapport.</span><span class="sxs-lookup"><span data-stu-id="80186-164">You can also save hello worksheet as a report.</span></span> <span data-ttu-id="80186-165">een werkblad van Hallo toosave **bestand** menu, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="80186-165">toosave a worksheet, from hello **File** menu, click **Save**.</span></span>

    <span data-ttu-id="80186-166">![Apache Spark BI-tegel in Power BI-dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI-tegel in Power BI-dashboard")</span><span class="sxs-lookup"><span data-stu-id="80186-166">![Apache Spark BI tile on Power BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="80186-167">U ziet dat Hallo **velden** lijst aan de rechterkant Hallo Hallo bevat **hvac** tabel die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="80186-167">Notice that hello **Fields** list on hello right lists hello **hvac** table you created earlier.</span></span> <span data-ttu-id="80186-168">Vouw Hallo tabel toosee Hallo velden in de tabel hello, zoals u eerder in de notebook hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="80186-168">Expand hello table toosee hello fields in hello table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="80186-169">![Lijst met tabellen op Apache Spark BI-dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "lijst tabellen op de Apache Spark BI-dashboard")</span><span class="sxs-lookup"><span data-stu-id="80186-169">![List tables on Apache Spark BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "List tables on Apache Spark BI dashboard")</span></span>

8. <span data-ttu-id="80186-170">Bouw een visualisatie tooshow Hallo verschil tussen doel temperatuur- en werkelijke temperatuur voor elk gebouw.</span><span class="sxs-lookup"><span data-stu-id="80186-170">Build a visualization tooshow hello variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="80186-171">gegevens van toovisualize wilt, schakelt u **vlakdiagram** (weergegeven in rood kader).</span><span class="sxs-lookup"><span data-stu-id="80186-171">toovisualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="80186-172">slepen en neerzetten Hallo-as Hallo toodefine **BuildingID** veld onder **as**, en **ActualTemp**/**TargetTemp** velden onder **waarde**.</span><span class="sxs-lookup"><span data-stu-id="80186-172">toodefine hello axis, drag-and-drop hello **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="80186-173">![Spark maken met behulp van Apache Spark BI gegevensvisualisaties](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "gegevensvisualisaties Spark maken met behulp van Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="80186-173">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

9. <span data-ttu-id="80186-174">Standaard bevat Hallo visualisatie Hallo som voor **ActualTemp** en **TargetTemp**.</span><span class="sxs-lookup"><span data-stu-id="80186-174">By default hello visualization shows hello sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="80186-175">Selecteer voor beide velden uit de vervolgkeuzelijst Hallo Hallo **gemiddelde** tooget gemiddeld werkelijke en doel temperaturen voor beide gebouwen.</span><span class="sxs-lookup"><span data-stu-id="80186-175">For both hello fields, from hello drop-down, select **Average** tooget an average of actual and target temperatures for both buildings.</span></span>

    <span data-ttu-id="80186-176">![Spark maken met behulp van Apache Spark BI gegevensvisualisaties](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "gegevensvisualisaties Spark maken met behulp van Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="80186-176">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

10. <span data-ttu-id="80186-177">Uw gegevensvisualisatie moet vergelijkbaar toohello in Hallo schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="80186-177">Your data visualization should be similar toohello one in hello screenshot.</span></span> <span data-ttu-id="80186-178">Plaats de cursor op Hallo visualisatie tooget knopinfo met relevante gegevens.</span><span class="sxs-lookup"><span data-stu-id="80186-178">Move your cursor over hello visualization tooget tool tips with relevant data.</span></span>

    <span data-ttu-id="80186-179">![Spark maken met behulp van Apache Spark BI gegevensvisualisaties](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "gegevensvisualisaties Spark maken met behulp van Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="80186-179">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

11. <span data-ttu-id="80186-180">Klik op **opslaan** van Hallo bovenste menu en geef de rapportnaam van een.</span><span class="sxs-lookup"><span data-stu-id="80186-180">Click **Save** from hello top menu and provide a report name.</span></span> <span data-ttu-id="80186-181">U kunt ook visual Hallo vastmaken.</span><span class="sxs-lookup"><span data-stu-id="80186-181">You can also pin hello visual.</span></span> <span data-ttu-id="80186-182">Wanneer u een visualisatie vastmaken, wordt opgeslagen op uw dashboard zodat u de laatste waarde in een oogopslag Hallo kunt bijhouden.</span><span class="sxs-lookup"><span data-stu-id="80186-182">When you pin a visualization, it is stored on your dashboard so you can track hello latest value at a glance.</span></span>

   <span data-ttu-id="80186-183">U kunt zoveel visualisaties als u wilt voor toevoegen Hallo dezelfde gegevensset en een pincode ze toohello dashboard voor een momentopname van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="80186-183">You can add as many visualizations as you want for hello same dataset and pin them toohello dashboard for a snapshot of your data.</span></span> <span data-ttu-id="80186-184">Spark-clusters in HDInsight zijn ook verbonden tooPower BI met direct connect.</span><span class="sxs-lookup"><span data-stu-id="80186-184">Also, Spark clusters on HDInsight are connected tooPower BI with direct connect.</span></span> <span data-ttu-id="80186-185">Dit zorgt ervoor dat Power BI altijd Hallo de meeste recente gegevens van uw cluster heeft zodat u geen tooschedule wordt vernieuwd voor Hallo gegevensset hoeft.</span><span class="sxs-lookup"><span data-stu-id="80186-185">This ensures that Power BI always has hello most up-to-date data from your cluster so you do not need tooschedule refreshes for hello dataset.</span></span>

## <span data-ttu-id="80186-186"><a name="tableau"></a>Tableau bureaublad gebruiken voor Spark gegevensvisualisatie</span><span class="sxs-lookup"><span data-stu-id="80186-186"><a name="tableau"></a>Use Tableau Desktop for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="80186-187">Deze sectie geldt alleen voor 1.5.2 Spark-clusters die zijn gemaakt in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80186-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="80186-188">Installeer [Tableau bureaublad](http://www.tableau.com/products/desktop) op Hallo-computer waarop u deze zelfstudie voor Apache Spark BI uitvoert.</span><span class="sxs-lookup"><span data-stu-id="80186-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on hello computer where you are running this Apache Spark BI tutorial.</span></span>

2. <span data-ttu-id="80186-189">Zorg ervoor dat deze computer ook Microsoft Spark ODBC-stuurprogramma geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="80186-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="80186-190">U kunt installeren stuurprogramma Hallo van [hier](http://go.microsoft.com/fwlink/?LinkId=616229).</span><span class="sxs-lookup"><span data-stu-id="80186-190">You can install hello driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="80186-191">Start Tableau bureaublad.</span><span class="sxs-lookup"><span data-stu-id="80186-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="80186-192">Klik in het linkerdeelvenster Hallo uit de lijst Hallo van server tooconnect, **Spark SQL**.</span><span class="sxs-lookup"><span data-stu-id="80186-192">In hello left pane, from hello list of server tooconnect to, click **Spark SQL**.</span></span> <span data-ttu-id="80186-193">Als Spark SQL niet wordt weergegeven in het linkerdeelvenster Hallo standaard, kunt u deze vinden door te klikken op **meer Servers**.</span><span class="sxs-lookup"><span data-stu-id="80186-193">If Spark SQL is not listed by default in hello left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="80186-194">Hallo Spark SQL-verbinding in het dialoogvenster, Hallo waarden zoals weergegeven in de schermafbeelding hello, op en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="80186-194">In hello Spark SQL connection dialog box, provide hello values as shown in hello screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="80186-195">![Verbinding maken met tooa cluster voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect tooa cluster voor Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="80186-195">![Connect tooa cluster for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect tooa cluster for Apache Spark BI")</span></span>

    <span data-ttu-id="80186-196">Hallo verificatie vervolgkeuzelijsten **Microsoft Azure HDInsight-Service** als optie alleen als u Hallo geïnstalleerd [ODBC-stuurprogramma van Microsoft Spark](http://go.microsoft.com/fwlink/?LinkId=616229) op Hallo-computer.</span><span class="sxs-lookup"><span data-stu-id="80186-196">hello authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed hello [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on hello computer.</span></span>
3. <span data-ttu-id="80186-197">Op de volgende scherm Hallo van Hallo **Schema** omlaag, klikt u op Hallo **vinden** pictogram en klik vervolgens op **standaard**.</span><span class="sxs-lookup"><span data-stu-id="80186-197">On hello next screen, from hello **Schema** drop-down, click hello **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="80186-198">![Schema voor Apache Spark BI vinden](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "schema voor Apache Spark BI zoeken")</span><span class="sxs-lookup"><span data-stu-id="80186-198">![Find schema for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")</span></span>
4. <span data-ttu-id="80186-199">Voor Hallo **tabel** veld, klikt u op Hallo **vinden** pictogram opnieuw toolist alle Hallo Hive-tabellen die beschikbaar zijn in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="80186-199">For hello **Table** field, click hello **Find** icon again toolist all hello Hive tables available in hello cluster.</span></span> <span data-ttu-id="80186-200">U ziet Hallo **hvac** tabel eerder met Hallo laptop hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="80186-200">You should see hello **hvac** table you created earlier using hello notebook.</span></span>

    <span data-ttu-id="80186-201">![Tabel niet vinden voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "tabel voor Apache Spark BI zoeken")</span><span class="sxs-lookup"><span data-stu-id="80186-201">![Find table for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")</span></span>
5. <span data-ttu-id="80186-202">Slepen en neerzetten Hallo tabel toohello bovenste vak op Hallo rechts.</span><span class="sxs-lookup"><span data-stu-id="80186-202">Drag and drop hello table toohello top box on hello right.</span></span> <span data-ttu-id="80186-203">Tableau hello gegevens worden geïmporteerd en worden Hallo schema als gemarkeerde door Hallo rood kader weergegeven.</span><span class="sxs-lookup"><span data-stu-id="80186-203">Tableau imports hello data and displays hello schema as highlighted by hello red box.</span></span>

    <span data-ttu-id="80186-204">![Tabellen tooTableau toevoegen voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "tabellen tooTableau voor Apache Spark BI toevoegen")</span><span class="sxs-lookup"><span data-stu-id="80186-204">![Add tables tooTableau for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables tooTableau for Apache Spark BI")</span></span>
6. <span data-ttu-id="80186-205">Klik op Hallo **Sheet1** op Hallo linksonder tabblad.</span><span class="sxs-lookup"><span data-stu-id="80186-205">Click hello **Sheet1** tab at hello bottom left.</span></span> <span data-ttu-id="80186-206">Controleer een visualisatie waarin Hallo gemiddelde doel en de werkelijke temperaturen voor alle gebouwen voor elke datum.</span><span class="sxs-lookup"><span data-stu-id="80186-206">Make a visualization that shows hello average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="80186-207">Sleep **datum** en **gebouw-ID** te**kolommen** en **werkelijke Temp**/**doel Temp**te**rijen**.</span><span class="sxs-lookup"><span data-stu-id="80186-207">Drag **Date** and **Building ID** too**Columns** and **Actual Temp**/**Target Temp** too**Rows**.</span></span> <span data-ttu-id="80186-208">Onder **aanhalingstekens**, selecteer **gebied** toouse voor Spark gegevensvisualisatie een toewijzing van gebied.</span><span class="sxs-lookup"><span data-stu-id="80186-208">Under **Marks**, select **Area** toouse an area map for Spark data visualization.</span></span>

     <span data-ttu-id="80186-209">![Toevoegen van velden voor Spark gegevensvisualisatie](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "velden voor Spark gegevensvisualisatie toevoegen")</span><span class="sxs-lookup"><span data-stu-id="80186-209">![Add fields for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")</span></span>
7. <span data-ttu-id="80186-210">Standaard Hallo temperatuur velden worden weergegeven als de statistische functie.</span><span class="sxs-lookup"><span data-stu-id="80186-210">By default, hello temperature fields are shown as aggregate.</span></span> <span data-ttu-id="80186-211">Als u in plaats daarvan tooshow Hallo gemiddelde temperatuur wilt, kunt u doen in vervolgkeuzelijst hello, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="80186-211">If you want tooshow hello average temperatures instead, you can do so from hello drop-down, as shown below.</span></span>

    <span data-ttu-id="80186-212">![Gemiddelde temperatuur voor Spark gegevensvisualisatie nemen](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "gemiddelde temperatuur voor Spark gegevensvisualisatie duren")</span><span class="sxs-lookup"><span data-stu-id="80186-212">![Take average of temperature for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")</span></span>

8. <span data-ttu-id="80186-213">U kunt ook super-opleggen één temperatuur kaart Hallo meer dan andere tooget een beter idee van verschil tussen het doel en de werkelijke temperaturen.</span><span class="sxs-lookup"><span data-stu-id="80186-213">You can also super-impose one temperature map over hello other tooget a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="80186-214">Hallo muis toohello hoek van Hallo lagere gebied kaart verplaatsen totdat u Hallo ingang shape gemarkeerd in een rode cirkel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="80186-214">Move hello mouse toohello corner of hello lower area map till you see hello handle shape highlighted in a red circle.</span></span> <span data-ttu-id="80186-215">Sleep Hallo toewijzen toohello andere kaart op Hallo boven- en release Hallo muis wanneer er Hallo vorm in rode rechthoek gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="80186-215">Drag hello map toohello other map on hello top and release hello mouse when you see hello shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="80186-216">![Samenvoegen van kaarten voor Spark gegevensvisualisatie](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "samenvoegen toegewezen voor Spark gegevensvisualisatie")</span><span class="sxs-lookup"><span data-stu-id="80186-216">![Merge maps for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")</span></span>

     <span data-ttu-id="80186-217">De weergave van uw gegevens moet wijzigen, zoals weergegeven in de schermafbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="80186-217">Your data visualization should change as shown in hello screenshot:</span></span>

    <span data-ttu-id="80186-218">![Tableau uitvoer voor Spark gegevensvisualisatie](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau uitvoer voor Spark gegevensvisualisatie")</span><span class="sxs-lookup"><span data-stu-id="80186-218">![Tableau output for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")</span></span>
9. <span data-ttu-id="80186-219">Klik op **opslaan** toosave Hallo werkblad.</span><span class="sxs-lookup"><span data-stu-id="80186-219">Click **Save** toosave hello worksheet.</span></span> <span data-ttu-id="80186-220">U kunt dashboards maken en toevoegen van een of meer werkbladen tooit.</span><span class="sxs-lookup"><span data-stu-id="80186-220">You can create dashboards and add one or more sheets tooit.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80186-221">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="80186-221">Next steps</span></span>

<span data-ttu-id="80186-222">Tot nu toe hebt u geleerd hoe toocreate een cluster, Spark gegevens frames tooquery gegevens maken en vervolgens toegang tot die gegevens vanuit BI-tools.</span><span class="sxs-lookup"><span data-stu-id="80186-222">So far you learned how toocreate a cluster, create Spark data frames tooquery data, and then access that data from BI tools.</span></span> <span data-ttu-id="80186-223">U kunt nu zoeken op instructies over hoe toomanage Hallo clusterbronnen en taken die worden uitgevoerd in een HDInsight Spark-cluster voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="80186-223">You can now look at instructions on how toomanage hello cluster resources and debug jobs that are running in an HDInsight Spark cluster.</span></span>

* [<span data-ttu-id="80186-224">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="80186-224">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="80186-225">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="80186-225">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

