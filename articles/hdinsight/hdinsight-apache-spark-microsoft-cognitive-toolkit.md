---
title: aaaMicrosoft cognitieve Toolkit met Azure HDInsight Spark voor grondige learning | Microsoft Docs
description: Meer informatie over hoe een getraind Microsoft cognitieve Toolkit grondige learning-model kan worden toegepast tooa gegevensset met Hallo Spark Python API in een Azure HDInsight Spark-cluster.
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
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="e2906-103">Gebruik Microsoft cognitieve Toolkit grondige learning-model met Azure HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="e2906-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="e2906-104">In dit artikel, u Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="e2906-104">In this article, you do hello following steps.</span></span>

1. <span data-ttu-id="e2906-105">Een aangepast script tooinstall Microsoft cognitieve Toolkit uitvoeren op een Azure HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="e2906-105">Run a custom script tooinstall Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="e2906-106">Het uploaden van een Jupyter-notebook toohello Spark-cluster toosee tooapply een getraind Microsoft cognitieve Toolkit grondige learning-model toofiles in een Azure Blob Storage-Account met behulp van Hallo [Spark Python-API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="e2906-106">Upload a Jupyter notebook toohello Spark cluster toosee how tooapply a trained Microsoft Cognitive Toolkit deep learning model toofiles in an Azure Blob Storage Account using hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2906-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e2906-107">Prerequisites</span></span>

* <span data-ttu-id="e2906-108">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="e2906-108">**An Azure subscription**.</span></span> <span data-ttu-id="e2906-109">Voordat u met deze zelfstudie begint, moet u een Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="e2906-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="e2906-110">Zie [Maak vandaag nog uw gratis Azure-account](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="e2906-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="e2906-111">**Azure HDInsight Spark-cluster**.</span><span class="sxs-lookup"><span data-stu-id="e2906-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="e2906-112">Voor dit artikel, een 2.0 Spark-cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="e2906-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="e2906-113">Zie voor instructies [maken Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e2906-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="e2906-114">Hoe deze oplossing stromen</span><span class="sxs-lookup"><span data-stu-id="e2906-114">How does this solution flow?</span></span>

<span data-ttu-id="e2906-115">Deze oplossing wordt verdeeld over dit artikel en een Jupyter-notebook die u als onderdeel van deze zelfstudie uploadt.</span><span class="sxs-lookup"><span data-stu-id="e2906-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="e2906-116">In dit artikel kunt u Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e2906-116">In this article, you complete hello following steps:</span></span>

* <span data-ttu-id="e2906-117">Een scriptactie uitvoeren op een HDInsight Spark-cluster tooinstall Microsoft cognitieve Toolkit en Python-pakketten.</span><span class="sxs-lookup"><span data-stu-id="e2906-117">Run a script action on an HDInsight Spark cluster tooinstall Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="e2906-118">Upload Hallo Jupyter-notebook die Hallo oplossing toohello HDInsight Spark-cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e2906-118">Upload hello Jupyter notebook that runs hello solution toohello HDInsight Spark cluster.</span></span>

<span data-ttu-id="e2906-119">Hallo worden volgende resterende stappen behandeld in Hallo Jupyter-notebook.</span><span class="sxs-lookup"><span data-stu-id="e2906-119">hello following remaining steps are covered in hello Jupyter notebook.</span></span>

- <span data-ttu-id="e2906-120">Installatiekopieën van het voorbeeld in een Spark Resiliant gedistribueerd gegevensset of RDD geladen</span><span class="sxs-lookup"><span data-stu-id="e2906-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="e2906-121">Laden van modules en standaardinstellingen definiëren</span><span class="sxs-lookup"><span data-stu-id="e2906-121">Load modules and define presets</span></span>
   - <span data-ttu-id="e2906-122">Hallo gegevensset lokaal op Hallo Spark-cluster downloaden</span><span class="sxs-lookup"><span data-stu-id="e2906-122">Download hello dataset locally on hello Spark cluster</span></span>
   - <span data-ttu-id="e2906-123">Hallo gegevensset converteren naar een RDD</span><span class="sxs-lookup"><span data-stu-id="e2906-123">Convert hello dataset into an RDD</span></span>
- <span data-ttu-id="e2906-124">Hallo afbeeldingen met een getraind cognitieve Toolkit model beoordelen</span><span class="sxs-lookup"><span data-stu-id="e2906-124">Score hello images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="e2906-125">Hallo getraind cognitieve Toolkit model toohello Spark-cluster downloaden</span><span class="sxs-lookup"><span data-stu-id="e2906-125">Download hello trained Cognitive Toolkit model toohello Spark cluster</span></span>
   - <span data-ttu-id="e2906-126">Functies toobe die wordt gebruikt door de worker-knooppunten definiëren</span><span class="sxs-lookup"><span data-stu-id="e2906-126">Define functions toobe used by worker nodes</span></span>
   - <span data-ttu-id="e2906-127">Score Hallo afbeeldingen op de worker-knooppunten</span><span class="sxs-lookup"><span data-stu-id="e2906-127">Score hello images on worker nodes</span></span>
   - <span data-ttu-id="e2906-128">De nauwkeurigheid model evalueren</span><span class="sxs-lookup"><span data-stu-id="e2906-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="e2906-129">Microsoft cognitieve Toolkit installeren</span><span class="sxs-lookup"><span data-stu-id="e2906-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="e2906-130">U kunt Microsoft cognitieve Toolkit installeren op een Spark-cluster met behulp van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="e2906-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="e2906-131">Scriptactie gebruikmaakt van aangepaste scripts tooinstall onderdelen op Hallo cluster die niet standaard beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="e2906-131">Script action uses custom scripts tooinstall components on hello cluster that are not available by default.</span></span> <span data-ttu-id="e2906-132">Kunt u aangepast script Hallo van hello Azure-Portal met behulp van HDInsight .NET SDK of met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2906-132">You can use hello custom script from hello Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="e2906-133">U kunt ook als onderdeel van het maken van het cluster, of nadat Hallo-cluster is actief en werkend Hallo script tooinstall Hallo toolkit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e2906-133">You can also use hello script tooinstall hello toolkit either as part of cluster creation, or after hello cluster is up and running.</span></span> 

<span data-ttu-id="e2906-134">In dit artikel gebruiken we Hallo portal tooinstall Hallo toolkit nadat Hallo-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2906-134">In this article, we use hello portal tooinstall hello toolkit, after hello cluster has been created.</span></span> <span data-ttu-id="e2906-135">Zie voor andere manieren toorun Hallo aangepast script, [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e2906-135">For other ways toorun hello custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="e2906-136">Met behulp van hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e2906-136">Using hello Azure Portal</span></span>

<span data-ttu-id="e2906-137">Zie voor instructies over hoe toouse hello Azure Portal toorun actie script, [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="e2906-137">For instructions on how toouse hello Azure Portal toorun script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="e2906-138">Zorg ervoor dat u na invoer tooinstall Microsoft cognitieve Toolkit Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="e2906-138">Make sure you provide hello following inputs tooinstall Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="e2906-139">Geef een waarde voor actienaam Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="e2906-139">Provide a value for hello script action name.</span></span>

* <span data-ttu-id="e2906-140">Voor **Bash script URI**, voer `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="e2906-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="e2906-141">Controleer of u Hallo script alleen uitvoeren op Hallo hoofd- en werkrollen knooppunten en wis alle andere selectievakjes Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2906-141">Make sure you run hello script only on hello head and worker nodes and clear all hello other checkboxes.</span></span>

* <span data-ttu-id="e2906-142">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e2906-142">Click **Create**.</span></span>

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a><span data-ttu-id="e2906-143">Hallo Jupyter-notebook tooAzure HDInsight Spark-cluster uploaden</span><span class="sxs-lookup"><span data-stu-id="e2906-143">Upload hello Jupyter notebook tooAzure HDInsight Spark cluster</span></span>

<span data-ttu-id="e2906-144">toouse hello Microsoft cognitieve Toolkit met hello Azure HDInsight Spark-cluster, moet u de Jupyter-notebook Hallo laden **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="e2906-144">toouse hello Microsoft Cognitive Toolkit with hello Azure HDInsight Spark cluster, you must load hello Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="e2906-145">Deze laptop is beschikbaar op GitHub op [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="e2906-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="e2906-146">Kloon Hallo GitHub-opslagplaats [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="e2906-146">Clone hello GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="e2906-147">Zie voor instructies tooclone, [een opslagplaats klonen](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="e2906-147">For instructions tooclone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="e2906-148">Open in hello Azure Portal, Hallo blade Spark-cluster dat u al ingericht, klikt u op **Cluster-Dashboard**, en klik vervolgens op **Jupyter-notebook**.</span><span class="sxs-lookup"><span data-stu-id="e2906-148">From hello Azure Portal, open hello Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="e2906-149">U kunt ook Hallo Jupyter-notebook starten door te gaan toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="e2906-149">You can also launch hello Jupyter notebook by going toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="e2906-150">Vervang \<clustername > Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e2906-150">Replace \<clustername> with hello name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="e2906-151">Hallo Jupyter-notebook, klik op **uploaden** in Hallo rechterbovenhoek en navigeer vervolgens toohello locatie waar u de GitHub-opslagplaats Hallo gekloond.</span><span class="sxs-lookup"><span data-stu-id="e2906-151">From hello Jupyter notebook, click **Upload** in hello top-right corner and then navigate toohello location where you cloned hello GitHub repository.</span></span>

    <span data-ttu-id="e2906-152">![Uploaden van Jupyter-notebook tooAzure HDInsight Spark-cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "uploaden Jupyter-notebook tooAzure HDInsight Spark-cluster")</span><span class="sxs-lookup"><span data-stu-id="e2906-152">![Upload Jupyter notebook tooAzure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook tooAzure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="e2906-153">Klik op **uploaden** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e2906-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="e2906-154">Nadat de notebook Hallo is geüpload, klikt u op de naam Hallo van Hallo laptop en volg Hallo-instructies in het Hallo-notebook zelf op hoe tooload Hallo gegevensset en Hallo zelfstudie uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e2906-154">After hello notebook is uploaded, click hello name of hello notebook and then follow hello instructions in hello notebook itself on how tooload hello data set and perform hello tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="e2906-155">Zie ook</span><span class="sxs-lookup"><span data-stu-id="e2906-155">See also</span></span>
* [<span data-ttu-id="e2906-156">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2906-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="e2906-157">Scenario's</span><span class="sxs-lookup"><span data-stu-id="e2906-157">Scenarios</span></span>
* [<span data-ttu-id="e2906-158">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="e2906-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e2906-159">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="e2906-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="e2906-160">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="e2906-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e2906-161">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="e2906-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="e2906-162">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2906-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="e2906-163">Analyse van Application Insights-telemetriegegevens met behulp van Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2906-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="e2906-164">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e2906-164">Create and run applications</span></span>
* [<span data-ttu-id="e2906-165">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="e2906-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e2906-166">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="e2906-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="e2906-167">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="e2906-167">Tools and extensions</span></span>
* [<span data-ttu-id="e2906-168">De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="e2906-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e2906-169">De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="e2906-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="e2906-170">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2906-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="e2906-171">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2906-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e2906-172">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="e2906-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="e2906-173">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="e2906-173">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="e2906-174">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="e2906-174">Manage resources</span></span>
* [<span data-ttu-id="e2906-175">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2906-175">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e2906-176">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="e2906-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
