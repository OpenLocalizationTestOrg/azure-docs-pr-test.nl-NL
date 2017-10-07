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
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a>Gebruik Caffe op Azure HDInsight Spark voor gedistribueerde grondige learning


## <a name="introduction"></a>Inleiding

Grondige learning is van invloed op Alles van gezondheidszorg tootransportation toomanufacturing en meer. Bedrijven schakelt toodeep learning toosolve harde problemen, zoals [installatiekopie classificatie](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [spraakherkenning](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)erkenning object en de vertaling van de computer. 

Er zijn [veel populaire frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), waaronder [Microsoft cognitieve Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, enzovoort. Caffe is een van de Hallo grootste beroemdheid neurale netwerk wordt niet symbolische (imperatieve) frameworks en veel worden gebruikt in veel gebieden, waaronder computer vision. Bovendien [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combineert Caffe met Apache Spark, in welk geval diep learning gemakkelijk kan worden gebruikt op een bestaande Hadoop-cluster samen met Spark ETL pijplijnen, de complexiteit van systeem en latentie voor end-to-end learning.

[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) Hallo is alleen een volledig beheerde cloud Hadoop aanbieding die voorziet in analytische clusters open-source geoptimaliseerd voor Spark, Hive, MapReduce, HBase, Storm, Kafka en ondersteund door een SLA met 99,9% R-Server. Al deze big data-technologieën en ISV-toepassingen zijn eenvoudig te implementeren als beheerde clusters met beveiliging en bewaking op ondernemingsniveau.

Sommige gebruikers vragen ons over het toouse grondige learning op HDInsight, namelijk PaaS Hadoop-product van Microsoft. We hebben meer tooshare in toekomstige hello, maar tegenwoordig willen we toosummarize een technische blog over de toouse Caffe op HDInsight Spark.

Als u Caffe voordat hebt geïnstalleerd, ziet u dat het installeren van dit framework iets lastig is. In deze blog we wordt eerst laten zien hoe tooinstall [Caffe op Spark](https://github.com/yahoo/CaffeOnSpark) voor een HDInsight-cluster vervolgens gebruik Hallo ingebouwde MNIST demo toodemostrate hoe toouse gedistribueerde grondige Learning met HDInsight Spark op CPU's.

Er zijn vier hoofdstappen tooget werkt deze op HDInsight.

1. Hallo vereist afhankelijkheden installeren op alle Hallo-knooppunten
2. Caffe voor Spark voor HDInsight op Hallo hoofdknooppunt bouwen
3. Hallo vereist bibliotheken tooall Hallo worker-knooppunten distribueren
4. Een model Caffe opstellen en voer dit distributely

Aangezien HDInsight een PaaS-oplossing is, biedt uitstekende platformfuncties - zodat u eenvoudig tooperform sommige taken. Een van de Hallo-functies die we veel in dit blogbericht gebruiken heet [scriptactie](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), die u kunt uitvoeren met de shell-opdrachten toocustomize clusterknooppunten (hoofdknooppunt, werkrolknooppunt of edge-knooppunt).

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a>Stap 1: Hallo vereist afhankelijkheden installeren op alle knooppunten van het Hallo

tooget gestart, moeten we tooinstall Hallo afhankelijkheden die we nodig hebben. Hallo Caffe site en [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) biedt sommige wiki erg nuttig zijn voor het installeren van Hallo afhankelijkheden voor Spark op YARN-modus (dit is de modus voor HDInsight Spark Hallo), maar we moeten tooadd enkele meer afhankelijkheden voor HDInsight-platform. We gebruiken Hallo scriptactie zoals hieronder en uitvoeren op alle hoofdknooppunten Hallo en worker-knooppunten. Deze scriptactie duurt ongeveer 20 minuten, zoals die afhankelijkheden is ook afhankelijk van andere pakketten zijn. U moet deze in een locatie die toegankelijk tooyour HDInsight-cluster, zoals een GitHub-locatie of Hallo standaard BLOB storage-account is geplaatst.

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


Er zijn twee stappen in de bovenstaande Hallo scriptactie. de eerste stap Hallo is tooinstall alle vereiste bibliotheken Hallo. Deze bibliotheken bevatten Hallo nodig bibliotheken voor zowel Caffe compileren (zoals gflags, glog) en het uitvoeren van Caffe (zoals numpy). We libatlas voor CPU-optimalisatie gebruiken, maar u kunt altijd Hallo CaffeOnSpark wiki volgen over het installeren van andere bibliotheken optimalisatie zoals MKL of CUDA (voor GPU).

Hallo tweede stap bestaat uit toodownload, compileren en protobuf 2.5.0 voor Caffe installeren tijdens runtime. Protobuf 2.5.0 [is vereist](https://github.com/yahoo/CaffeOnSpark/issues/87), maar deze versie niet beschikbaar als een pakket op Ubuntu 16, is dus we er toocompile moeten op Hallo broncode. Er zijn ook enkele bronnen op Hallo Internet over het toocompile, zoals [dit](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)

toosimply aan de slag, u kunt alleen uitvoeren met deze scriptactie op uw cluster tooall Hallo worker knooppunten en head knooppunten (voor HDInsight 3.5). U kunt ofwel scriptacties Hallo voor een actieve cluster uitvoeren of u kunt ook Hallo scriptacties uitvoeren tijdens Hallo cluster inrichten. Zie voor meer informatie over scriptacties Hallo Hallo documentatie [hier](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)

![Script acties tooInstall afhankelijkheden](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a>Stap 2: Caffe voor Spark voor HDInsight op Hallo hoofdknooppunt bouwen

de tweede stap Hallo toobuild Caffe op Hallo headnode is en vervolgens distribueren Hallo gecompileerd bibliotheken tooall Hallo worker-knooppunten. In deze stap moet u te[ssh in uw headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), volg Hallo gewoon [CaffeOnSpark buildproces](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), en hieronder vindt u toobuild CaffeOnSpark kunt gebruiken met een aantal extra stappen Hallo-script. 

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

Mogelijk moet u toodo meer dan welke documentatie Hallo van CaffeOnSpark staat. Hallo wijzigingen zijn:
- Wijzig alleen tooCPU en libatlas bepaalde hiervoor gebruiken.
- Hallo gegevenssets toohello BLOB storage, een gedeelde locatie plaatsen is dat toegankelijk tooall worker-knooppunten voor later gebruik.
- Put Hallo gecompileerd Caffe bibliotheken tooBLOB opslag en kopieert u later deze bibliotheken tooall Hallo knooppunten met behulp van script acties tooavoid extra compileertijd.


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a>Voor probleemoplossing: Een BuildException Ant is opgetreden: exec geretourneerd: 2

Wanneer u eerst probeert toobuild CaffeOnSpark, wordt soms er

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

Gewoon schone Hallo code opslagplaats door 'schone maken' uit en vervolgens uitvoeren 'Maak bouwen' lost dit probleem, zolang u de juiste afhankelijkheden Hallo hebt.

### <a name="troubleshooting-maven-repository-connection-time-out"></a>Voor probleemoplossing: Maven-opslagplaats verbindingstime-out optreedt

Soms hebt maven mij Hallo verbinding time-outfout, vergelijkbare toobelow:

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

Deze OK na een wachttijd van een paar minuten en probeer NET toorebuild Hallo code, zodat Maven mogelijk enigszins limieten Hallo verkeer van een opgegeven IP-adres.


### <a name="troubleshooting-test-failure-for-caffe"></a>Voor probleemoplossing: Fout voor Caffe testen

Waarschijnlijk ziet u een test-fout bij het uitvoeren van de laatste controle Hallo voor CaffeOnSpark, vergelijkbaar met hieronder. Dit is prabably gerelateerd aan UTF-8-codering, maar moet geen invloed op Hallo gebruik van Caffe

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a>Stap 3: Distribueert vereiste Hallo bibliotheken tooall Hallo worker-knooppunten

de volgende stap Hallo is toodistribute Hallo-bibliotheken (in feite Hallo-bibliotheken in CaffeOnSpark/caffe-openbare/distribueren/lib/en CaffeOnSpark/caffe-distri/distribueren/lib /) tooall Hallo knooppunten. In stap 2 we deze bibliotheken in BLOB storage plaatsen en in deze stap gebruiken we script acties toocopy het tooall Hallo hoofdknooppunten en worker-knooppunten.

toodo deze, eenvoudig uitvoeren van een scriptactie zoals hieronder (u moet toopoint toohello juiste locatie specifieke tooyour cluster):

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

Omdat u in stap 2, we op plaatsen Hallo BLOB-opslag die toegankelijk tooall Hallo knooppunten, in deze stap kopiëren gewoon items we deze tooall Hallo knooppunten.

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a>Stap 4: Een model Caffe opstellen en voer dit distributely

Na het uitvoeren van Hallo bovenstaande stappen Caffe is al geïnstalleerd op Hallo headnode en de goede toogo. de volgende stap Hallo is toowrite een Caffe-model. 

Caffe maakt gebruik van een 'expressieve architectuur,' wanneer een model u zojuist hebt voor het opstellen van een configuratiebestand toodefine en zonder codering helemaal (in de meeste gevallen). Dus laten we er. 

we zullen vandaag trainen Hallo-model is een voorbeeld-model voor MNIST training. Hallo MNIST database geschreven cijfers heeft een trainingset 60.000 voorbeelden en geen testset van 10.000 voorbeelden. Dit is een subset van een grotere set van NIST beschikbaar. Hallo cijfers zijn grootte genormaliseerd en in het midden van de installatiekopie van een vaste grootte. CaffeOnSpark heeft een aantal scripts toodownload Hallo gegevensset en te converteren naar de juiste notatie Hallo.

CaffeOnSpark biedt een aantal voorbeelden van de netwerk-topologieën voor MNIST training. Een goed ontwerp van splitsing Hallo netwerkarchitectuur (Hallo topologie van het Hallo-netwerk) en optimalisatie van heeft. In dit geval zijn er twee bestanden vereist: 

Hallo 'Solver '' bestand (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) wordt gebruikt voor het Hallo-optimalisatie overzien en parameter updates genereren. Bijvoorbeeld definieert of CPU of GPU wordt gebruikt, wat is er Hallo dynamiek, het aantal iteraties zal zijn, enzovoort. Ook wordt gedefinieerd welke netwerktopologie neuron moet Hallo programma gebruiken (dit is de tweede bestand Hallo we moeten). Voor meer informatie over Solver Raadpleeg te[Caffe documentatie](http://caffe.berkeleyvision.org/tutorial/solver.html).

We gebruiken CPU in plaats van GPU, moeten we voor dit voorbeeld Hallo laatste regel te wijzigen:

    # solver mode: CPU or GPU
    solver_mode: CPU

![Caffe Config](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

U kunt andere regels indien nodig wijzigen.

tweede Hallo-bestand (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) definieert hoe Hallo neuron netwerk eruit, en relevante Hallo-invoer en uitvoerbestand. Er moet ook tooupdate hello tooreflect Hallo training gegevens bestandslocatie. Wijzig hello onderdeel in lenet_memory_train_test.prototxt (u moet toopoint toohello juiste locatie specifieke tooyour cluster) te volgen:

- Hallo 'file:/Users/mridul/bigml/demodl/mnist_train_lmdb' te wijzigen "wasb: / / / projecten/machine_learning/image_dataset/mnist_train_lmdb '
- 'file:/Users/mridul/bigml/demodl/mnist_test_lmdb/' te wijzigen "wasb: / / / projecten/machine_learning/image_dataset/mnist_test_lmdb '

![Caffe Config](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

Controleer voor meer informatie over hoe toodefine netwerk Hallo Hallo [Caffe documentatie over MNIST gegevensset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)

Voor Hallo doel van deze blog gebruiken we dit eenvoudige voorbeeld van MNIST. Hallo onderstaande opdracht moet worden uitgevoerd vanaf het hoofdknooppunt Hallo van:

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

In feite wordt gedistribueerd Hallo vereist-bestanden (lenet_memory_solver.prototxt en lenet_memory_train_test.prototxt) tooeach garens container en ook relevante pad van elke Spark stuurprogramma/executor tooLD_LIBRARY_PATH, die is gedefinieerd in Hallo Hallo vorige code codefragment en punten toohello locatie met CaffeOnSpark bibliotheken. 

## <a name="monitoring-and-troubleshooting"></a>Bewaking en probleemoplossing

We gebruiken YARN clustermodus, in welk geval Hallo Spark stuurprogramma worden geplande tooan willekeurige container (en een willekeurige werkrolknooppunt) moet wordt alleen weergegeven in het Hallo console uitvoeren als:

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

Als u tooknow wat er gebeurd is wilt, moet u meestal tooget Hallo Spark van stuurprogramma-logboek met meer informatie. In dit geval moet u toogo toohello gebruikersinterface van YARN toofind Hallo relevante YARN-Logboeken. U kunt krijgen Hallo gebruikersinterface van YARN door deze URL: 

    https://yourclustername.azurehdinsight.net/yarnui
   
![GEBRUIKERSINTERFACE VAN YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

U kunt bekijken hoeveel resources worden toegewezen voor deze bepaalde toepassing op te nemen. U kunt klikken op Hallo 'Scheduler' koppeling en, ziet u dat voor deze toepassing, er zijn 9 containers die worden uitgevoerd. We vragen YARN tooprovide 8 Executor en een andere container is voor stuurprogramma-proces. 

![YARN Scheduler](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

U kunt toocheck Hallo stuurprogramma Logboeken of de logboeken van de container als er fouten zijn. Voor het stuurprogramma zich aanmeldt, kunt u Hallo toepassings-ID in de gebruikersinterface van YARN, klik op Hallo 'Logs' knop. Hallo stuurprogramma logboeken worden geschreven in stderr.

![GEBRUIKERSINTERFACE VAN YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

Bijvoorbeeld, ziet u mogelijk enkele Hallo fout hieronder van Hallo stuurprogramma zich aanmeldt, die aangeeft dat u te veel Executor toewijzen.

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

Soms Hallo probleem kan zich voordoen in Executor in plaats van stuurprogramma's. In dit geval moet u toocheck Hallo container Logboeken. U kunt altijd Hallo container logboeken ophalen en vervolgens Hallo mislukte container. Bijvoorbeeld mogelijk voldoet deze fout aan wanneer Caffe wordt uitgevoerd.

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

In dit geval moet u tooget Hallo mislukt container-ID (in Hallo boven het geval is, is het container_1485916338528_0008_05_000005). Vervolgens moet u toorun 

    yarn logs -containerId container_1485916338528_0008_03_000005

van Hallo headnode. Nadat u hebt gecontroleerd container mislukt, wordt dit veroorzaakt door met GPU-modus (waarbij u gebruik CPU-modus in plaats daarvan) in lenet_memory_solver.prototxt.

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a>Ophalen van resultaten

Aangezien we 8 Executor toewijzen wilt en netwerktopologie Hallo eenvoudig is, neemt het ongeveer 30 minuten toorun Hallo resultaat. Vanaf de opdrachtregel hello, ziet u dat we plaatst u Hallo model toowasb:///mnist.model, en Hallo resultaten tooa map met de naam wasb: / / / mnist_features_result.

U kunt Hallo resultaten krijgen door te voeren

    hadoop fs -cat hdfs:///mnist_features_result/*

en Hallo resultaat lijkt op:

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

Hallo SampleID vertegenwoordigt Hallo-ID in Hallo MNIST gegevensset en Hallo-label is Hallo getal dat Hallo model identificeert.


## <a name="conclusion"></a>Conclusie

U hebt in deze documentatie tooinstall CaffeOnSpark geprobeerd met het uitvoeren van een eenvoudig voorbeeld. HDInsight is een volledig beheerde gedistribueerde compute cloudplatform, Hallo beste plaats voor het uitvoeren van machine learning en geavanceerde analyses werkbelastingen op grote gegevensset en voor gedistribueerde grondige learning, kunt u Caffe gebruiken in HDInsight Spark tooperform grondige kennis taken.


## <a name="seealso"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenario's
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)

