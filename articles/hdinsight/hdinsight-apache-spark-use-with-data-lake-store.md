---
title: Apache Spark gebruiken voor het analyseren van gegevens in Azure Data Lake Store | Microsoft Docs
description: Spark-taken voor het analyseren van gegevens die zijn opgeslagen in Azure Data Lake Store uitvoeren
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
ms.openlocfilehash: 66f115c4f348ccaeb8855568ba1ad50faa442173
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-hdinsight-spark-cluster-to-analyze-data-in-data-lake-store"></a><span data-ttu-id="55e91-103">HDInsight Spark-cluster gebruiken voor het analyseren van gegevens in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="55e91-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>

<span data-ttu-id="55e91-104">In deze zelfstudie maakt u Jupyter-notebook beschikbaar met HDInsight Spark-clusters gebruiken om uit te voeren van een taak die gegevens uit een Data Lake Store-account leest.</span><span class="sxs-lookup"><span data-stu-id="55e91-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55e91-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="55e91-105">Prerequisites</span></span>

* <span data-ttu-id="55e91-106">Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="55e91-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="55e91-107">Volg de instructies in [Aan de slag met Azure Data Lake Store met Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="55e91-107">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="55e91-108">Azure HDInsight Spark-cluster met Data Lake Store als opslag.</span><span class="sxs-lookup"><span data-stu-id="55e91-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="55e91-109">Volg de instructies voor [een HDInsight-cluster maken met Data Lake Store met Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="55e91-109">Follow the instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-the-data"></a><span data-ttu-id="55e91-110">De gegevens voorbereiden</span><span class="sxs-lookup"><span data-stu-id="55e91-110">Prepare the data</span></span>

> [!NOTE]
> <span data-ttu-id="55e91-111">U hoeft niet in deze stap uitvoeren als u het HDInsight-cluster met Data Lake Store als standaard opslag hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="55e91-111">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="55e91-112">De cluster-vervaardigingsproces voegt voorbeeldgegevens in de Data Lake Store-account dat u opgeeft tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="55e91-112">The cluster creation processes adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span></span> <span data-ttu-id="55e91-113">Ga naar de sectie [gebruik HDInsight Spark-cluster met Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="55e91-113">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="55e91-114">Als u een HDInsight-cluster met Data Lake Store als extra opslagruimte en Azure Storage-Blob als standaard opslag gemaakt, moet u eerst via voorbeeldgegevens kopiëren naar het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="55e91-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span></span> <span data-ttu-id="55e91-115">U kunt het voorbeeld dat gegevens van de Azure Storage-Blob die is gekoppeld aan het HDInsight-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="55e91-115">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span></span> <span data-ttu-id="55e91-116">U kunt de [ADLCopy hulpprogramma](http://aka.ms/downloadadlcopy) om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="55e91-116">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span></span> <span data-ttu-id="55e91-117">Download en installeer het hulpprogramma via de koppeling.</span><span class="sxs-lookup"><span data-stu-id="55e91-117">Download and install the tool from the link.</span></span>

1. <span data-ttu-id="55e91-118">Open een opdrachtprompt en navigeer naar de map waar AdlCopy is geïnstalleerd, doorgaans `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="55e91-118">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="55e91-119">Voer de volgende opdracht om een specifieke blob kopiëren van de Broncontainer naar een Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="55e91-119">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="55e91-120">Kopieer de **HVAC.csv** voorbeeldgegevens op het bestand **/HdiSamples/HdiSamples/SensorSampleData/hvac/** aan het Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="55e91-120">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span></span> <span data-ttu-id="55e91-121">Het codefragment moet eruitzien als:</span><span class="sxs-lookup"><span data-stu-id="55e91-121">The code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="55e91-122">Zorg ervoor dat u die de namen van de bestands- en in het juiste geval zijn.</span><span class="sxs-lookup"><span data-stu-id="55e91-122">Make sure you the file and path names are in the proper case.</span></span>
   >
   >
3. <span data-ttu-id="55e91-123">U wordt gevraagd de referenties voor de Azure-abonnement waaronder die u een Data Lake Store-account hebt invoeren.</span><span class="sxs-lookup"><span data-stu-id="55e91-123">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="55e91-124">Hier ziet u uitvoer ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="55e91-124">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="55e91-125">Het gegevensbestand (**HVAC.csv**) in een map worden gekopieerd **/hvac** in het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="55e91-125">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="55e91-126">Een HDInsight Spark-cluster gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="55e91-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="55e91-127">Klik vanuit de [Azure Portal](https://portal.azure.com/), vanaf het startboard, op de tegel voor uw Spark-cluster (als u deze aan het startboard hebt vastgemaakt).</span><span class="sxs-lookup"><span data-stu-id="55e91-127">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="55e91-128">U kunt ook naar uw cluster navigeren onder **Bladeren** > **HDInsight-clusters**.</span><span class="sxs-lookup"><span data-stu-id="55e91-128">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="55e91-129">Klik vanuit de blade Spark-cluster op **Snelkoppelingen**. Klik vervolgens vanuit het **Cluster-dashboard** op **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="55e91-129">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="55e91-130">Voer de beheerdersreferenties voor het cluster in als u daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="55e91-130">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="55e91-131">Mogelijk bereikt u de Jupyter-notebook voor uw cluster ook door de volgende URL in uw browser te openen.</span><span class="sxs-lookup"><span data-stu-id="55e91-131">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="55e91-132">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="55e91-132">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="55e91-133">Maak een nieuwe notebook.</span><span class="sxs-lookup"><span data-stu-id="55e91-133">Create a new notebook.</span></span> <span data-ttu-id="55e91-134">Klik op **Nieuw** en klik vervolgens op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="55e91-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="55e91-135">![Een nieuwe Jupyter-notebook maken](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Een nieuwe Jupyter-notebook maken")</span><span class="sxs-lookup"><span data-stu-id="55e91-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="55e91-136">Omdat u de notebook met behulp van de PySpark-kernel hebt gemaakt, hoeft u niet expliciet contexten te maken.</span><span class="sxs-lookup"><span data-stu-id="55e91-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="55e91-137">De Spark- en Hive-contexten worden automatisch voor u gemaakt tijdens het uitvoeren van de eerste codecel.</span><span class="sxs-lookup"><span data-stu-id="55e91-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="55e91-138">Als eerste stap importeert u de typen die voor dit scenario zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="55e91-138">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="55e91-139">Plak hiertoe het volgende codefragment in een cel en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="55e91-139">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="55e91-140">Telkens wanneer u een taak in Jupyter uitvoert, toont de venstertitel van uw webbrowser de status **(Bezet)** samen met de notebooktitel.</span><span class="sxs-lookup"><span data-stu-id="55e91-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="55e91-141">Ook ziet u een gevulde cirkel naast de **PySpark**-tekst in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="55e91-141">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="55e91-142">Nadat de taak is voltooid, verandert deze in een lege cirkel.</span><span class="sxs-lookup"><span data-stu-id="55e91-142">After the job is completed, this will change to a hollow circle.</span></span>

     <span data-ttu-id="55e91-143">![Status van een Jupyter-notebooktaak](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status van een Jupyter-notebooktaak")</span><span class="sxs-lookup"><span data-stu-id="55e91-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="55e91-144">Voorbeeldgegevens laden in een tijdelijke tabel met de **HVAC.csv** bestand dat u hebt gekopieerd naar het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="55e91-144">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span></span> <span data-ttu-id="55e91-145">U kunt toegang tot de gegevens in de Data Lake Store-account met behulp van de volgende URL-patroon.</span><span class="sxs-lookup"><span data-stu-id="55e91-145">You can access the data in the Data Lake Store account using the following URL pattern.</span></span>

    * <span data-ttu-id="55e91-146">Als u Data Lake Store als standaard opslag hebt, zijn HVAC.csv in het pad dat vergelijkbaar is met de volgende URL:</span><span class="sxs-lookup"><span data-stu-id="55e91-146">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="55e91-147">Of u kunt ook een kortere indeling, zoals de volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="55e91-147">Or, you could also use a shortened format such as the following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="55e91-148">Als u Data Lake Store als extra opslagruimte hebt, zijn HVAC.csv op de locatie waar u hebt gekopieerd, zoals:</span><span class="sxs-lookup"><span data-stu-id="55e91-148">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="55e91-149">Plak het volgende codevoorbeeld in een lege cel, vervangen door **MYDATALAKESTORE** met uw Data Lake Store-accountnaam en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="55e91-149">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="55e91-150">Dit codevoorbeeld registreert de gegevens in een tijdelijke tabel genaamd **hvac**.</span><span class="sxs-lookup"><span data-stu-id="55e91-150">This code example registers the data into a temporary table called **hvac**.</span></span>

            # Load the data. The path below assumes Data Lake Store is default storage for the Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create the schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse the data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register the data fram as a table to run queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="55e91-151">Omdat u een PySpark-kernel gebruikt, kunt u nu rechtstreeks een SQL-query uitvoeren op de tijdelijke tabel **hvac**, die u zojuist hebt gemaakt met behulp van de `%%sql`-magic.</span><span class="sxs-lookup"><span data-stu-id="55e91-151">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span></span> <span data-ttu-id="55e91-152">Voor meer informatie over de `%%sql`-magic, evenals over andere magics die voor de PySpark-kernel beschikbaar zijn, raadpleegt u [Beschikbare kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="55e91-152">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="55e91-153">Nadat de taak is voltooid, wordt standaard de volgende uitvoer in tabelvorm weergegeven.</span><span class="sxs-lookup"><span data-stu-id="55e91-153">Once the job is completed successfully, the following tabular output is displayed by default.</span></span>

      <span data-ttu-id="55e91-154">![Tabeluitvoer van het queryresultaat](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Tabeluitvoer van het queryresultaat")</span><span class="sxs-lookup"><span data-stu-id="55e91-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="55e91-155">U kunt de resultaten ook in andere visualisaties bekijken.</span><span class="sxs-lookup"><span data-stu-id="55e91-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="55e91-156">Zo ziet een gebiedsgrafiek voor dezelfde uitvoer er als volgt uit.</span><span class="sxs-lookup"><span data-stu-id="55e91-156">For example, an area graph for the same output would look like the following.</span></span>

     <span data-ttu-id="55e91-157">![Gebiedsgrafiek van het queryresultaat](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Gebiedsgrafiek van het queryresultaat")</span><span class="sxs-lookup"><span data-stu-id="55e91-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="55e91-158">Wanneer u klaar bent met het uitvoeren van de toepassing, moet u de notebook afsluiten om de resources vrij te geven.</span><span class="sxs-lookup"><span data-stu-id="55e91-158">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="55e91-159">Dit doet u door in het menu **Bestand** in de notebook te klikken op **Sluiten en stoppen**.</span><span class="sxs-lookup"><span data-stu-id="55e91-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="55e91-160">Hiermee wordt de notebook afgesloten.</span><span class="sxs-lookup"><span data-stu-id="55e91-160">This will shutdown and close the notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="55e91-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55e91-161">Next steps</span></span>

* [<span data-ttu-id="55e91-162">Een zelfstandige Scala toepassing uit te voeren op Apache Spark-cluster maken</span><span class="sxs-lookup"><span data-stu-id="55e91-162">Create a standalone Scala application to run on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="55e91-163">Gebruik van HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ Spark-toepassingen voor HDInsight Spark Linux-cluster maken</span><span class="sxs-lookup"><span data-stu-id="55e91-163">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="55e91-164">Gebruik van HDInsight-hulpprogramma's in Azure Toolkit voor Eclipse Spark-toepassingen voor HDInsight Spark Linux-cluster maken</span><span class="sxs-lookup"><span data-stu-id="55e91-164">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
