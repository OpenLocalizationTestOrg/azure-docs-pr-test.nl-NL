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
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a><span data-ttu-id="fcc26-103">Gebruik van HDInsight Spark-cluster tooanalyze gegevens in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fcc26-103">Use HDInsight Spark cluster tooanalyze data in Data Lake Store</span></span>

<span data-ttu-id="fcc26-104">In deze zelfstudie gebruikt u Jupyter-notebook beschikbaar met HDInsight Spark-clusters toorun een taak die gegevens uit een Data Lake Store-account leest.</span><span class="sxs-lookup"><span data-stu-id="fcc26-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters toorun a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcc26-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fcc26-105">Prerequisites</span></span>

* <span data-ttu-id="fcc26-106">Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="fcc26-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="fcc26-107">Volg de instructies Hallo voor [aan de slag met Azure Data Lake Store met Azure Portal Hallo](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fcc26-107">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="fcc26-108">Azure HDInsight Spark-cluster met Data Lake Store als opslag.</span><span class="sxs-lookup"><span data-stu-id="fcc26-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="fcc26-109">Volg de instructies Hallo voor [een HDInsight-cluster maken met Data Lake Store met Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fcc26-109">Follow hello instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-hello-data"></a><span data-ttu-id="fcc26-110">Hallo gegevens voorbereiden</span><span class="sxs-lookup"><span data-stu-id="fcc26-110">Prepare hello data</span></span>

> [!NOTE]
> <span data-ttu-id="fcc26-111">U hoeft geen tooperform deze stap als u Hallo HDInsight-cluster met Data Lake Store als standaard opslag hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fcc26-111">You do not need tooperform this step if you have created hello HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="fcc26-112">Hallo cluster vervaardigingsproces voegt voorbeeldgegevens in Hallo Data Lake Store-account die u opgeeft tijdens het Hallo-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="fcc26-112">hello cluster creation processes adds some sample data in hello Data Lake Store account that you specify while creating hello cluster.</span></span> <span data-ttu-id="fcc26-113">Toohello sectie overslaan [gebruik HDInsight Spark-cluster met Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="fcc26-113">Skip toohello section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="fcc26-114">Als u een HDInsight-cluster met Data Lake Store als extra opslagruimte en Azure Storage-Blob als standaard opslag gemaakt, moet u eerst kopiëren via sommige sample data toohello Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="fcc26-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data toohello Data Lake Store account.</span></span> <span data-ttu-id="fcc26-115">U kunt de voorbeeldgegevens Hallo uit Azure Storage-Blob die is gekoppeld aan de HDInsight-cluster Hallo Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fcc26-115">You can use hello sample data from hello Azure Storage Blob associated with hello HDInsight cluster.</span></span> <span data-ttu-id="fcc26-116">U kunt Hallo [ADLCopy hulpprogramma](http://aka.ms/downloadadlcopy) toodo zodat.</span><span class="sxs-lookup"><span data-stu-id="fcc26-116">You can use hello [ADLCopy tool](http://aka.ms/downloadadlcopy) toodo so.</span></span> <span data-ttu-id="fcc26-117">Download en installeer Hallo hulpprogramma via Hallo-koppeling.</span><span class="sxs-lookup"><span data-stu-id="fcc26-117">Download and install hello tool from hello link.</span></span>

