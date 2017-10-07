---
title: aangepaste Maven-pakketten aaaUse met Jupyter in Spark op Azure HDInsight | Microsoft Docs
description: Stapsgewijze instructies over hoe tooconfigure Jupyter-notebooks beschikbaar met HDInsight Spark-clusters toouse aangepaste Maven-pakketten.
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
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="6b475-103">Externe pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b475-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b475-104">Met behulp van de cel verwerkt Magic-pakket</span><span class="sxs-lookup"><span data-stu-id="6b475-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="6b475-105">Met behulp van de scriptactie</span><span class="sxs-lookup"><span data-stu-id="6b475-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="6b475-106">Meer informatie over hoe tooconfigure een Jupyter-notebook in Apache Spark-cluster in HDInsight toouse externe, community-hebben bijgedragen **maven** pakketten die niet zijn opgenomen out-of-the-box in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6b475-106">Learn how tooconfigure a Jupyter notebook in Apache Spark cluster on HDInsight toouse external, community-contributed **maven** packages that are not included out-of-the-box in hello cluster.</span></span> 

<span data-ttu-id="6b475-107">U kunt zoeken Hallo [Maven opslagplaats](http://search.maven.org/) voor Hallo volledige lijst met pakketten die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="6b475-107">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="6b475-108">U kunt ook een lijst met beschikbare pakketten opvragen uit andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="6b475-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="6b475-109">Bijvoorbeeld, een volledige lijst met pakketten community bijgedragen is beschikbaar op [Spark pakketten](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="6b475-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="6b475-110">In dit artikel leert u hoe toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakket met de Jupyter-notebook Hallo.</span><span class="sxs-lookup"><span data-stu-id="6b475-110">In this article, you will learn how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="6b475-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6b475-111">Prerequisites</span></span>
<span data-ttu-id="6b475-112">U moet Hallo volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="6b475-112">You must have hello following:</span></span>

* <span data-ttu-id="6b475-113">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6b475-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="6b475-114">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="6b475-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="6b475-115">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="6b475-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="6b475-116">Van Hallo [Azure Portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt).</span><span class="sxs-lookup"><span data-stu-id="6b475-116">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="6b475-117">U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.</span><span class="sxs-lookup"><span data-stu-id="6b475-117">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="6b475-118">Klik vanuit Hallo blade Spark-cluster op **snelkoppelingen**, en klik vervolgens vanuit Hallo **Cluster-Dashboard** blade klikt u op **Jupyter-Notebook**.</span><span class="sxs-lookup"><span data-stu-id="6b475-118">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="6b475-119">Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6b475-119">If prompted, enter hello admin credentials for hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b475-120">U mogelijk ook Hallo Jupyter-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="6b475-120">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="6b475-121">Vervang **CLUSTERNAME** met Hallo-naam van het cluster:</span><span class="sxs-lookup"><span data-stu-id="6b475-121">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="6b475-122">Maak een nieuwe notebook.</span><span class="sxs-lookup"><span data-stu-id="6b475-122">Create a new notebook.</span></span> <span data-ttu-id="6b475-123">Klik op **nieuw**, en klik vervolgens op **Spark**.</span><span class="sxs-lookup"><span data-stu-id="6b475-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="6b475-124">![Een nieuwe Jupyter-notebook maken](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Een nieuwe Jupyter-notebook maken")</span><span class="sxs-lookup"><span data-stu-id="6b475-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="6b475-125">Een nieuwe notebook gemaakt en geopend met de Hallo naam Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="6b475-125">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="6b475-126">Klik op Hallo notebook naam Hallo boven en een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="6b475-126">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="6b475-127">![Geef een naam voor de notebook Hallo](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Geef een naam voor de notebook Hallo")</span><span class="sxs-lookup"><span data-stu-id="6b475-127">![Provide a name for hello notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="6b475-128">U gebruikt Hallo `%%configure` magische tooconfigure Hallo notebook toouse een externe-pakket.</span><span class="sxs-lookup"><span data-stu-id="6b475-128">You will use hello `%%configure` magic tooconfigure hello notebook toouse an external package.</span></span> <span data-ttu-id="6b475-129">Zorg ervoor dat u Hallo aanroepen in notitieblokken die gebruikmaken van externe pakketten, `%%configure` magische in de eerste codecel Hallo.</span><span class="sxs-lookup"><span data-stu-id="6b475-129">In notebooks that use external packages, make sure you call hello `%%configure` magic in hello first code cell.</span></span> <span data-ttu-id="6b475-130">Dit zorgt ervoor dat kernel Hallo geconfigureerde toouse Hallo pakket voordat het Hallo-sessie gestart.</span><span class="sxs-lookup"><span data-stu-id="6b475-130">This ensures that hello kernel is configured toouse hello package before hello session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="6b475-131">Als u tooconfigure Hallo kernel in de eerste cel Hallo vergeet, kunt u Hallo `%%configure` Hello `-f` parameter, maar die wordt opnieuw opgestart Hallo-sessie en voortgang van alle gaan verloren.</span><span class="sxs-lookup"><span data-stu-id="6b475-131">If you forget tooconfigure hello kernel in hello first cell, you can use hello `%%configure` with hello `-f` parameter, but that will restart hello session and all progress will be lost.</span></span>

    | <span data-ttu-id="6b475-132">HDInsight-versie</span><span class="sxs-lookup"><span data-stu-id="6b475-132">HDInsight version</span></span> | <span data-ttu-id="6b475-133">Opdracht</span><span class="sxs-lookup"><span data-stu-id="6b475-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="6b475-134">Voor HDInsight 3.3 en HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="6b475-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="6b475-135">Voor HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="6b475-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="6b475-136">Hallo codefragment hierboven verwacht Hallo maven-coördinaten voor een externe Hallo-pakket in de centrale opslagplaats Maven.</span><span class="sxs-lookup"><span data-stu-id="6b475-136">hello snippet above expects hello maven coordinates for hello external package in Maven Central Repository.</span></span> <span data-ttu-id="6b475-137">In dit fragment `com.databricks:spark-csv_2.10:1.4.0` hello maven-coördinaat voor **spark-csv** pakket.</span><span class="sxs-lookup"><span data-stu-id="6b475-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is hello maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="6b475-138">Hier ziet u hoe u Hallo-coördinaten voor een pakket maken.</span><span class="sxs-lookup"><span data-stu-id="6b475-138">Here's how you construct hello coordinates for a package.</span></span>
   
    <span data-ttu-id="6b475-139">a.</span><span class="sxs-lookup"><span data-stu-id="6b475-139">a.</span></span> <span data-ttu-id="6b475-140">Hallo-pakket niet vinden in Hallo Maven-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6b475-140">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="6b475-141">Voor deze zelfstudie gebruiken we [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="6b475-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="6b475-142">b.</span><span class="sxs-lookup"><span data-stu-id="6b475-142">b.</span></span> <span data-ttu-id="6b475-143">Verzamel uit de opslagplaats hello, Hallo waarden voor **GroupId**, **artefact-id**, en **versie**.</span><span class="sxs-lookup"><span data-stu-id="6b475-143">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="6b475-144">Zorg ervoor dat u verzamelen Hallo-waarden overeenkomen met uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6b475-144">Make sure that hello values you gather match your cluster.</span></span> <span data-ttu-id="6b475-145">In dit geval gebruiken we een Scala 2.10 en Spark 1.4.0 pakket, maar mogelijk moet u verschillende versies van tooselect voor de juiste Scala of Spark versie Hallo in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6b475-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need tooselect different versions for hello appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="6b475-146">U vindt hier Hallo Scala versie op het cluster door het uitvoeren van `scala.util.Properties.versionString` op Hallo Spark Jupyter kernel of Spark verzenden.</span><span class="sxs-lookup"><span data-stu-id="6b475-146">You can find out hello Scala version on your cluster by running `scala.util.Properties.versionString` on hello Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="6b475-147">U vindt hier Hallo Spark versie op het cluster door het uitvoeren van `sc.version` op Jupyter-notebooks.</span><span class="sxs-lookup"><span data-stu-id="6b475-147">You can find out hello Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="6b475-148">![Externe pakketten gebruiken met Jupyter-notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "externe pakketten gebruiken met Jupyter-notebook")</span><span class="sxs-lookup"><span data-stu-id="6b475-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="6b475-149">c.</span><span class="sxs-lookup"><span data-stu-id="6b475-149">c.</span></span> <span data-ttu-id="6b475-150">Samenvoegen van Hallo drie waarden, gescheiden door een dubbele punt (**:**).</span><span class="sxs-lookup"><span data-stu-id="6b475-150">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="6b475-151">Hallo codecel uitvoeren met Hallo `%%configure` verwerkt Magic-pakket.</span><span class="sxs-lookup"><span data-stu-id="6b475-151">Run hello code cell with hello `%%configure` magic.</span></span> <span data-ttu-id="6b475-152">Dit configureert Hallo onderliggende Livy sessie toouse Hallo pakket die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6b475-152">This will configure hello underlying Livy session toouse hello package you provided.</span></span> <span data-ttu-id="6b475-153">U kunt nu Hallo-pakket gebruiken in de volgende cellen Hallo in Hallo laptop, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6b475-153">In hello subsequent cells in hello notebook, you can now use hello package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="6b475-154">Vervolgens kunt u Hallo codefragmenten uitvoeren, zoals hieronder weergegeven tooview hello gegevens van Hallo dataframe u hebt gemaakt in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="6b475-154">You can then run hello snippets, like shown below, tooview hello data from hello dataframe you created in hello previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="6b475-155"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="6b475-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="6b475-156">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b475-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="6b475-157">Scenario's</span><span class="sxs-lookup"><span data-stu-id="6b475-157">Scenarios</span></span>
* [<span data-ttu-id="6b475-158">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="6b475-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="6b475-159">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="6b475-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="6b475-160">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="6b475-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="6b475-161">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="6b475-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="6b475-162">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b475-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="6b475-163">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6b475-163">Create and run applications</span></span>
* [<span data-ttu-id="6b475-164">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="6b475-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="6b475-165">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="6b475-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="6b475-166">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="6b475-166">Tools and extensions</span></span>

* [<span data-ttu-id="6b475-167">Externe python-pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="6b475-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="6b475-168">De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="6b475-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="6b475-169">De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="6b475-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="6b475-170">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b475-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="6b475-171">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b475-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="6b475-172">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="6b475-172">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="6b475-173">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="6b475-173">Manage resources</span></span>
* [<span data-ttu-id="6b475-174">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b475-174">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="6b475-175">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="6b475-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

