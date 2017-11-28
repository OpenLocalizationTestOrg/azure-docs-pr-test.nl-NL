---
title: aaaUse Caffe op Azure HDInsight Spark voor gedistribueerde grondige learning | Microsoft Docs
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
ms.openlocfilehash: d6476a7ed3a0df38538e845d7d5404067b01113c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="1ba4e-103">Gebruik Caffe op Azure HDInsight Spark voor gedistribueerde grondige learning</span><span class="sxs-lookup"><span data-stu-id="1ba4e-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="1ba4e-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="1ba4e-104">Introduction</span></span>

<span data-ttu-id="1ba4e-105">Grondige learning is van invloed op Alles van gezondheidszorg tootransportation toomanufacturing en meer.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-105">Deep learning is impacting everything from healthcare tootransportation toomanufacturing, and more.</span></span> <span data-ttu-id="1ba4e-106">Bedrijven schakelt toodeep learning toosolve harde problemen, zoals [installatiekopie classificatie](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [spraakherkenning](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)erkenning object en de vertaling van de computer.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-106">Companies are turning toodeep learning toosolve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="1ba4e-107">Er zijn [veel populaire frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), waaronder [Microsoft cognitieve Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, enzovoort. Caffe is een van de Hallo grootste beroemdheid neurale netwerk wordt niet symbolische (imperatieve) frameworks en veel worden gebruikt in veel gebieden, waaronder computer vision.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of hello most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="1ba4e-108">Bovendien [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combineert Caffe met Apache Spark, in welk geval diep learning gemakkelijk kan worden gebruikt op een bestaande Hadoop-cluster samen met Spark ETL pijplijnen, de complexiteit van systeem en latentie voor end-to-end learning.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="1ba4e-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) Hallo is alleen een volledig beheerde cloud Hadoop aanbieding die voorziet in analytische clusters open-source geoptimaliseerd voor Spark, Hive, MapReduce, HBase, Storm, Kafka en ondersteund door een SLA met 99,9% R-Server.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is hello only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="1ba4e-110">Al deze big data-technologieën en ISV-toepassingen zijn eenvoudig te implementeren als beheerde clusters met beveiliging en bewaking op ondernemingsniveau.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="1ba4e-111">Sommige gebruikers vragen ons over het toouse grondige learning op HDInsight, namelijk PaaS Hadoop-product van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-111">Some users are asking us about how toouse deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="1ba4e-112">We hebben meer tooshare in toekomstige hello, maar tegenwoordig willen we toosummarize een technische blog over de toouse Caffe op HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-112">We will have more tooshare in hello future, but today we want toosummarize a technical blog on how toouse Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="1ba4e-113">Als u Caffe voordat hebt geïnstalleerd, ziet u dat het installeren van dit framework iets lastig is.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="1ba4e-114">In deze blog we wordt eerst laten zien hoe tooinstall [Caffe op Spark](https://github.com/yahoo/CaffeOnSpark) voor een HDInsight-cluster vervolgens gebruik Hallo ingebouwde MNIST demo toodemostrate hoe toouse gedistribueerde grondige Learning met HDInsight Spark op CPU's.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-114">In this blog, we will first illustrate how tooinstall [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use hello built-in MNIST demo toodemostrate how toouse Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="1ba4e-115">Er zijn vier hoofdstappen tooget werkt deze op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-115">There are four major steps tooget it work on HDInsight.</span></span>

1. <span data-ttu-id="1ba4e-116">Hallo vereist afhankelijkheden installeren op alle Hallo-knooppunten</span><span class="sxs-lookup"><span data-stu-id="1ba4e-116">Install hello required dependencies on all hello nodes</span></span>
2. <span data-ttu-id="1ba4e-117">Caffe voor Spark voor HDInsight op Hallo hoofdknooppunt bouwen</span><span class="sxs-lookup"><span data-stu-id="1ba4e-117">Build Caffe on Spark for HDInsight on hello head node</span></span>
3. <span data-ttu-id="1ba4e-118">Hallo vereist bibliotheken tooall Hallo worker-knooppunten distribueren</span><span class="sxs-lookup"><span data-stu-id="1ba4e-118">Distribute hello required libraries tooall hello worker nodes</span></span>
4. <span data-ttu-id="1ba4e-119">Een model Caffe opstellen en voer dit distributely</span><span class="sxs-lookup"><span data-stu-id="1ba4e-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="1ba4e-120">Aangezien HDInsight een PaaS-oplossing is, biedt uitstekende platformfuncties - zodat u eenvoudig tooperform sommige taken.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy tooperform some tasks.</span></span> <span data-ttu-id="1ba4e-121">Een van de Hallo-functies die we veel in dit blogbericht gebruiken heet [scriptactie](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), die u kunt uitvoeren met de shell-opdrachten toocustomize clusterknooppunten (hoofdknooppunt, werkrolknooppunt of edge-knooppunt).</span><span class="sxs-lookup"><span data-stu-id="1ba4e-121">One of hello features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands toocustomize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a><span data-ttu-id="1ba4e-122">Stap 1: Hallo vereist afhankelijkheden installeren op alle knooppunten van het Hallo</span><span class="sxs-lookup"><span data-stu-id="1ba4e-122">Step 1:  Install hello required dependencies on all hello nodes</span></span>

<span data-ttu-id="1ba4e-123">tooget gestart, moeten we tooinstall Hallo afhankelijkheden die we nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-123">tooget started, we need tooinstall hello dependencies we need.</span></span> <span data-ttu-id="1ba4e-124">Hallo Caffe site en [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) biedt sommige wiki erg nuttig zijn voor het installeren van Hallo afhankelijkheden voor Spark op YARN-modus (dit is de modus voor HDInsight Spark Hallo), maar we moeten tooadd enkele meer afhankelijkheden voor HDInsight-platform.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-124">hello Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing hello dependencies for Spark on YARN mode (which is hello mode for HDInsight Spark), but we need tooadd a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="1ba4e-125">We gebruiken Hallo scriptactie zoals hieronder en uitvoeren op alle hoofdknooppunten Hallo en worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-125">We will use hello script action as below and run it on all hello head nodes and worker nodes.</span></span> <span data-ttu-id="1ba4e-126">Deze scriptactie duurt ongeveer 20 minuten, zoals die afhankelijkheden is ook afhankelijk van andere pakketten zijn.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="1ba4e-127">U moet deze in een locatie die toegankelijk tooyour HDInsight-cluster, zoals een GitHub-locatie of Hallo standaard BLOB storage-account is geplaatst.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-127">You should put it in some location that is accessible tooyour HDInsight cluster, such as a GitHub location or hello default BLOB storage account.</span></span>

    #!/bin/bash
    #Please be aware that installing hello below will add additional 20 mins toocluster creation because of hello dependencies
    #installing all dependencies, including hello ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all hello nodes

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


<span data-ttu-id="1ba4e-128">Er zijn twee stappen in de bovenstaande Hallo scriptactie.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-128">There are two steps in hello script action above.</span></span> <span data-ttu-id="1ba4e-129">de eerste stap Hallo is tooinstall alle vereiste bibliotheken Hallo.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-129">hello first step is tooinstall all hello required libraries.</span></span> <span data-ttu-id="1ba4e-130">Deze bibliotheken bevatten Hallo nodig bibliotheken voor zowel Caffe compileren (zoals gflags, glog) en het uitvoeren van Caffe (zoals numpy).</span><span class="sxs-lookup"><span data-stu-id="1ba4e-130">Those libraries include hello necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="1ba4e-131">We libatlas voor CPU-optimalisatie gebruiken, maar u kunt altijd Hallo CaffeOnSpark wiki volgen over het installeren van andere bibliotheken optimalisatie zoals MKL of CUDA (voor GPU).</span><span class="sxs-lookup"><span data-stu-id="1ba4e-131">We are using libatlas for CPU optimization, but you can always follow hello CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="1ba4e-132">Hallo tweede stap bestaat uit toodownload, compileren en protobuf 2.5.0 voor Caffe installeren tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-132">hello second step is toodownload, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="1ba4e-133">Protobuf 2.5.0 [is vereist](https://github.com/yahoo/CaffeOnSpark/issues/87), maar deze versie niet beschikbaar als een pakket op Ubuntu 16, is dus we er toocompile moeten op Hallo broncode.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need toocompile it from hello source code.</span></span> <span data-ttu-id="1ba4e-134">Er zijn ook enkele bronnen op Hallo Internet over het toocompile, zoals [dit](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="1ba4e-134">There are also a few resources on hello Internet on how toocompile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="1ba4e-135">toosimply aan de slag, u kunt alleen uitvoeren met deze scriptactie op uw cluster tooall Hallo worker knooppunten en head knooppunten (voor HDInsight 3.5).</span><span class="sxs-lookup"><span data-stu-id="1ba4e-135">toosimply get started, you can just run this script action against your cluster tooall hello worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="1ba4e-136">U kunt ofwel scriptacties Hallo voor een actieve cluster uitvoeren of u kunt ook Hallo scriptacties uitvoeren tijdens Hallo cluster inrichten.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-136">You can either run hello script actions for a running cluster, or you can also run hello script actions during hello cluster provision time.</span></span> <span data-ttu-id="1ba4e-137">Zie voor meer informatie over scriptacties Hallo Hallo documentatie [hier](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="1ba4e-137">For more details on hello script actions, please see hello documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![Script acties tooInstall afhankelijkheden](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a><span data-ttu-id="1ba4e-139">Stap 2: Caffe voor Spark voor HDInsight op Hallo hoofdknooppunt bouwen</span><span class="sxs-lookup"><span data-stu-id="1ba4e-139">Step 2: Build Caffe on Spark for HDInsight on hello head node</span></span>

<span data-ttu-id="1ba4e-140">de tweede stap Hallo toobuild Caffe op Hallo headnode is en vervolgens distribueren Hallo gecompileerd bibliotheken tooall Hallo worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-140">hello second step is toobuild Caffe on hello headnode, and then distribute hello compiled libraries tooall hello worker nodes.</span></span> <span data-ttu-id="1ba4e-141">In deze stap moet u te[ssh in uw headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), volg Hallo gewoon [CaffeOnSpark buildproces](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), en hieronder vindt u toobuild CaffeOnSpark kunt gebruiken met een aantal extra stappen Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-141">In this step, you will need too[ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow hello [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is hello script you can use toobuild CaffeOnSpark with a few additional steps.</span></span> 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need toobe updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want tooupdate those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up hello environment before building (especially when rebuiding), or there will be errors such as "failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #hello build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put hello already compiled CaffeOnSpark libraries toowasb storage, then read back tooeach node using script actions. This is because CaffeOnSpark requires all hello nodes have hello libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

<span data-ttu-id="1ba4e-142">Mogelijk moet u toodo meer dan welke documentatie Hallo van CaffeOnSpark staat.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-142">You may need toodo more than what hello documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="1ba4e-143">Hallo wijzigingen zijn:</span><span class="sxs-lookup"><span data-stu-id="1ba4e-143">hello changes are:</span></span>
- <span data-ttu-id="1ba4e-144">Wijzig alleen tooCPU en libatlas bepaalde hiervoor gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-144">Change tooCPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="1ba4e-145">Hallo gegevenssets toohello BLOB storage, een gedeelde locatie plaatsen is dat toegankelijk tooall worker-knooppunten voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-145">Put hello datasets toohello BLOB storage, which is a shared location that is accessible tooall worker nodes for later use.</span></span>
- <span data-ttu-id="1ba4e-146">Put Hallo gecompileerd Caffe bibliotheken tooBLOB opslag en kopieert u later deze bibliotheken tooall Hallo knooppunten met behulp van script acties tooavoid extra compileertijd.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-146">Put hello compiled Caffe libraries tooBLOB storage, and later you will copy those libraries tooall hello nodes using script actions tooavoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="1ba4e-147">Voor probleemoplossing: Een BuildException Ant is opgetreden: exec geretourneerd: 2</span><span class="sxs-lookup"><span data-stu-id="1ba4e-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="1ba4e-148">Wanneer u eerst probeert toobuild CaffeOnSpark, wordt soms er</span><span class="sxs-lookup"><span data-stu-id="1ba4e-148">When first trying toobuild CaffeOnSpark, sometimes it will say</span></span>

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="1ba4e-149">Gewoon schone Hallo code opslagplaats door 'schone maken' uit en vervolgens uitvoeren 'Maak bouwen' lost dit probleem, zolang u de juiste afhankelijkheden Hallo hebt.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-149">Simply clean hello code repository by "make clean" and then run "make build" will solve this issue, as long as you have hello correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="1ba4e-150">Voor probleemoplossing: Maven-opslagplaats verbindingstime-out optreedt</span><span class="sxs-lookup"><span data-stu-id="1ba4e-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="1ba4e-151">Soms hebt maven mij Hallo verbinding time-outfout, vergelijkbare toobelow:</span><span class="sxs-lookup"><span data-stu-id="1ba4e-151">Sometimes maven gives me hello connection time out error, similar toobelow:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="1ba4e-152">Deze OK na een wachttijd van een paar minuten en probeer NET toorebuild Hallo code, zodat Maven mogelijk enigszins limieten Hallo verkeer van een opgegeven IP-adres.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-152">It will be OK after waiting for a few minutes and then just try toorebuild hello code, so it might be Maven somehow limits hello traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="1ba4e-153">Voor probleemoplossing: Fout voor Caffe testen</span><span class="sxs-lookup"><span data-stu-id="1ba4e-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="1ba4e-154">Waarschijnlijk ziet u een test-fout bij het uitvoeren van de laatste controle Hallo voor CaffeOnSpark, vergelijkbaar met hieronder.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-154">You probably will see a test failure when doing hello final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="1ba4e-155">Dit is prabably gerelateerd aan UTF-8-codering, maar moet geen invloed op Hallo gebruik van Caffe</span><span class="sxs-lookup"><span data-stu-id="1ba4e-155">This is prabably related with UTF-8 encoding, but should not impact hello usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a><span data-ttu-id="1ba4e-156">Stap 3: Distribueert vereiste Hallo bibliotheken tooall Hallo worker-knooppunten</span><span class="sxs-lookup"><span data-stu-id="1ba4e-156">Step 3: Distribute hello required libraries tooall hello worker nodes</span></span>

<span data-ttu-id="1ba4e-157">de volgende stap Hallo is toodistribute Hallo-bibliotheken (in feite Hallo-bibliotheken in CaffeOnSpark/caffe-openbare/distribueren/lib/en CaffeOnSpark/caffe-distri/distribueren/lib /) tooall Hallo knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-157">hello next step is toodistribute hello libraries (basically hello libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) tooall hello nodes.</span></span> <span data-ttu-id="1ba4e-158">In stap 2 we deze bibliotheken in BLOB storage plaatsen en in deze stap gebruiken we script acties toocopy het tooall Hallo hoofdknooppunten en worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions toocopy it tooall hello head nodes and worker nodes.</span></span>

<span data-ttu-id="1ba4e-159">toodo deze, eenvoudig uitvoeren van een scriptactie zoals hieronder (u moet toopoint toohello juiste locatie specifieke tooyour cluster):</span><span class="sxs-lookup"><span data-stu-id="1ba4e-159">toodo this, simple run a script action as below (you need toopoint toohello right location specific tooyour cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="1ba4e-160">Omdat u in stap 2, we op plaatsen Hallo BLOB-opslag die toegankelijk tooall Hallo knooppunten, in deze stap kopiëren gewoon items we deze tooall Hallo knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-160">Because in step 2, we put it on hello BLOB storage which is accessible tooall hello nodes, in this step we just simply copy it tooall hello nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="1ba4e-161">Stap 4: Een model Caffe opstellen en voer dit distributely</span><span class="sxs-lookup"><span data-stu-id="1ba4e-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="1ba4e-162">Na het uitvoeren van Hallo bovenstaande stappen Caffe is al geïnstalleerd op Hallo headnode en de goede toogo.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-162">After running hello above steps, Caffe is alreay installed on hello headnode and we are good toogo.</span></span> <span data-ttu-id="1ba4e-163">de volgende stap Hallo is toowrite een Caffe-model.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-163">hello next step is toowrite a Caffe model.</span></span> 

<span data-ttu-id="1ba4e-164">Caffe maakt gebruik van een 'expressieve architectuur,' wanneer een model u zojuist hebt voor het opstellen van een configuratiebestand toodefine en zonder codering helemaal (in de meeste gevallen).</span><span class="sxs-lookup"><span data-stu-id="1ba4e-164">Caffe is using an "expressive architecture", where for composing a model, you just need toodefine a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="1ba4e-165">Dus laten we er.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-165">So let's take a look there.</span></span> 

<span data-ttu-id="1ba4e-166">we zullen vandaag trainen Hallo-model is een voorbeeld-model voor MNIST training.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-166">hello model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="1ba4e-167">Hallo MNIST database geschreven cijfers heeft een trainingset 60.000 voorbeelden en geen testset van 10.000 voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-167">hello MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="1ba4e-168">Dit is een subset van een grotere set van NIST beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="1ba4e-169">Hallo cijfers zijn grootte genormaliseerd en in het midden van de installatiekopie van een vaste grootte.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-169">hello digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="1ba4e-170">CaffeOnSpark heeft een aantal scripts toodownload Hallo gegevensset en te converteren naar de juiste notatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-170">CaffeOnSpark has some scripts toodownload hello dataset and convert it into hello right format.</span></span>

<span data-ttu-id="1ba4e-171">CaffeOnSpark biedt een aantal voorbeelden van de netwerk-topologieën voor MNIST training.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="1ba4e-172">Een goed ontwerp van splitsing Hallo netwerkarchitectuur (Hallo topologie van het Hallo-netwerk) en optimalisatie van heeft.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-172">It has a nice design of splitting hello network architecture (hello topology of hello network) and optimization.</span></span> <span data-ttu-id="1ba4e-173">In dit geval zijn er twee bestanden vereist:</span><span class="sxs-lookup"><span data-stu-id="1ba4e-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="1ba4e-174">Hallo 'Solver '' bestand (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) wordt gebruikt voor het Hallo-optimalisatie overzien en parameter updates genereren.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-174">hello "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing hello optimization and generating parameter updates.</span></span> <span data-ttu-id="1ba4e-175">Bijvoorbeeld definieert of CPU of GPU wordt gebruikt, wat is er Hallo dynamiek, het aantal iteraties zal zijn, enzovoort. Ook wordt gedefinieerd welke netwerktopologie neuron moet Hallo programma gebruiken (dit is de tweede bestand Hallo we moeten).</span><span class="sxs-lookup"><span data-stu-id="1ba4e-175">For example, it defines whether CPU or GPU will be used, what's hello momentum, how many iterations will be, etc. It also defines which neuron network topology should hello program use (which is hello second file we need).</span></span> <span data-ttu-id="1ba4e-176">Voor meer informatie over Solver Raadpleeg te[Caffe documentatie](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="1ba4e-176">For more information about Solver, please refer too[Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="1ba4e-177">We gebruiken CPU in plaats van GPU, moeten we voor dit voorbeeld Hallo laatste regel te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="1ba4e-177">For this example, since we are using CPU rather than GPU, we should change hello last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Caffe Config](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="1ba4e-179">U kunt andere regels indien nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-179">You can change other lines as needed.</span></span>

<span data-ttu-id="1ba4e-180">tweede Hallo-bestand (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) definieert hoe Hallo neuron netwerk eruit, en relevante Hallo-invoer en uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-180">hello second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how hello neuron network looks like, and hello relevant input and output file.</span></span> <span data-ttu-id="1ba4e-181">Er moet ook tooupdate hello tooreflect Hallo training gegevens bestandslocatie.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-181">We also need tooupdate hello file tooreflect hello training data location.</span></span> <span data-ttu-id="1ba4e-182">Wijzig hello onderdeel in lenet_memory_train_test.prototxt (u moet toopoint toohello juiste locatie specifieke tooyour cluster) te volgen:</span><span class="sxs-lookup"><span data-stu-id="1ba4e-182">Change hello following part in lenet_memory_train_test.prototxt (you need toopoint toohello right location specific tooyour cluster):</span></span>

- <span data-ttu-id="1ba4e-183">Hallo 'file:/Users/mridul/bigml/demodl/mnist_train_lmdb' te wijzigen "wasb: / / / projecten/machine_learning/image_dataset/mnist_train_lmdb '</span><span class="sxs-lookup"><span data-stu-id="1ba4e-183">change hello "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" too"wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="1ba4e-184">'file:/Users/mridul/bigml/demodl/mnist_test_lmdb/' te wijzigen "wasb: / / / projecten/machine_learning/image_dataset/mnist_test_lmdb '</span><span class="sxs-lookup"><span data-stu-id="1ba4e-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" too"wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Caffe Config](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="1ba4e-186">Controleer voor meer informatie over hoe toodefine netwerk Hallo Hallo [Caffe documentatie over MNIST gegevensset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="1ba4e-186">For more information on how toodefine hello network, please check hello [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="1ba4e-187">Voor Hallo doel van deze blog gebruiken we dit eenvoudige voorbeeld van MNIST.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-187">For hello purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="1ba4e-188">Hallo onderstaande opdracht moet worden uitgevoerd vanaf het hoofdknooppunt Hallo van:</span><span class="sxs-lookup"><span data-stu-id="1ba4e-188">You should run hello command below from hello head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="1ba4e-189">In feite wordt gedistribueerd Hallo vereist-bestanden (lenet_memory_solver.prototxt en lenet_memory_train_test.prototxt) tooeach garens container en ook relevante pad van elke Spark stuurprogramma/executor tooLD_LIBRARY_PATH, die is gedefinieerd in Hallo Hallo vorige code codefragment en punten toohello locatie met CaffeOnSpark bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-189">Basically it distributes hello required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) tooeach YARN container, and also set hello relevant PATH of each Spark driver/executor tooLD_LIBRARY_PATH, which is defined in hello previous code snippet and points toohello location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="1ba4e-190">Bewaking en probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="1ba4e-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="1ba4e-191">We gebruiken YARN clustermodus, in welk geval Hallo Spark stuurprogramma worden geplande tooan willekeurige container (en een willekeurige werkrolknooppunt) moet wordt alleen weergegeven in het Hallo console uitvoeren als:</span><span class="sxs-lookup"><span data-stu-id="1ba4e-191">Since we are using YARN cluster mode, in which case hello Spark driver will be scheduled tooan arbitrary container (and an arbitrary worker node) you should only see in hello console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="1ba4e-192">Als u tooknow wat er gebeurd is wilt, moet u meestal tooget Hallo Spark van stuurprogramma-logboek met meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-192">If you want tooknow what happened, you usually need tooget hello Spark driver's log, which has more information.</span></span> <span data-ttu-id="1ba4e-193">In dit geval moet u toogo toohello gebruikersinterface van YARN toofind Hallo relevante YARN-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-193">In this case, you need toogo toohello YARN UI toofind hello relevant YARN logs.</span></span> <span data-ttu-id="1ba4e-194">U kunt krijgen Hallo gebruikersinterface van YARN door deze URL:</span><span class="sxs-lookup"><span data-stu-id="1ba4e-194">You can get hello YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![GEBRUIKERSINTERFACE VAN YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="1ba4e-196">U kunt bekijken hoeveel resources worden toegewezen voor deze bepaalde toepassing op te nemen.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="1ba4e-197">U kunt klikken op Hallo 'Scheduler' koppeling en, ziet u dat voor deze toepassing, er zijn 9 containers die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-197">You can click hello "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="1ba4e-198">We vragen YARN tooprovide 8 Executor en een andere container is voor stuurprogramma-proces.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-198">We ask YARN tooprovide 8 executors, and another container is for driver process.</span></span> 

![YARN Scheduler](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="1ba4e-200">U kunt toocheck Hallo stuurprogramma Logboeken of de logboeken van de container als er fouten zijn.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-200">You may want toocheck hello  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="1ba4e-201">Voor het stuurprogramma zich aanmeldt, kunt u Hallo toepassings-ID in de gebruikersinterface van YARN, klik op Hallo 'Logs' knop.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-201">For driver logs, you can click hello application ID in YARN UI, then click hello "Logs" button.</span></span> <span data-ttu-id="1ba4e-202">Hallo stuurprogramma logboeken worden geschreven in stderr.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-202">hello driver logs are written into stderr.</span></span>

![GEBRUIKERSINTERFACE VAN YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="1ba4e-204">Bijvoorbeeld, ziet u mogelijk enkele Hallo fout hieronder van Hallo stuurprogramma zich aanmeldt, die aangeeft dat u te veel Executor toewijzen.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-204">For example, you might see some of hello error below from hello driver logs, indicating you allocate too many executors.</span></span>

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

<span data-ttu-id="1ba4e-205">Soms Hallo probleem kan zich voordoen in Executor in plaats van stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-205">Sometimes, hello issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="1ba4e-206">In dit geval moet u toocheck Hallo container Logboeken.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-206">In this case, you need toocheck hello container logs.</span></span> <span data-ttu-id="1ba4e-207">U kunt altijd Hallo container logboeken ophalen en vervolgens Hallo mislukte container.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-207">You can always get hello container logs, and then get hello failed container.</span></span> <span data-ttu-id="1ba4e-208">Bijvoorbeeld mogelijk voldoet deze fout aan wanneer Caffe wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-208">For example, you might meet this failure when running Caffe.</span></span>

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

<span data-ttu-id="1ba4e-209">In dit geval moet u tooget Hallo mislukt container-ID (in Hallo boven het geval is, is het container_1485916338528_0008_05_000005).</span><span class="sxs-lookup"><span data-stu-id="1ba4e-209">In this case, you need tooget hello failed container ID (in hello above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="1ba4e-210">Vervolgens moet u toorun</span><span class="sxs-lookup"><span data-stu-id="1ba4e-210">Then you need toorun</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="1ba4e-211">van Hallo headnode.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-211">from hello headnode.</span></span> <span data-ttu-id="1ba4e-212">Nadat u hebt gecontroleerd container mislukt, wordt dit veroorzaakt door met GPU-modus (waarbij u gebruik CPU-modus in plaats daarvan) in lenet_memory_solver.prototxt.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="1ba4e-213">Ophalen van resultaten</span><span class="sxs-lookup"><span data-stu-id="1ba4e-213">Getting results</span></span>

<span data-ttu-id="1ba4e-214">Aangezien we 8 Executor toewijzen wilt en netwerktopologie Hallo eenvoudig is, neemt het ongeveer 30 minuten toorun Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-214">Since we are allocating 8 executors, and hello network topology is simple, it should only take around 30 minutes toorun hello result.</span></span> <span data-ttu-id="1ba4e-215">Vanaf de opdrachtregel hello, ziet u dat we plaatst u Hallo model toowasb:///mnist.model, en Hallo resultaten tooa map met de naam wasb: / / / mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-215">From hello command line, you can see that we put hello model toowasb:///mnist.model, and put hello results tooa folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="1ba4e-216">U kunt Hallo resultaten krijgen door te voeren</span><span class="sxs-lookup"><span data-stu-id="1ba4e-216">You can get hello results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="1ba4e-217">en Hallo resultaat lijkt op:</span><span class="sxs-lookup"><span data-stu-id="1ba4e-217">and hello result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="1ba4e-218">Hallo SampleID vertegenwoordigt Hallo-ID in Hallo MNIST gegevensset en Hallo-label is Hallo getal dat Hallo model identificeert.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-218">hello SampleID represents hello ID in hello MNIST dataset, and hello label is hello number that hello model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="1ba4e-219">Conclusie</span><span class="sxs-lookup"><span data-stu-id="1ba4e-219">Conclusion</span></span>

<span data-ttu-id="1ba4e-220">U hebt in deze documentatie tooinstall CaffeOnSpark geprobeerd met het uitvoeren van een eenvoudig voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-220">In this documentation, you have tried tooinstall CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="1ba4e-221">HDInsight is een volledig beheerde gedistribueerde compute cloudplatform, Hallo beste plaats voor het uitvoeren van machine learning en geavanceerde analyses werkbelastingen op grote gegevensset en voor gedistribueerde grondige learning, kunt u Caffe gebruiken in HDInsight Spark tooperform grondige kennis taken.</span><span class="sxs-lookup"><span data-stu-id="1ba4e-221">HDInsight is a full managed cloud distributed compute platform, and is hello best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark tooperform deep learning tasks.</span></span>


## <span data-ttu-id="1ba4e-222"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="1ba4e-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="1ba4e-223">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1ba4e-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="1ba4e-224">Scenario's</span><span class="sxs-lookup"><span data-stu-id="1ba4e-224">Scenarios</span></span>
* [<span data-ttu-id="1ba4e-225">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="1ba4e-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="1ba4e-226">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="1ba4e-226">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="1ba4e-227">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="1ba4e-227">Manage resources</span></span>
* [<span data-ttu-id="1ba4e-228">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1ba4e-228">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

