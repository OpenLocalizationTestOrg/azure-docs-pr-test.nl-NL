---
title: Aangepaste Maven-pakketten gebruiken met Jupyter in Spark op Azure HDInsight | Microsoft Docs
description: Stapsgewijze instructies voor het configureren van Jupyter-notebooks met HDInsight Spark-clusters aangepaste Maven-pakketten gebruiken.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 0bcfe220e60e34937c667c7b416065d5f3dc8d63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="111a6-103">Externe pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="111a6-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="111a6-104">Met behulp van de cel verwerkt Magic-pakket</span><span class="sxs-lookup"><span data-stu-id="111a6-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="111a6-105">Met behulp van de scriptactie</span><span class="sxs-lookup"><span data-stu-id="111a6-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="111a6-106">Informatie over het configureren van een Jupyter-notebook in Apache Spark-cluster in HDInsight gebruiken van externe, community bijgedragen **maven** pakketten die niet out-of-the-box opgenomen in het cluster.</span><span class="sxs-lookup"><span data-stu-id="111a6-106">Learn how to configure a Jupyter notebook in Apache Spark cluster on HDInsight to use external, community-contributed **maven** packages that are not included out-of-the-box in the cluster.</span></span> 

<span data-ttu-id="111a6-107">U kunt zoeken in de [Maven opslagplaats](http://search.maven.org/) voor de volledige lijst met pakketten die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="111a6-107">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="111a6-108">U kunt ook een lijst met beschikbare pakketten opvragen uit andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="111a6-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="111a6-109">Bijvoorbeeld, een volledige lijst met pakketten community bijgedragen is beschikbaar op [Spark pakketten](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="111a6-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="111a6-110">In dit artikel leert u hoe u de [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakket met de Jupyter-notebook.</span><span class="sxs-lookup"><span data-stu-id="111a6-110">In this article, you will learn how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="111a6-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="111a6-111">Prerequisites</span></span>
<span data-ttu-id="111a6-112">U hebt het volgende:</span><span class="sxs-lookup"><span data-stu-id="111a6-112">You must have the following:</span></span>

* <span data-ttu-id="111a6-113">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="111a6-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="111a6-114">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="111a6-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="111a6-115">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="111a6-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="111a6-116">Klik vanuit de [Azure Portal](https://portal.azure.com/), vanaf het startboard, op de tegel voor uw Spark-cluster (als u deze aan het startboard hebt vastgemaakt).</span><span class="sxs-lookup"><span data-stu-id="111a6-116">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="111a6-117">U kunt ook naar uw cluster navigeren onder **Bladeren** > **HDInsight-clusters**.</span><span class="sxs-lookup"><span data-stu-id="111a6-117">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="111a6-118">Klik vanuit de blade Spark-cluster op **Snelkoppelingen**. Klik vervolgens vanuit het **Cluster-dashboard** op **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="111a6-118">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="111a6-119">Voer de beheerdersreferenties voor het cluster in als u daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="111a6-119">If prompted, enter the admin credentials for the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="111a6-120">Mogelijk bereikt u de Jupyter-notebook voor uw cluster ook door de volgende URL in uw browser te openen.</span><span class="sxs-lookup"><span data-stu-id="111a6-120">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="111a6-121">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="111a6-121">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="111a6-122">Maak een nieuwe notebook.</span><span class="sxs-lookup"><span data-stu-id="111a6-122">Create a new notebook.</span></span> <span data-ttu-id="111a6-123">Klik op **nieuw**, en klik vervolgens op **Spark**.</span><span class="sxs-lookup"><span data-stu-id="111a6-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="111a6-124">![Een nieuwe Jupyter-notebook maken](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Een nieuwe Jupyter-notebook maken")</span><span class="sxs-lookup"><span data-stu-id="111a6-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="111a6-125">Er wordt een nieuwe notebook gemaakt en geopend met de naam Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="111a6-125">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="111a6-126">Klik bovenaan op de naam van de notebook en wijzig deze in een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="111a6-126">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="111a6-127">![Een naam opgeven voor de notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Een naam opgeven voor de notebook")</span><span class="sxs-lookup"><span data-stu-id="111a6-127">![Provide a name for the notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="111a6-128">U gebruikt de `%%configure` verwerkt Magic-pakket voor het configureren van de notebook voor het gebruik van een externe-pakket.</span><span class="sxs-lookup"><span data-stu-id="111a6-128">You will use the `%%configure` magic to configure the notebook to use an external package.</span></span> <span data-ttu-id="111a6-129">Zorg ervoor dat u aanroept in notitieblokken die gebruikmaken van externe pakketten, het `%%configure` magische in de eerste codecel.</span><span class="sxs-lookup"><span data-stu-id="111a6-129">In notebooks that use external packages, make sure you call the `%%configure` magic in the first code cell.</span></span> <span data-ttu-id="111a6-130">Dit zorgt ervoor dat de kernel is geconfigureerd voor gebruik van het pakket voordat de sessie wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="111a6-130">This ensures that the kernel is configured to use the package before the session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="111a6-131">Als u voor het configureren van de kernel in de eerste cel vergeet, kunt u de `%%configure` met de `-f` parameter, maar die wordt de sessie opnieuw starten en alle voortgang gaan verloren.</span><span class="sxs-lookup"><span data-stu-id="111a6-131">If you forget to configure the kernel in the first cell, you can use the `%%configure` with the `-f` parameter, but that will restart the session and all progress will be lost.</span></span>

    | <span data-ttu-id="111a6-132">HDInsight-versie</span><span class="sxs-lookup"><span data-stu-id="111a6-132">HDInsight version</span></span> | <span data-ttu-id="111a6-133">Opdracht</span><span class="sxs-lookup"><span data-stu-id="111a6-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="111a6-134">Voor HDInsight 3.3 en HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="111a6-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="111a6-135">Voor HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="111a6-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="111a6-136">Het bovenstaande fragment verwacht de maven-coördinaten voor de externe pakket in de centrale opslagplaats Maven.</span><span class="sxs-lookup"><span data-stu-id="111a6-136">The snippet above expects the maven coordinates for the external package in Maven Central Repository.</span></span> <span data-ttu-id="111a6-137">In dit fragment `com.databricks:spark-csv_2.10:1.4.0` is de maven-coördinaat voor **spark-csv** pakket.</span><span class="sxs-lookup"><span data-stu-id="111a6-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is the maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="111a6-138">Hier ziet u hoe u de coördinaten voor een pakket maken.</span><span class="sxs-lookup"><span data-stu-id="111a6-138">Here's how you construct the coordinates for a package.</span></span>
   
    <span data-ttu-id="111a6-139">a.</span><span class="sxs-lookup"><span data-stu-id="111a6-139">a.</span></span> <span data-ttu-id="111a6-140">Het pakket niet vinden in de opslagplaats met Maven.</span><span class="sxs-lookup"><span data-stu-id="111a6-140">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="111a6-141">Voor deze zelfstudie gebruiken we [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="111a6-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="111a6-142">b.</span><span class="sxs-lookup"><span data-stu-id="111a6-142">b.</span></span> <span data-ttu-id="111a6-143">Verzamel de waarden voor uit de opslagplaats **GroupId**, **artefact-id**, en **versie**.</span><span class="sxs-lookup"><span data-stu-id="111a6-143">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="111a6-144">Zorg ervoor dat de waarden die u verzamelt die overeenkomen met uw cluster.</span><span class="sxs-lookup"><span data-stu-id="111a6-144">Make sure that the values you gather match your cluster.</span></span> <span data-ttu-id="111a6-145">In dit geval gebruiken we een Scala 2.10 en Spark 1.4.0 pakket, maar mogelijk moet u verschillende versies voor de juiste Scala of Spark versie selecteren in het cluster.</span><span class="sxs-lookup"><span data-stu-id="111a6-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need to select different versions for the appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="111a6-146">U vindt hier de Scala-versie op het cluster door het uitvoeren van `scala.util.Properties.versionString` op de kernel Spark Jupyter of Spark verzenden.</span><span class="sxs-lookup"><span data-stu-id="111a6-146">You can find out the Scala version on your cluster by running `scala.util.Properties.versionString` on the Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="111a6-147">U vindt hier de Spark-versie op het cluster door het uitvoeren van `sc.version` op Jupyter-notebooks.</span><span class="sxs-lookup"><span data-stu-id="111a6-147">You can find out the Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="111a6-148">![Externe pakketten gebruiken met Jupyter-notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "externe pakketten gebruiken met Jupyter-notebook")</span><span class="sxs-lookup"><span data-stu-id="111a6-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="111a6-149">c.</span><span class="sxs-lookup"><span data-stu-id="111a6-149">c.</span></span> <span data-ttu-id="111a6-150">De drie waarden, gescheiden door een dubbele punt (**:**).</span><span class="sxs-lookup"><span data-stu-id="111a6-150">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="111a6-151">Voer de codecel met de `%%configure` verwerkt Magic-pakket.</span><span class="sxs-lookup"><span data-stu-id="111a6-151">Run the code cell with the `%%configure` magic.</span></span> <span data-ttu-id="111a6-152">Hiermee wordt de onderliggende Livy sessie configureren voor gebruik van het pakket dat u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="111a6-152">This will configure the underlying Livy session to use the package you provided.</span></span> <span data-ttu-id="111a6-153">U kunt nu het pakket gebruiken in de volgende cellen in de notebook, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="111a6-153">In the subsequent cells in the notebook, you can now use the package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="111a6-154">Vervolgens kunt u uitvoeren de codefragmenten zoals u hieronder kunt zien, om weer te geven van de gegevens van de dataframe die u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="111a6-154">You can then run the snippets, like shown below, to view the data from the dataframe you created in the previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="111a6-155"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="111a6-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="111a6-156">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="111a6-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="111a6-157">Scenario's</span><span class="sxs-lookup"><span data-stu-id="111a6-157">Scenarios</span></span>
* [<span data-ttu-id="111a6-158">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="111a6-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="111a6-159">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="111a6-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="111a6-160">Spark met Machine Learning: Spark in HDInsight gebruiken om voedselinspectieresultaten te voorspellen</span><span class="sxs-lookup"><span data-stu-id="111a6-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="111a6-161">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="111a6-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="111a6-162">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="111a6-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="111a6-163">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="111a6-163">Create and run applications</span></span>
* [<span data-ttu-id="111a6-164">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="111a6-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="111a6-165">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="111a6-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="111a6-166">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="111a6-166">Tools and extensions</span></span>

* [<span data-ttu-id="111a6-167">Externe python-pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="111a6-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="111a6-168">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om Spark Scala-toepassingen te maken en in te dienen</span><span class="sxs-lookup"><span data-stu-id="111a6-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="111a6-169">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om op afstand fouten in Spark Scala-toepassingen op te lossen</span><span class="sxs-lookup"><span data-stu-id="111a6-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="111a6-170">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="111a6-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="111a6-171">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="111a6-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="111a6-172">Jupyter op uw computer installeren en verbinding maken met een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="111a6-172">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="111a6-173">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="111a6-173">Manage resources</span></span>
* [<span data-ttu-id="111a6-174">Resources beheren voor het Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="111a6-174">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="111a6-175">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="111a6-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

