---
title: Microsoft cognitieve Toolkit met Azure HDInsight Spark voor grondige learning | Microsoft Docs
description: Meer informatie over hoe een getraind Microsoft cognitieve Toolkit grondige learning-model kan worden toegepast op een gegevensset met de API van de Python Spark in Azure HDInsight Spark-cluster.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: fafd738f782660b824732bab8cc3bec8405947e7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="c4749-103">Gebruik Microsoft cognitieve Toolkit grondige learning-model met Azure HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="c4749-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="c4749-104">In dit artikel leert uitvoeren u de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="c4749-104">In this article, you do the following steps.</span></span>

1. <span data-ttu-id="c4749-105">Voer een aangepast script voor het installeren van Microsoft cognitieve Toolkit op een Azure HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="c4749-105">Run a custom script to install Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="c4749-106">Een Jupyter-notebook uploaden naar het Spark-cluster om te zien hoe een getraind Microsoft cognitieve Toolkit grondige learning-model toepassen op bestanden in een Azure Blob Storage-Account met behulp van de [Spark Python-API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="c4749-106">Upload a Jupyter notebook to the Spark cluster to see how to apply a trained Microsoft Cognitive Toolkit deep learning model to files in an Azure Blob Storage Account using the [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4749-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c4749-107">Prerequisites</span></span>

* <span data-ttu-id="c4749-108">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="c4749-108">**An Azure subscription**.</span></span> <span data-ttu-id="c4749-109">Voordat u met deze zelfstudie begint, moet u een Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="c4749-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="c4749-110">Zie [Maak vandaag nog uw gratis Azure-account](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="c4749-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="c4749-111">**Azure HDInsight Spark-cluster**.</span><span class="sxs-lookup"><span data-stu-id="c4749-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="c4749-112">Voor dit artikel, een 2.0 Spark-cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="c4749-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="c4749-113">Zie voor instructies [maken Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="c4749-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="c4749-114">Hoe deze oplossing stromen</span><span class="sxs-lookup"><span data-stu-id="c4749-114">How does this solution flow?</span></span>

<span data-ttu-id="c4749-115">Deze oplossing wordt verdeeld over dit artikel en een Jupyter-notebook die u als onderdeel van deze zelfstudie uploadt.</span><span class="sxs-lookup"><span data-stu-id="c4749-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="c4749-116">In dit artikel leert uitvoeren u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c4749-116">In this article, you complete the following steps:</span></span>

* <span data-ttu-id="c4749-117">Een scriptactie uitgevoerd op een HDInsight Spark-cluster om Microsoft cognitieve Toolkit en Python-pakketten te installeren.</span><span class="sxs-lookup"><span data-stu-id="c4749-117">Run a script action on an HDInsight Spark cluster to install Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="c4749-118">Upload de Jupyter-notebook dat wordt uitgevoerd van de oplossing met HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="c4749-118">Upload the Jupyter notebook that runs the solution to the HDInsight Spark cluster.</span></span>

<span data-ttu-id="c4749-119">De volgende overige stappen worden in de Jupyter-notebook besproken.</span><span class="sxs-lookup"><span data-stu-id="c4749-119">The following remaining steps are covered in the Jupyter notebook.</span></span>

- <span data-ttu-id="c4749-120">Installatiekopieën van het voorbeeld in een Spark Resiliant gedistribueerd gegevensset of RDD geladen</span><span class="sxs-lookup"><span data-stu-id="c4749-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="c4749-121">Laden van modules en standaardinstellingen definiëren</span><span class="sxs-lookup"><span data-stu-id="c4749-121">Load modules and define presets</span></span>
   - <span data-ttu-id="c4749-122">Downloaden van de gegevensset lokaal op het Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="c4749-122">Download the dataset locally on the Spark cluster</span></span>
   - <span data-ttu-id="c4749-123">De gegevensset converteren naar een RDD</span><span class="sxs-lookup"><span data-stu-id="c4749-123">Convert the dataset into an RDD</span></span>
- <span data-ttu-id="c4749-124">De afbeeldingen met een getraind cognitieve Toolkit model beoordelen</span><span class="sxs-lookup"><span data-stu-id="c4749-124">Score the images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="c4749-125">Het getrainde model voor cognitieve Toolkit downloaden naar het Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="c4749-125">Download the trained Cognitive Toolkit model to the Spark cluster</span></span>
   - <span data-ttu-id="c4749-126">Definieer functies kunnen worden gebruikt door de worker-knooppunten</span><span class="sxs-lookup"><span data-stu-id="c4749-126">Define functions to be used by worker nodes</span></span>
   - <span data-ttu-id="c4749-127">Score van de installatiekopieën op de worker-knooppunten</span><span class="sxs-lookup"><span data-stu-id="c4749-127">Score the images on worker nodes</span></span>
   - <span data-ttu-id="c4749-128">De nauwkeurigheid model evalueren</span><span class="sxs-lookup"><span data-stu-id="c4749-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="c4749-129">Microsoft cognitieve Toolkit installeren</span><span class="sxs-lookup"><span data-stu-id="c4749-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="c4749-130">U kunt Microsoft cognitieve Toolkit installeren op een Spark-cluster met behulp van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="c4749-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="c4749-131">Scriptactie maakt gebruik van aangepaste scripts om onderdelen te installeren op het cluster die niet standaard beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="c4749-131">Script action uses custom scripts to install components on the cluster that are not available by default.</span></span> <span data-ttu-id="c4749-132">U kunt de aangepaste scripts vanuit de Azure-Portal met behulp van HDInsight .NET SDK of met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4749-132">You can use the custom script from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="c4749-133">U kunt het script ook gebruiken voor het installeren van de toolkit als onderdeel van het maken van het cluster, of nadat het cluster actief is.</span><span class="sxs-lookup"><span data-stu-id="c4749-133">You can also use the script to install the toolkit either as part of cluster creation, or after the cluster is up and running.</span></span> 

<span data-ttu-id="c4749-134">In dit artikel gebruiken we de portal voor het installeren van de toolkit nadat het cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4749-134">In this article, we use the portal to install the toolkit, after the cluster has been created.</span></span> <span data-ttu-id="c4749-135">Zie voor andere manieren om uit te voeren van het aangepaste script [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c4749-135">For other ways to run the custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="c4749-136">Azure Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="c4749-136">Using the Azure Portal</span></span>

<span data-ttu-id="c4749-137">Zie voor instructies over het gebruik van de Azure Portal om uit te voeren scriptactie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="c4749-137">For instructions on how to use the Azure Portal to run script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="c4749-138">Zorg ervoor dat u het volgende invoeren voor het installeren van Microsoft cognitieve Toolkit opgeven.</span><span class="sxs-lookup"><span data-stu-id="c4749-138">Make sure you provide the following inputs to install Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="c4749-139">Geef een waarde voor de naam van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="c4749-139">Provide a value for the script action name.</span></span>

* <span data-ttu-id="c4749-140">Voor **Bash script URI**, voer `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="c4749-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="c4749-141">Zorg ervoor dat u het script uitvoert op de hoofd- en werkrollen knooppunten alleen en schakel de selectievakjes.</span><span class="sxs-lookup"><span data-stu-id="c4749-141">Make sure you run the script only on the head and worker nodes and clear all the other checkboxes.</span></span>

* <span data-ttu-id="c4749-142">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4749-142">Click **Create**.</span></span>

## <a name="upload-the-jupyter-notebook-to-azure-hdinsight-spark-cluster"></a><span data-ttu-id="c4749-143">De Jupyter-notebook uploaden naar Azure HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="c4749-143">Upload the Jupyter notebook to Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="c4749-144">Voor het gebruik van de Microsoft cognitieve Toolkit met het Azure HDInsight Spark-cluster, moet u de Jupyter-notebook laden **CNTK_model_scoring_on_Spark_walkthrough.ipynb** aan het Azure HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="c4749-144">To use the Microsoft Cognitive Toolkit with the Azure HDInsight Spark cluster, you must load the Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** to the Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="c4749-145">Deze laptop is beschikbaar op GitHub op [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="c4749-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="c4749-146">Kloon de GitHub-opslagplaats [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="c4749-146">Clone the GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="c4749-147">Zie voor instructies voor het klonen [een opslagplaats klonen](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="c4749-147">For instructions to clone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="c4749-148">Open de blade Spark-cluster dat u al ingericht, klikt u op in de Azure-Portal **Cluster-Dashboard**, en klik vervolgens op **Jupyter-notebook**.</span><span class="sxs-lookup"><span data-stu-id="c4749-148">From the Azure Portal, open the Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="c4749-149">U kunt ook de Jupyter-notebook starten door te gaan naar de URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="c4749-149">You can also launch the Jupyter notebook by going to the URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="c4749-150">Vervang \<clustername > met de naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="c4749-150">Replace \<clustername> with the name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="c4749-151">Klik op de Jupyter-notebook **uploaden** in de rechterbovenhoek hoek en navigeer vervolgens naar de locatie waar u de GitHub-opslagplaats gekloond.</span><span class="sxs-lookup"><span data-stu-id="c4749-151">From the Jupyter notebook, click **Upload** in the top-right corner and then navigate to the location where you cloned the GitHub repository.</span></span>

    <span data-ttu-id="c4749-152">![Jupyter-notebook uploaden naar Azure HDInsight Spark-cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "uploaden Jupyter-notebook met Azure HDInsight Spark-cluster")</span><span class="sxs-lookup"><span data-stu-id="c4749-152">![Upload Jupyter notebook to Azure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="c4749-153">Klik op **uploaden** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c4749-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="c4749-154">Nadat de laptop is geüpload, klikt u op de naam van de notebook en volg de instructies in de notebook zelf voor het laden van de gegevensset en het uitvoeren van de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c4749-154">After the notebook is uploaded, click the name of the notebook and then follow the instructions in the notebook itself on how to load the data set and perform the tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="c4749-155">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c4749-155">See also</span></span>
* [<span data-ttu-id="c4749-156">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4749-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="c4749-157">Scenario's</span><span class="sxs-lookup"><span data-stu-id="c4749-157">Scenarios</span></span>
* [<span data-ttu-id="c4749-158">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="c4749-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c4749-159">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="c4749-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c4749-160">Spark met Machine Learning: Spark in HDInsight gebruiken om voedselinspectieresultaten te voorspellen</span><span class="sxs-lookup"><span data-stu-id="c4749-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c4749-161">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="c4749-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="c4749-162">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4749-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="c4749-163">Analyse van Application Insights-telemetriegegevens met behulp van Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4749-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="c4749-164">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c4749-164">Create and run applications</span></span>
* [<span data-ttu-id="c4749-165">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="c4749-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c4749-166">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="c4749-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c4749-167">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="c4749-167">Tools and extensions</span></span>
* [<span data-ttu-id="c4749-168">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om Spark Scala-toepassingen te maken en in te dienen</span><span class="sxs-lookup"><span data-stu-id="c4749-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c4749-169">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om op afstand fouten in Spark Scala-toepassingen op te lossen</span><span class="sxs-lookup"><span data-stu-id="c4749-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c4749-170">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4749-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="c4749-171">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4749-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c4749-172">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="c4749-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="c4749-173">Jupyter op uw computer installeren en verbinding maken met een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="c4749-173">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="c4749-174">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="c4749-174">Manage resources</span></span>
* [<span data-ttu-id="c4749-175">Resources beheren voor het Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4749-175">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="c4749-176">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="c4749-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
