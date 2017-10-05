---
title: Actie - pakketten voor Python installeren met Jupyter op Azure HDInsight script | Microsoft Docs
description: Stapsgewijze instructies voor het gebruik van de scriptactie voor het configureren van Jupyter-notebooks met HDInsight Spark-clusters externe python-pakketten gebruiken.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 20cf384c96d4ff4eaf064c8880ad128d521fb9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-script-action-to-install-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="77d2d-103">Scriptactie gebruiken voor het installeren van externe Python-pakketten voor Jupyter-notebooks in Apache Spark-clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="77d2d-103">Use Script Action to install external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="77d2d-104">Met behulp van de cel verwerkt Magic-pakket</span><span class="sxs-lookup"><span data-stu-id="77d2d-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="77d2d-105">Met behulp van de scriptactie</span><span class="sxs-lookup"><span data-stu-id="77d2d-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="77d2d-106">Informatie over het gebruik van scriptacties voor het configureren van een Apache Spark-cluster in HDInsight (Linux) gebruiken van externe, community bijgedragen **python** pakketten die niet out-of-the-box opgenomen in het cluster.</span><span class="sxs-lookup"><span data-stu-id="77d2d-106">Learn how to use Script Actions to configure an Apache Spark cluster on HDInsight (Linux) to use external, community-contributed **python** packages that are not included out-of-the-box in the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="77d2d-107">U kunt ook een Jupyter-notebook configureren met behulp van `%%configure` magic externe pakketten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="77d2d-107">You can also configure a Jupyter notebook by using `%%configure` magic to use external packages.</span></span> <span data-ttu-id="77d2d-108">Zie voor instructies [externe pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="77d2d-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="77d2d-109">U kunt zoeken in de [package index](https://pypi.python.org/pypi) voor de volledige lijst met pakketten die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="77d2d-109">You can search the [package index](https://pypi.python.org/pypi) for the complete list of packages that are available.</span></span> <span data-ttu-id="77d2d-110">U kunt ook een lijst met beschikbare pakketten opvragen uit andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="77d2d-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="77d2d-111">Bijvoorbeeld, kunt u pakketten beschikbaar gesteld via installeren [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) of [conda smidse](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="77d2d-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="77d2d-112">In dit artikel leert u hoe u installeert de [TensorFlow](https://www.tensorflow.org/) van het pakket met Script Actoin op het cluster en wordt via de Jupyter-notebook gebruikt.</span><span class="sxs-lookup"><span data-stu-id="77d2d-112">In this article, you will learn how to install the [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via the Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77d2d-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="77d2d-113">Prerequisites</span></span>
<span data-ttu-id="77d2d-114">U hebt het volgende:</span><span class="sxs-lookup"><span data-stu-id="77d2d-114">You must have the following:</span></span>

* <span data-ttu-id="77d2d-115">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="77d2d-115">An Azure subscription.</span></span> <span data-ttu-id="77d2d-116">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="77d2d-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="77d2d-117">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77d2d-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="77d2d-118">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="77d2d-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="77d2d-119">Als u nog geen een Spark-cluster in HDInsight Linux, kunt u scriptacties uitvoeren tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="77d2d-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="77d2d-120">Ga naar de documentatie op [het gebruik van aangepaste scriptacties](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="77d2d-120">Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="77d2d-121">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="77d2d-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="77d2d-122">Klik vanuit de [Azure Portal](https://portal.azure.com/), vanaf het startboard, op de tegel voor uw Spark-cluster (als u deze aan het startboard hebt vastgemaakt).</span><span class="sxs-lookup"><span data-stu-id="77d2d-122">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="77d2d-123">U kunt ook naar uw cluster navigeren onder **Bladeren** > **HDInsight-clusters**.</span><span class="sxs-lookup"><span data-stu-id="77d2d-123">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="77d2d-124">Klik in de blade Spark-cluster op **scriptacties** onder **gebruik**.</span><span class="sxs-lookup"><span data-stu-id="77d2d-124">From the Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="77d2d-125">De aangepaste actie uitgevoerd installeert die TensorFlow in de hoofdknooppunten en worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="77d2d-125">Run the custom action that installs TensorFlow in the head nodes and the worker nodes.</span></span> <span data-ttu-id="77d2d-126">Het script bash kan worden verwezen vanuit: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh gaat u naar de documentatie op [het gebruik van aangepaste scriptacties](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="77d2d-126">The bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="77d2d-127">Er zijn twee python-installaties in het cluster.</span><span class="sxs-lookup"><span data-stu-id="77d2d-127">There are two python installations in the cluster.</span></span> <span data-ttu-id="77d2d-128">Spark gebruikt de Anaconda python-installatie zich bevindt op `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="77d2d-128">Spark will use the Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="77d2d-129">Met de installatie in uw aangepaste acties via verwijzen naar `/usr/bin/anaconda/bin/pip` en `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="77d2d-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="77d2d-130">Open een PySpark Jupyter-notebook</span><span class="sxs-lookup"><span data-stu-id="77d2d-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="77d2d-131">![Een nieuwe Jupyter-notebook maken](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Een nieuwe Jupyter-notebook maken")</span><span class="sxs-lookup"><span data-stu-id="77d2d-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="77d2d-132">Er wordt een nieuwe notebook gemaakt en geopend met de naam Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="77d2d-132">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="77d2d-133">Klik bovenaan op de naam van de notebook en wijzig deze in een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="77d2d-133">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="77d2d-134">![Een naam opgeven voor de notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Een naam opgeven voor de notebook")</span><span class="sxs-lookup"><span data-stu-id="77d2d-134">![Provide a name for the notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="77d2d-135">U gaat nu `import tensorflow` en een Hallo wereld-voorbeeld uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="77d2d-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="77d2d-136">Code kopiëren:</span><span class="sxs-lookup"><span data-stu-id="77d2d-136">Code to copy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="77d2d-137">Het resultaat ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="77d2d-137">The result will look like this:</span></span>
    
    <span data-ttu-id="77d2d-138">![De uitvoering van code TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "code TensorFlow uitvoeren")</span><span class="sxs-lookup"><span data-stu-id="77d2d-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="77d2d-139"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="77d2d-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="77d2d-140">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="77d2d-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="77d2d-141">Scenario's</span><span class="sxs-lookup"><span data-stu-id="77d2d-141">Scenarios</span></span>
* [<span data-ttu-id="77d2d-142">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="77d2d-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="77d2d-143">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="77d2d-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="77d2d-144">Spark met Machine Learning: Spark in HDInsight gebruiken om voedselinspectieresultaten te voorspellen</span><span class="sxs-lookup"><span data-stu-id="77d2d-144">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="77d2d-145">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="77d2d-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="77d2d-146">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="77d2d-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="77d2d-147">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="77d2d-147">Create and run applications</span></span>
* [<span data-ttu-id="77d2d-148">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="77d2d-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="77d2d-149">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="77d2d-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="77d2d-150">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="77d2d-150">Tools and extensions</span></span>
* [<span data-ttu-id="77d2d-151">Externe pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="77d2d-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="77d2d-152">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om Spark Scala-toepassingen te maken en in te dienen</span><span class="sxs-lookup"><span data-stu-id="77d2d-152">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="77d2d-153">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om op afstand fouten in Spark Scala-toepassingen op te lossen</span><span class="sxs-lookup"><span data-stu-id="77d2d-153">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="77d2d-154">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="77d2d-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="77d2d-155">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="77d2d-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="77d2d-156">Jupyter op uw computer installeren en verbinding maken met een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="77d2d-156">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="77d2d-157">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="77d2d-157">Manage resources</span></span>
* [<span data-ttu-id="77d2d-158">Resources beheren voor het Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="77d2d-158">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="77d2d-159">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="77d2d-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