1. <span data-ttu-id="fcc26-118">Open een opdrachtprompt en navigeer toohello directory waar AdlCopy is geïnstalleerd, doorgaans `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="fcc26-118">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="fcc26-119">Voer Hallo opdracht toocopy na een specifieke blob van Hallo bron container tooa Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="fcc26-119">Run hello following command toocopy a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="fcc26-120">Kopiëren Hallo **HVAC.csv** voorbeeldgegevens op het bestand **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="fcc26-120">Copy hello **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store account.</span></span> <span data-ttu-id="fcc26-121">Hallo-codefragment moet eruitzien als:</span><span class="sxs-lookup"><span data-stu-id="fcc26-121">hello code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="fcc26-122">Controleer of u bestand Hallo en padnamen zijn in de juiste geval Hallo.</span><span class="sxs-lookup"><span data-stu-id="fcc26-122">Make sure you hello file and path names are in hello proper case.</span></span>
   >
   >
3. <span data-ttu-id="fcc26-123">U zult de vraag tooenter Hallo referenties voor hello Azure-abonnement waaronder die u een Data Lake Store-account hebt.</span><span class="sxs-lookup"><span data-stu-id="fcc26-123">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="fcc26-124">Hier ziet u een vergelijkbare toohello volgende van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="fcc26-124">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="fcc26-125">Hallo-gegevensbestand (**HVAC.csv**) in een map worden gekopieerd **/hvac** in Hallo Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="fcc26-125">hello data file (**HVAC.csv**) will be copied under a folder **/hvac** in hello Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="fcc26-126">Een HDInsight Spark-cluster gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fcc26-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="fcc26-127">Van Hallo [Azure Portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt).</span><span class="sxs-lookup"><span data-stu-id="fcc26-127">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="fcc26-128">U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.</span><span class="sxs-lookup"><span data-stu-id="fcc26-128">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="fcc26-129">Klik vanuit Hallo blade Spark-cluster op **snelkoppelingen**, en klik vervolgens vanuit Hallo **Cluster-Dashboard** blade klikt u op **Jupyter-Notebook**.</span><span class="sxs-lookup"><span data-stu-id="fcc26-129">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="fcc26-130">Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="fcc26-130">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fcc26-131">U mogelijk ook Hallo Jupyter-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="fcc26-131">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="fcc26-132">Vervang **CLUSTERNAME** met Hallo-naam van het cluster:</span><span class="sxs-lookup"><span data-stu-id="fcc26-132">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="fcc26-133">Maak een nieuwe notebook.</span><span class="sxs-lookup"><span data-stu-id="fcc26-133">Create a new notebook.</span></span> <span data-ttu-id="fcc26-134">Klik op **Nieuw** en klik vervolgens op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="fcc26-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="fcc26-135">![Een nieuwe Jupyter-notebook maken](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Een nieuwe Jupyter-notebook maken")</span><span class="sxs-lookup"><span data-stu-id="fcc26-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="fcc26-136">Omdat u de notebook met behulp van Hallo PySpark-kernel hebt gemaakt, hoeft u geen toocreate contexten expliciet.</span><span class="sxs-lookup"><span data-stu-id="fcc26-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="fcc26-137">Hallo Spark en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel Hallo uitvoert.</span><span class="sxs-lookup"><span data-stu-id="fcc26-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="fcc26-138">U kunt starten door het Hallo-typen die nodig zijn voor dit scenario te importeren.</span><span class="sxs-lookup"><span data-stu-id="fcc26-138">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="fcc26-139">toodo plakken dus Hallo volgende codefragment in een cel en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fcc26-139">toodo so, paste hello following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="fcc26-140">Telkens wanneer u een taak in Jupyter uitvoert, de venstertitel van uw web-browser wordt weergegeven een **(bezet)** status samen met de notebooktitel Hallo.</span><span class="sxs-lookup"><span data-stu-id="fcc26-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="fcc26-141">U ziet ook een gevulde cirkel volgende toohello **PySpark** tekst in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="fcc26-141">You will also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="fcc26-142">Nadat het Hallo-taak is voltooid, wordt dit lege cirkel tooa wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fcc26-142">After hello job is completed, this will change tooa hollow circle.</span></span>

     <span data-ttu-id="fcc26-143">![Status van een Jupyter-notebooktaak](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status van een Jupyter-notebooktaak")</span><span class="sxs-lookup"><span data-stu-id="fcc26-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="fcc26-144">Voorbeeldgegevens laden in een tijdelijke tabel met Hallo **HVAC.csv** bestand dat u toohello Data Lake Store-account hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="fcc26-144">Load sample data into a temporary table using hello **HVAC.csv** file you copied toohello Data Lake Store account.</span></span> <span data-ttu-id="fcc26-145">Hallo-gegevens in Hallo Hallo URL patroon volgen met Data Lake Store-account, kunt u openen.</span><span class="sxs-lookup"><span data-stu-id="fcc26-145">You can access hello data in hello Data Lake Store account using hello following URL pattern.</span></span>

    * <span data-ttu-id="fcc26-146">Als u Data Lake Store als standaard opslag hebt, zijn HVAC.csv op Hallo pad vergelijkbare toohello volgende URL:</span><span class="sxs-lookup"><span data-stu-id="fcc26-146">If you have Data Lake Store as default storage, HVAC.csv will be at hello path similar toohello following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="fcc26-147">Of u kunt ook een kortere indeling zoals Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="fcc26-147">Or, you could also use a shortened format such as hello following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="fcc26-148">Als u Data Lake Store als extra opslagruimte hebt, zijn HVAC.csv op Hallo-locatie waar u hebt gekopieerd, zoals:</span><span class="sxs-lookup"><span data-stu-id="fcc26-148">If you have Data Lake Store as additional storage, HVAC.csv will be at hello location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="fcc26-149">Vervang in een lege cel, plakken Hallo volgende codevoorbeeld, **MYDATALAKESTORE** met uw Data Lake Store-accountnaam en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fcc26-149">In an empty cell, paste hello following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="fcc26-150">Dit codevoorbeeld registreert Hallo gegevens in een tijdelijke tabel genaamd **hvac**.</span><span class="sxs-lookup"><span data-stu-id="fcc26-150">This code example registers hello data into a temporary table called **hvac**.</span></span>

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

6. <span data-ttu-id="fcc26-151">Omdat u een PySpark-kernel gebruikt, u kunt nu rechtstreeks uitvoeren een SQL-query op de tijdelijke tabel Hallo **hvac** dat u zojuist hebt gemaakt met behulp van Hallo `%%sql` verwerkt Magic-pakket.</span><span class="sxs-lookup"><span data-stu-id="fcc26-151">Because you are using a PySpark kernel, you can now directly run a SQL query on hello temporary table **hvac** that you just created by using hello `%%sql` magic.</span></span> <span data-ttu-id="fcc26-152">Voor meer informatie over Hallo `%%sql` magic, evenals andere magics die beschikbaar zijn met de PySpark-kernel hello, Zie [beschikbare Kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="fcc26-152">For more information about hello `%%sql` magic, as well as other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="fcc26-153">Zodra het Hallo-taak is voltooid, wordt standaard Hallo na uitvoer in tabelvorm weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fcc26-153">Once hello job is completed successfully, hello following tabular output is displayed by default.</span></span>

      <span data-ttu-id="fcc26-154">![Tabeluitvoer van het queryresultaat](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Tabeluitvoer van het queryresultaat")</span><span class="sxs-lookup"><span data-stu-id="fcc26-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="fcc26-155">U ziet ook Hallo resulteert in een andere visualisaties.</span><span class="sxs-lookup"><span data-stu-id="fcc26-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="fcc26-156">Bijvoorbeeld, een gebiedsgrafiek voor dezelfde uitvoer Hallo volgende eruit zou Hallo.</span><span class="sxs-lookup"><span data-stu-id="fcc26-156">For example, an area graph for hello same output would look like hello following.</span></span>

     <span data-ttu-id="fcc26-157">![Gebiedsgrafiek van het queryresultaat](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Gebiedsgrafiek van het queryresultaat")</span><span class="sxs-lookup"><span data-stu-id="fcc26-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="fcc26-158">Als u klaar bent met het uitvoeren van de toepassing hello moet afsluiten Hallo notebook toorelease Hallo resources.</span><span class="sxs-lookup"><span data-stu-id="fcc26-158">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="fcc26-159">toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**.</span><span class="sxs-lookup"><span data-stu-id="fcc26-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="fcc26-160">Deze wordt afgesloten en sluiten Hallo notebook.</span><span class="sxs-lookup"><span data-stu-id="fcc26-160">This will shutdown and close hello notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fcc26-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fcc26-161">Next steps</span></span>

* [<span data-ttu-id="fcc26-162">Een zelfstandige Scala toepassing toorun op Apache Spark-cluster maken</span><span class="sxs-lookup"><span data-stu-id="fcc26-162">Create a standalone Scala application toorun on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="fcc26-163">Gebruik van HDInsight Tools voor IntelliJ toocreate Spark scala-toepassingen voor HDInsight Spark Linux-cluster in Azure Toolkit</span><span class="sxs-lookup"><span data-stu-id="fcc26-163">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="fcc26-164">HDInsight-hulpprogramma's gebruiken in Azure Toolkit voor Eclipse toocreate Spark scala-toepassingen voor HDInsight Spark Linux-cluster</span><span class="sxs-lookup"><span data-stu-id="fcc26-164">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
