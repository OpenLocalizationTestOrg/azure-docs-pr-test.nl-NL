---
title: aaaScript action - pakketten voor Python installeren met Jupyter op Azure HDInsight | Microsoft Docs
description: Stapsgewijze instructies over hoe toouse script actie tooconfigure Jupyter-notebooks beschikbaar met HDInsight Spark-clusters toouse externe python-pakketten.
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
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="76220-103">Scriptactie tooinstall externe Python-pakketten gebruiken voor Jupyter-notebooks in Apache Spark-clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="76220-103">Use Script Action tooinstall external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="76220-104">Met behulp van de cel verwerkt Magic-pakket</span><span class="sxs-lookup"><span data-stu-id="76220-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="76220-105">Met behulp van de scriptactie</span><span class="sxs-lookup"><span data-stu-id="76220-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="76220-106">Meer informatie over hoe toouse scriptacties tooconfigure een Apache Spark-cluster in HDInsight (Linux) toouse externe, community-hebben bijgedragen **python** pakketten die niet zijn opgenomen out-of-the-box in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="76220-106">Learn how toouse Script Actions tooconfigure an Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed **python** packages that are not included out-of-the-box in hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="76220-107">U kunt ook een Jupyter-notebook configureren met behulp van `%%configure` magic toouse externe pakketten.</span><span class="sxs-lookup"><span data-stu-id="76220-107">You can also configure a Jupyter notebook by using `%%configure` magic toouse external packages.</span></span> <span data-ttu-id="76220-108">Zie voor instructies [externe pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="76220-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="76220-109">U kunt zoeken Hallo [package index](https://pypi.python.org/pypi) voor Hallo volledige lijst met pakketten die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="76220-109">You can search hello [package index](https://pypi.python.org/pypi) for hello complete list of packages that are available.</span></span> <span data-ttu-id="76220-110">U kunt ook een lijst met beschikbare pakketten opvragen uit andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="76220-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="76220-111">Bijvoorbeeld, kunt u pakketten beschikbaar gesteld via installeren [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) of [conda smidse](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="76220-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="76220-112">In dit artikel leert u hoe tooinstall hello [TensorFlow](https://www.tensorflow.org/) van het pakket met Script Actoin op het cluster en deze gebruiken via Jupyter-notebook Hallo.</span><span class="sxs-lookup"><span data-stu-id="76220-112">In this article, you will learn how tooinstall hello [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via hello Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76220-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="76220-113">Prerequisites</span></span>
<span data-ttu-id="76220-114">U moet Hallo volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="76220-114">You must have hello following:</span></span>

* <span data-ttu-id="76220-115">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="76220-115">An Azure subscription.</span></span> <span data-ttu-id="76220-116">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="76220-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="76220-117">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76220-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="76220-118">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="76220-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="76220-119">Als u nog geen een Spark-cluster in HDInsight Linux, kunt u scriptacties uitvoeren tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="76220-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="76220-120">Ga naar Hallo-documentatie op [hoe toouse aangepaste acties script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="76220-120">Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="76220-121">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="76220-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="76220-122">Van Hallo [Azure Portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt).</span><span class="sxs-lookup"><span data-stu-id="76220-122">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="76220-123">U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.</span><span class="sxs-lookup"><span data-stu-id="76220-123">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="76220-124">Klik op Hallo blade Spark-cluster **scriptacties** onder **gebruik**.</span><span class="sxs-lookup"><span data-stu-id="76220-124">From hello Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="76220-125">Hallo aangepaste actie uitvoeren installeert die TensorFlow in de hoofdknooppunten Hallo en Hallo worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="76220-125">Run hello custom action that installs TensorFlow in hello head nodes and hello worker nodes.</span></span> <span data-ttu-id="76220-126">Hallo bash-script kan worden verwezen vanuit: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh bezoek Hallo documentatie op [hoe toouse aangepaste acties script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="76220-126">hello bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="76220-127">Er zijn twee python-installaties in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="76220-127">There are two python installations in hello cluster.</span></span> <span data-ttu-id="76220-128">Spark gebruikt Hallo Anaconda python installatie zich bevindt op `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="76220-128">Spark will use hello Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="76220-129">Met de installatie in uw aangepaste acties via verwijzen naar `/usr/bin/anaconda/bin/pip` en `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="76220-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="76220-130">Open een PySpark Jupyter-notebook</span><span class="sxs-lookup"><span data-stu-id="76220-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="76220-131">![Een nieuwe Jupyter-notebook maken](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Een nieuwe Jupyter-notebook maken")</span><span class="sxs-lookup"><span data-stu-id="76220-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="76220-132">Een nieuwe notebook gemaakt en geopend met de Hallo naam Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="76220-132">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="76220-133">Klik op Hallo notebook naam Hallo boven en een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="76220-133">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="76220-134">![Geef een naam voor de notebook Hallo](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Geef een naam voor de notebook Hallo")</span><span class="sxs-lookup"><span data-stu-id="76220-134">![Provide a name for hello notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="76220-135">U gaat nu `import tensorflow` en een Hallo wereld-voorbeeld uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="76220-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="76220-136">Code toocopy:</span><span class="sxs-lookup"><span data-stu-id="76220-136">Code toocopy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="76220-137">Hallo resultaat ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="76220-137">hello result will look like this:</span></span>
    
    <span data-ttu-id="76220-138">![De uitvoering van code TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "code TensorFlow uitvoeren")</span><span class="sxs-lookup"><span data-stu-id="76220-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="76220-139"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="76220-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="76220-140">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="76220-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="76220-141">Scenario's</span><span class="sxs-lookup"><span data-stu-id="76220-141">Scenarios</span></span>
* [<span data-ttu-id="76220-142">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="76220-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="76220-143">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="76220-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="76220-144">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="76220-144">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="76220-145">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="76220-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="76220-146">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="76220-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="76220-147">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="76220-147">Create and run applications</span></span>
* [<span data-ttu-id="76220-148">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="76220-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="76220-149">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="76220-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="76220-150">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="76220-150">Tools and extensions</span></span>
* [<span data-ttu-id="76220-151">Externe pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="76220-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="76220-152">De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="76220-152">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="76220-153">De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="76220-153">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="76220-154">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="76220-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="76220-155">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="76220-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="76220-156">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="76220-156">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="76220-157">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="76220-157">Manage resources</span></span>
* [<span data-ttu-id="76220-158">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="76220-158">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="76220-159">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="76220-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
