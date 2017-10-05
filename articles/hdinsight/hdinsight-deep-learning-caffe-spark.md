---
title: Gebruik Caffe op Azure HDInsight Spark voor gedistribueerde grondige learning | Microsoft Docs
description: Gebruik Caffe op Azure HDInsight Spark voor gedistribueerde grondige learning
services: hdinsight
documentationcenter: 
author: xiaoyongzhu
manager: asadk
editor: cgronlun
tags: azure-portal
ms.assetid: 71dcd1ad-4cad-47ad-8a9d-dcb7fa3c2ff9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: xiaoyzhu
ms.openlocfilehash: 14b7808c9534bce3049422d6bce1e8914b2c2fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="7c7b5-103">Gebruik Caffe op Azure HDInsight Spark voor gedistribueerde grondige learning</span><span class="sxs-lookup"><span data-stu-id="7c7b5-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="7c7b5-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="7c7b5-104">Introduction</span></span>

<span data-ttu-id="7c7b5-105">Grondige learning is van invloed op alle gegevens van de gezondheidszorg voor verzending naar productie en meer.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-105">Deep learning is impacting everything from healthcare to transportation to manufacturing, and more.</span></span> <span data-ttu-id="7c7b5-106">Bedrijven schakelt grondig learning voor het oplossen van problemen met vaste, zoals [installatiekopie classificatie](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [spraakherkenning](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)erkenning object en de vertaling van de computer.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-106">Companies are turning to deep learning to solve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="7c7b5-107">Er zijn [veel populaire frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), waaronder [Microsoft cognitieve Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, enzovoort. Caffe is een van de grootste beroemdheid frameworks voor neurale netwerk wordt niet symbolische (imperatieve) en veel worden gebruikt in veel gebieden, waaronder computer vision.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of the most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="7c7b5-108">Bovendien [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combineert Caffe met Apache Spark, in welk geval diep learning gemakkelijk kan worden gebruikt op een bestaande Hadoop-cluster samen met Spark ETL pijplijnen, de complexiteit van systeem en latentie voor end-to-end learning.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="7c7b5-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) cloud alleen volledig beheerde Hadoop aangeboden met geoptimaliseerde open-source analytische clusters voor Spark, Hive, MapReduce, HBase, Storm, Kafka en R Server back-up een SLA met 99,9%.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is the only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="7c7b5-110">Al deze big data-technologieën en ISV-toepassingen zijn eenvoudig te implementeren als beheerde clusters met beveiliging en bewaking op ondernemingsniveau.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="7c7b5-111">Sommige gebruikers zijn ons vragen over het gebruik van grondige learning op HDInsight, namelijk PaaS Hadoop-product van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-111">Some users are asking us about how to use deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="7c7b5-112">Er wordt meer hebben om te delen in de toekomst, maar we willen geven een overzicht van een technische blog over het gebruik van Caffe op HDInsight Spark vandaag.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-112">We will have more to share in the future, but today we want to summarize a technical blog on how to use Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="7c7b5-113">Als u Caffe voordat hebt geïnstalleerd, ziet u dat het installeren van dit framework iets lastig is.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="7c7b5-114">In deze blog we wordt eerst te laten zien hoe installeren [Caffe op Spark](https://github.com/yahoo/CaffeOnSpark) voor een HDInsight-cluster, gebruik vervolgens de ingebouwde MNIST die demo voor demostrate grondige Learning gedistribueerd met behulp van HDInsight Spark op CPU's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-114">In this blog, we will first illustrate how to install [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use the built-in MNIST demo to demostrate how to use Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="7c7b5-115">Er zijn vier hoofdstappen downloaden werken op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-115">There are four major steps to get it work on HDInsight.</span></span>

1. <span data-ttu-id="7c7b5-116">De vereiste afhankelijkheden te installeren op alle knooppunten</span><span class="sxs-lookup"><span data-stu-id="7c7b5-116">Install the required dependencies on all the nodes</span></span>
2. <span data-ttu-id="7c7b5-117">Caffe op Spark voor HDInsight voor het hoofdknooppunt bouwen</span><span class="sxs-lookup"><span data-stu-id="7c7b5-117">Build Caffe on Spark for HDInsight on the head node</span></span>
3. <span data-ttu-id="7c7b5-118">De vereiste bibliotheken voor alle worker-knooppunten distribueren</span><span class="sxs-lookup"><span data-stu-id="7c7b5-118">Distribute the required libraries to all the worker nodes</span></span>
4. <span data-ttu-id="7c7b5-119">Een model Caffe opstellen en voer dit distributely</span><span class="sxs-lookup"><span data-stu-id="7c7b5-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="7c7b5-120">Aangezien HDInsight een PaaS-oplossing is, biedt uitstekende platformfuncties - zodat u heel gemakkelijk een aantal taken uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy to perform some tasks.</span></span> <span data-ttu-id="7c7b5-121">Een van de functies die we veel in dit blogbericht gebruiken heet [scriptactie](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), waarmee u de shell-opdrachten voor het aanpassen van de clusterknooppunten (hoofdknooppunt, werkrolknooppunt of edge-knooppunt) kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-121">One of the features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands to customize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-the-required-dependencies-on-all-the-nodes"></a><span data-ttu-id="7c7b5-122">Stap 1: De vereiste afhankelijkheden installeren op alle knooppunten</span><span class="sxs-lookup"><span data-stu-id="7c7b5-122">Step 1:  Install the required dependencies on all the nodes</span></span>

<span data-ttu-id="7c7b5-123">Om te beginnen, moet voor het installeren van de afhankelijkheden die we nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-123">To get started, we need to install the dependencies we need.</span></span> <span data-ttu-id="7c7b5-124">De site Caffe en [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) biedt sommige wiki erg nuttig zijn voor het installeren van de afhankelijkheden voor Spark op YARN-modus (dit is de modus voor HDInsight Spark), maar moeten we enkele meer afhankelijkheden voor HDInsight platform toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-124">The Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing the dependencies for Spark on YARN mode (which is the mode for HDInsight Spark), but we need to add a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="7c7b5-125">We gebruiken de scriptactie zoals hieronder en uitvoeren op alle hoofdknooppunten en worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-125">We will use the script action as below and run it on all the head nodes and worker nodes.</span></span> <span data-ttu-id="7c7b5-126">Deze scriptactie duurt ongeveer 20 minuten, zoals die afhankelijkheden is ook afhankelijk van andere pakketten zijn.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="7c7b5-127">U moet deze plaatsen op een locatie die toegankelijk is voor uw HDInsight-cluster, zoals een GitHub-locatie of de standaard BLOB storage-account.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-127">You should put it in some location that is accessible to your HDInsight cluster, such as a GitHub location or the default BLOB storage account.</span></span>

    #!/bin/bash
    #Please be aware that installing the below will add additional 20 mins to cluster creation because of the dependencies
    #installing all dependencies, including the ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all the nodes

    sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler maven libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev build-essential  libboost-all-dev python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

    #install protobuf
    wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
    sudo tar xzvf protobuf-2.5.0.tar.gz -C /tmp/
    cd /tmp/protobuf-2.5.0/
    sudo ./configure
    sudo make
    sudo make check
    sudo make install
    sudo ldconfig
    echo "protobuf installation done"


<span data-ttu-id="7c7b5-128">Er zijn twee stappen in de bovenstaande scriptactie.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-128">There are two steps in the script action above.</span></span> <span data-ttu-id="7c7b5-129">De eerste stap is het de vereiste bibliotheken installeren.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-129">The first step is to install all the required libraries.</span></span> <span data-ttu-id="7c7b5-130">Deze bibliotheken bevatten de benodigde bibliotheken voor zowel Caffe compileren (zoals gflags, glog) en het uitvoeren van Caffe (zoals numpy).</span><span class="sxs-lookup"><span data-stu-id="7c7b5-130">Those libraries include the necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="7c7b5-131">We libatlas voor CPU-optimalisatie gebruiken, maar u kunt de wiki CaffeOnSpark altijd volgen over het installeren van andere bibliotheken optimalisatie zoals MKL of CUDA (voor GPU).</span><span class="sxs-lookup"><span data-stu-id="7c7b5-131">We are using libatlas for CPU optimization, but you can always follow the CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="7c7b5-132">De tweede stap is het downloaden en protobuf 2.5.0 voor Caffe installeren tijdens de runtime worden gecompileerd.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-132">The second step is to download, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="7c7b5-133">Protobuf 2.5.0 [is vereist](https://github.com/yahoo/CaffeOnSpark/issues/87), maar deze versie niet beschikbaar als een pakket op Ubuntu 16, is dus moeten we er tijdens het compileren van de broncode.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need to compile it from the source code.</span></span> <span data-ttu-id="7c7b5-134">Er zijn ook enkele bronnen op het Internet voor het eerst compileren, zoals [dit](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="7c7b5-134">There are also a few resources on the Internet on how to compile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="7c7b5-135">Gewoon aan de slag kunt u alleen uitvoeren met deze scriptactie op basis van uw cluster voor alle worker-knooppunten en hoofdknooppunten (voor HDInsight 3.5).</span><span class="sxs-lookup"><span data-stu-id="7c7b5-135">To simply get started, you can just run this script action against your cluster to all the worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="7c7b5-136">Kunt u de scriptacties voor een actieve cluster uitvoeren of u kunt ook de scriptacties uitvoeren tijdens de periode van cluster inrichten.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-136">You can either run the script actions for a running cluster, or you can also run the script actions during the cluster provision time.</span></span> <span data-ttu-id="7c7b5-137">Zie de documentatie voor meer informatie over de scriptacties [hier](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="7c7b5-137">For more details on the script actions, please see the documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![Scriptacties afhankelijkheden installeren](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-the-head-node"></a><span data-ttu-id="7c7b5-139">Stap 2: Caffe op Spark voor HDInsight voor het hoofdknooppunt bouwen</span><span class="sxs-lookup"><span data-stu-id="7c7b5-139">Step 2: Build Caffe on Spark for HDInsight on the head node</span></span>

<span data-ttu-id="7c7b5-140">De tweede stap is het bouwen van Caffe op de headnode, en distribueert u vervolgens de gecompileerde bibliotheken voor alle worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-140">The second step is to build Caffe on the headnode, and then distribute the compiled libraries to all the worker nodes.</span></span> <span data-ttu-id="7c7b5-141">In deze stap moet u [ssh in uw headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), gewoon Volg daarna de [CaffeOnSpark buildproces](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), en hieronder ziet u het script kunt u CaffeOnSpark bij het maken van een aantal extra stappen.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-141">In this step, you will need to [ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow the [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is the script you can use to build CaffeOnSpark with a few additional steps.</span></span> 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need to be updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want to update those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up the environment before building (especially when rebuiding), or there will be errors such as "failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #the build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put the already compiled CaffeOnSpark libraries to wasb storage, then read back to each node using script actions. This is because CaffeOnSpark requires all the nodes have the libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

<span data-ttu-id="7c7b5-142">Wellicht moet u meer dan wat de documentatie van CaffeOnSpark staat.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-142">You may need to do more than what the documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="7c7b5-143">De wijzigingen zijn:</span><span class="sxs-lookup"><span data-stu-id="7c7b5-143">The changes are:</span></span>
- <span data-ttu-id="7c7b5-144">Ga naar de CPU alleen en libatlas bepaalde hiervoor gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-144">Change to CPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="7c7b5-145">Plaats de gegevenssets naar de BLOB-opslag is een gedeelde locatie die toegankelijk is voor alle worker-knooppunten voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-145">Put the datasets to the BLOB storage, which is a shared location that is accessible to all worker nodes for later use.</span></span>
- <span data-ttu-id="7c7b5-146">Plaats de gecompileerde Caffe bibliotheken naar BLOB storage en later kopieert u deze bibliotheken voor alle knooppunten met behulp van scriptacties om te voorkomen dat extra compileertijd.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-146">Put the compiled Caffe libraries to BLOB storage, and later you will copy those libraries to all the nodes using script actions to avoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="7c7b5-147">Voor probleemoplossing: Een BuildException Ant is opgetreden: exec geretourneerd: 2</span><span class="sxs-lookup"><span data-stu-id="7c7b5-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="7c7b5-148">Wanneer u eerst probeert CaffeOnSpark bouwen, wordt soms er</span><span class="sxs-lookup"><span data-stu-id="7c7b5-148">When first trying to build CaffeOnSpark, sometimes it will say</span></span>

    failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="7c7b5-149">De opslagplaats code door gewoon opschonen "Maak schone" en voer 'Maak bouwen' lost dit probleem, zolang u de juiste afhankelijkheden hebben.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-149">Simply clean the code repository by "make clean" and then run "make build" will solve this issue, as long as you have the correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="7c7b5-150">Voor probleemoplossing: Maven-opslagplaats verbindingstime-out optreedt</span><span class="sxs-lookup"><span data-stu-id="7c7b5-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="7c7b5-151">Soms krijg maven de time-out-verbindingsfout, vergelijkbaar met hieronder:</span><span class="sxs-lookup"><span data-stu-id="7c7b5-151">Sometimes maven gives me the connection time out error, similar to below:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request to {s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="7c7b5-152">Het wordt OK worden na een wachttijd van een paar minuten en probeer vervolgens alleen de code opnieuw samenstellen zodat deze kan worden dat maven enigszins beperkt het verkeer van een opgegeven IP-adres.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-152">It will be OK after waiting for a few minutes and then just try to rebuild the code, so it might be Maven somehow limits the traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="7c7b5-153">Voor probleemoplossing: Fout voor Caffe testen</span><span class="sxs-lookup"><span data-stu-id="7c7b5-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="7c7b5-154">Waarschijnlijk ziet u een test-fout bij het uitvoeren van de laatste controle op CaffeOnSpark, vergelijkbaar met hieronder.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-154">You probably will see a test failure when doing the final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="7c7b5-155">Dit is gerelateerd aan UTF-8-codering prabably, maar moet geen invloed op het gebruik van Caffe</span><span class="sxs-lookup"><span data-stu-id="7c7b5-155">This is prabably related with UTF-8 encoding, but should not impact the usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-the-required-libraries-to-all-the-worker-nodes"></a><span data-ttu-id="7c7b5-156">Stap 3: Distribueert vereiste bibliotheken voor alle worker-knooppunten</span><span class="sxs-lookup"><span data-stu-id="7c7b5-156">Step 3: Distribute the required libraries to all the worker nodes</span></span>

<span data-ttu-id="7c7b5-157">De volgende stap is het distribueren van de tapewisselaars (in feite de bibliotheken in CaffeOnSpark/caffe-openbare/distribueren/lib/en CaffeOnSpark/caffe-distri/distribueren/lib /) voor alle knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-157">The next step is to distribute the libraries (basically the libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) to all the nodes.</span></span> <span data-ttu-id="7c7b5-158">In stap 2, we deze bibliotheken in BLOB storage plaatsen en in deze stap gebruiken we scriptacties om deze te kopiëren naar de hoofdknooppunten en worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions to copy it to all the head nodes and worker nodes.</span></span>

<span data-ttu-id="7c7b5-159">U doet dit door eenvoudig een scriptactie uitvoeren zoals hieronder (u moet verwijzen naar de juiste locatie die specifiek zijn voor uw cluster):</span><span class="sxs-lookup"><span data-stu-id="7c7b5-159">To do this, simple run a script action as below (you need to point to the right location specific to your cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="7c7b5-160">Omdat u in stap 2, we plaatsen in de BLOB-opslag die toegankelijk is voor alle knooppunten, in deze stap kopiëren gewoon items we deze voor alle knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-160">Because in step 2, we put it on the BLOB storage which is accessible to all the nodes, in this step we just simply copy it to all the nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="7c7b5-161">Stap 4: Een model Caffe opstellen en voer dit distributely</span><span class="sxs-lookup"><span data-stu-id="7c7b5-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="7c7b5-162">Na het uitvoeren van de bovenstaande stappen Caffe is al geïnstalleerd op de headnode en de aan de slag.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-162">After running the above steps, Caffe is alreay installed on the headnode and we are good to go.</span></span> <span data-ttu-id="7c7b5-163">De volgende stap is het schrijven van een model Caffe.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-163">The next step is to write a Caffe model.</span></span> 

<span data-ttu-id="7c7b5-164">Caffe is een 'expressieve architectuur', waarbij voor het opstellen van een model, u alleen hoeft te definiëren van een configuratiebestand met en zonder codering helemaal (in de meeste gevallen).</span><span class="sxs-lookup"><span data-stu-id="7c7b5-164">Caffe is using an "expressive architecture", where for composing a model, you just need to define a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="7c7b5-165">Dus laten we er.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-165">So let's take a look there.</span></span> 

<span data-ttu-id="7c7b5-166">Het model die we zullen vandaag trainen is een voorbeeld-model voor MNIST training.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-166">The model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="7c7b5-167">De database MNIST geschreven cijfers heeft een trainingset 60.000 voorbeelden en geen testset van 10.000 voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-167">The MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="7c7b5-168">Dit is een subset van een grotere set van NIST beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="7c7b5-169">De cijfers zijn grootte genormaliseerd en in het midden van de installatiekopie van een vaste grootte.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-169">The digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="7c7b5-170">CaffeOnSpark heeft sommige scripts voor het downloaden van de gegevensset en deze converteren naar de juiste indeling.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-170">CaffeOnSpark has some scripts to download the dataset and convert it into the right format.</span></span>

<span data-ttu-id="7c7b5-171">CaffeOnSpark biedt een aantal voorbeelden van de netwerk-topologieën voor MNIST training.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="7c7b5-172">Er is een goed ontwerp van het splitsen van de netwerkarchitectuur (de topologie van het netwerk) en optimalisatie van.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-172">It has a nice design of splitting the network architecture (the topology of the network) and optimization.</span></span> <span data-ttu-id="7c7b5-173">In dit geval zijn er twee bestanden vereist:</span><span class="sxs-lookup"><span data-stu-id="7c7b5-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="7c7b5-174">het bestand 'Solver '' (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) wordt gebruikt voor de optimalisatie overzien en updates van de parameter wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-174">the "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing the optimization and generating parameter updates.</span></span> <span data-ttu-id="7c7b5-175">Bijvoorbeeld definieert of CPU of GPU wordt gebruikt, wat is de dynamiek, het aantal iteraties zal zijn, enzovoort. Wordt ook gedefinieerd welke netwerktopologie neuron moet het programma gebruiken (dit is het tweede bestand we moeten).</span><span class="sxs-lookup"><span data-stu-id="7c7b5-175">For example, it defines whether CPU or GPU will be used, what's the momentum, how many iterations will be, etc. It also defines which neuron network topology should the program use (which is the second file we need).</span></span> <span data-ttu-id="7c7b5-176">Raadpleeg voor meer informatie over Solver [Caffe documentatie](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="7c7b5-176">For more information about Solver, please refer to [Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="7c7b5-177">We gebruiken CPU in plaats van GPU, moeten we voor dit voorbeeld de laatste regel te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="7c7b5-177">For this example, since we are using CPU rather than GPU, we should change the last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Caffe Config](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="7c7b5-179">U kunt andere regels indien nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-179">You can change other lines as needed.</span></span>

<span data-ttu-id="7c7b5-180">De tweede (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt)-bestand definieert hoe het netwerk neuron eruit, en de relevante invoer- en -uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-180">The second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how the neuron network looks like, and the relevant input and output file.</span></span> <span data-ttu-id="7c7b5-181">Ook moet het bestand om de locatie van de gegevens training bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-181">We also need to update the file to reflect the training data location.</span></span> <span data-ttu-id="7c7b5-182">Wijzig het volgende gedeelte in lenet_memory_train_test.prototxt (u moet verwijzen naar de juiste locatie die specifiek zijn voor uw cluster):</span><span class="sxs-lookup"><span data-stu-id="7c7b5-182">Change the following part in lenet_memory_train_test.prototxt (you need to point to the right location specific to your cluster):</span></span>

- <span data-ttu-id="7c7b5-183">Wijzig de 'file:/Users/mridul/bigml/demodl/mnist_train_lmdb' in ' wasb: / / / projecten/machine_learning/image_dataset/mnist_train_lmdb '</span><span class="sxs-lookup"><span data-stu-id="7c7b5-183">change the "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" to "wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="7c7b5-184">wijzigen in 'file:/Users/mridul/bigml/demodl/mnist_test_lmdb/' ' wasb: / / / projecten/machine_learning/image_dataset/mnist_test_lmdb '</span><span class="sxs-lookup"><span data-stu-id="7c7b5-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" to "wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Caffe Config](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="7c7b5-186">Voor meer informatie over het definiëren van het netwerk, Controleer of de [Caffe documentatie over MNIST gegevensset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="7c7b5-186">For more information on how to define the network, please check the [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="7c7b5-187">Omwille van deze blog we dit eenvoudige voorbeeld van MNIST gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-187">For the purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="7c7b5-188">U moet de onderstaande opdracht uitvoeren vanaf het hoofdknooppunt van:</span><span class="sxs-lookup"><span data-stu-id="7c7b5-188">You should run the command below from the head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="7c7b5-189">In feite deze distribueert de vereiste bestanden (lenet_memory_solver.prototxt en lenet_memory_train_test.prototxt) naar elke YARN-container en het relevante pad van elke Spark stuurprogramma/executor ook instellen op LD_LIBRARY_PATH die is gedefinieerd in de vorige codefragment en verwijst naar de locatie die CaffeOnSpark bibliotheken is.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-189">Basically it distributes the required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) to each YARN container, and also set the relevant PATH of each Spark driver/executor to LD_LIBRARY_PATH, which is defined in the previous code snippet and points to the location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="7c7b5-190">Bewaking en probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="7c7b5-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="7c7b5-191">We gebruiken YARN clustermodus, in dat geval het Spark-stuurprogramma wordt gepland om een willekeurige container (en een willekeurige werkrolknooppunt) weergegeven alleen in de console ongeveer als volgt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7c7b5-191">Since we are using YARN cluster mode, in which case the Spark driver will be scheduled to an arbitrary container (and an arbitrary worker node) you should only see in the console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="7c7b5-192">Als u weten wat er gebeurd is wilt, moet u doorgaans de Spark ophalen van stuurprogramma-logboek met meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-192">If you want to know what happened, you usually need to get the Spark driver's log, which has more information.</span></span> <span data-ttu-id="7c7b5-193">In dit geval moet u gaat u naar de gebruikersinterface van YARN de relevante YARN-logboeken vinden.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-193">In this case, you need to go to the YARN UI to find the relevant YARN logs.</span></span> <span data-ttu-id="7c7b5-194">U kunt de gebruikersinterface van YARN door deze URL krijgen:</span><span class="sxs-lookup"><span data-stu-id="7c7b5-194">You can get the YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![GEBRUIKERSINTERFACE VAN YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="7c7b5-196">U kunt bekijken hoeveel resources worden toegewezen voor deze bepaalde toepassing op te nemen.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="7c7b5-197">U kunt klikken op de koppeling "Scheduler" en vervolgens ziet u dat voor deze toepassing, er zijn 9 containers die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-197">You can click the "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="7c7b5-198">We vragen YARN voor 8 Executor en een andere container is voor stuurprogramma-proces.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-198">We ask YARN to provide 8 executors, and another container is for driver process.</span></span> 

![YARN Scheduler](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="7c7b5-200">U kunt de logboeken van de container of stuurprogramma logboeken controleren of er fouten.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-200">You may want to check the  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="7c7b5-201">Voor stuurprogramma zich aanmeldt, kunt u de toepassings-ID in de gebruikersinterface van YARN Klik op de knop 'Logboeken'.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-201">For driver logs, you can click the application ID in YARN UI, then click the "Logs" button.</span></span> <span data-ttu-id="7c7b5-202">De stuurprogramma-Logboeken geschreven in stderr.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-202">The driver logs are written into stderr.</span></span>

![GEBRUIKERSINTERFACE VAN YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="7c7b5-204">Bijvoorbeeld, ziet u mogelijk enkele van de fout hieronder in de stuurprogramma-logboeken die aangeeft dat u te veel Executor toewijzen.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-204">For example, you might see some of the error below from the driver logs, indicating you allocate too many executors.</span></span>

    17/02/01 07:26:06 ERROR ApplicationMaster: User class threw exception: java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
    java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
        at com.yahoo.ml.caffe.CaffeOnSpark.trainWithValidation(CaffeOnSpark.scala:261)
        at com.yahoo.ml.caffe.CaffeOnSpark$.main(CaffeOnSpark.scala:42)
        at com.yahoo.ml.caffe.CaffeOnSpark.main(CaffeOnSpark.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.spark.deploy.yarn.ApplicationMaster$$anon$2.run(ApplicationMaster.scala:627)

<span data-ttu-id="7c7b5-205">Soms kan het probleem kan zich voordoen in Executor in plaats van stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-205">Sometimes, the issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="7c7b5-206">In dit geval moet u de logboeken van de container.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-206">In this case, you need to check the container logs.</span></span> <span data-ttu-id="7c7b5-207">U kunt altijd de container-logboeken ophalen en vervolgens de container is mislukt.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-207">You can always get the container logs, and then get the failed container.</span></span> <span data-ttu-id="7c7b5-208">Bijvoorbeeld mogelijk voldoet deze fout aan wanneer Caffe wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-208">For example, you might meet this failure when running Caffe.</span></span>

    17/02/01 07:12:05 WARN YarnAllocator: Container marked as failed: container_1485916338528_0008_05_000005 on host: 10.0.0.14. Exit status: 134. Diagnostics: Exception from container-launch.
    Container id: container_1485916338528_0008_05_000005
    Exit code: 134
    Exception message: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

    Stack trace: ExitCodeException exitCode=134: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

        at org.apache.hadoop.util.Shell.runCommand(Shell.java:933)
        at org.apache.hadoop.util.Shell.run(Shell.java:844)
        at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:1123)
        at org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor.launchContainer(DefaultContainerExecutor.java:225)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:317)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:83)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
        at java.lang.Thread.run(Thread.java:745)


    Container exited with a non-zero exit code 134

<span data-ttu-id="7c7b5-209">In dit geval moet u de mislukte container-ID (dit is in het bovenstaande geval container_1485916338528_0008_05_000005).</span><span class="sxs-lookup"><span data-stu-id="7c7b5-209">In this case, you need to get the failed container ID (in the above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="7c7b5-210">U hoeft uit te voeren</span><span class="sxs-lookup"><span data-stu-id="7c7b5-210">Then you need to run</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="7c7b5-211">van de headnode.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-211">from the headnode.</span></span> <span data-ttu-id="7c7b5-212">Nadat u hebt gecontroleerd container mislukt, wordt dit veroorzaakt door met GPU-modus (waarbij u gebruik CPU-modus in plaats daarvan) in lenet_memory_solver.prototxt.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written to STDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="7c7b5-213">Ophalen van resultaten</span><span class="sxs-lookup"><span data-stu-id="7c7b5-213">Getting results</span></span>

<span data-ttu-id="7c7b5-214">Aangezien we 8 Executor toewijzen wilt en de netwerktopologie eenvoudig is, moet het alleen ongeveer 30 minuten duren om uit te voeren van het resultaat.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-214">Since we are allocating 8 executors, and the network topology is simple, it should only take around 30 minutes to run the result.</span></span> <span data-ttu-id="7c7b5-215">Vanaf de opdrachtregel, ziet u dat we plaatst u het model voor wasb:///mnist.model, en de resultaten naar een map met de naam wasb: / / / mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-215">From the command line, you can see that we put the model to wasb:///mnist.model, and put the results to a folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="7c7b5-216">U kunt de resultaten krijgen door te voeren</span><span class="sxs-lookup"><span data-stu-id="7c7b5-216">You can get the results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="7c7b5-217">en het resultaat lijkt op:</span><span class="sxs-lookup"><span data-stu-id="7c7b5-217">and the result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="7c7b5-218">De SampleID vertegenwoordigt de ID in de gegevensset MNIST, en het label is het nummer van het model.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-218">The SampleID represents the ID in the MNIST dataset, and the label is the number that the model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="7c7b5-219">Conclusie</span><span class="sxs-lookup"><span data-stu-id="7c7b5-219">Conclusion</span></span>

<span data-ttu-id="7c7b5-220">U hebt geprobeerd in deze documentatie CaffeOnSpark installeren met het uitvoeren van een eenvoudig voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-220">In this documentation, you have tried to install CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="7c7b5-221">HDInsight is een volledig beheerde cloud gedistribueerde compute-platform en de beste plaats voor het uitvoeren van machine learning en geavanceerde analyses werkbelastingen op grote gegevensset en voor gedistribueerde grondige learning, kunt u Caffe op HDInsight Spark grondige learning taken uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="7c7b5-221">HDInsight is a full managed cloud distributed compute platform, and is the best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark to perform deep learning tasks.</span></span>


## <span data-ttu-id="7c7b5-222"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="7c7b5-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="7c7b5-223">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c7b5-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="7c7b5-224">Scenario's</span><span class="sxs-lookup"><span data-stu-id="7c7b5-224">Scenarios</span></span>
* [<span data-ttu-id="7c7b5-225">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="7c7b5-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="7c7b5-226">Spark met Machine Learning: Spark in HDInsight gebruiken om voedselinspectieresultaten te voorspellen</span><span class="sxs-lookup"><span data-stu-id="7c7b5-226">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="7c7b5-227">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="7c7b5-227">Manage resources</span></span>
* [<span data-ttu-id="7c7b5-228">Resources beheren voor het Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c7b5-228">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

