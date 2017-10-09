---
title: 'Azure Cosmos DB: Grafiek analyses uitvoeren met behulp van Spark en Apache TinkerPop Gremlin | Microsoft Docs'
description: Dit artikel bevat instructies voor het instellen en uitvoeren van grafiek analytics en parallelle berekeningen in Azure Cosmos DB met Spark en TinkerPop SparkGraphComputer.
services: cosmosdb
documentationcenter: 
author: khdang
manager: shireest
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: gremlin
ms.topic: article
ms.date: 06/05/2017
ms.author: khdang
ms.openlocfilehash: 0be5c9b12cdba4a428c809d00e1e68785a9ec1ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="8a596-103">Azure Cosmos DB: Grafiek analyses uitvoeren met behulp van Spark en Apache TinkerPop Gremlin</span><span class="sxs-lookup"><span data-stu-id="8a596-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="8a596-104">[Azure Cosmos DB](introduction.md) is Hallo globaal gedistribueerd en modellen database-service van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8a596-104">[Azure Cosmos DB](introduction.md) is hello globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="8a596-105">U kunt maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van de algemene distributie en het horizontale schaal mogelijkheden Hallo Hallo kern van Azure DB die Cosmos profiteren.</span><span class="sxs-lookup"><span data-stu-id="8a596-105">You can create and query document, key/value, and graph databases, all of which benefit from hello global-distribution and horizontal-scale capabilities at hello core of Azure Cosmos DB.</span></span> <span data-ttu-id="8a596-106">Azure Cosmos DB ondersteunt online transactieverwerking (OLTP) grafiek werkbelastingen die gebruikmaken van [Apache TinkerPop Gremlin](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8a596-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="8a596-107">[Spark](http://spark.apache.org/) is een Apache Software Foundation-project dat gericht op het verwerken van gegevens voor algemene doeleinden online analytical processing (OLAP).</span><span class="sxs-lookup"><span data-stu-id="8a596-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="8a596-108">Spark biedt een hybride in-memory/op basis van schijven gedistribueerde computermodel dat vergelijkbare toohello Hadoop MapReduce-model.</span><span class="sxs-lookup"><span data-stu-id="8a596-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar toohello Hadoop MapReduce model.</span></span> <span data-ttu-id="8a596-109">U kunt een Apache Spark in Hallo cloud implementeren met behulp van [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="8a596-109">You can deploy Apache Spark in hello cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="8a596-110">U kunt door een combinatie van Azure DB die Cosmos en Spark OLTP- en OLAP-werkbelastingen uitvoeren wanneer u Gremlin gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8a596-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="8a596-111">In dit artikel snel starten laat zien hoe toorun Gremlin query's op basis van Azure DB die Cosmos in een Azure HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="8a596-111">This quick-start article demonstrates how toorun Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a596-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8a596-112">Prerequisites</span></span>

<span data-ttu-id="8a596-113">Voordat u dit voorbeeld uitvoeren kunt, hebt u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="8a596-113">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="8a596-114">Azure HDInsight Spark-cluster 2.0</span><span class="sxs-lookup"><span data-stu-id="8a596-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="8a596-115">JDK 1.8 + (als u geen JDK, voert u `apt-get install default-jdk`.)</span><span class="sxs-lookup"><span data-stu-id="8a596-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="8a596-116">Maven (als u geen Maven, voert u `apt-get install maven`.)</span><span class="sxs-lookup"><span data-stu-id="8a596-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="8a596-117">Een Azure-abonnement ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="8a596-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="8a596-118">Voor informatie over het tooset van een Azure HDInsight Spark-cluster, Zie [inrichten van HDInsight-clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="8a596-118">For information about how tooset up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="8a596-119">Een Azure DB die Cosmos-databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="8a596-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="8a596-120">Maak eerst een databaseaccount Hello Graph API door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="8a596-120">First, create a database account with hello Graph API by doing hello following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="8a596-121">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="8a596-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="8a596-122">Apache TinkerPop ophalen</span><span class="sxs-lookup"><span data-stu-id="8a596-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="8a596-123">Apache TinkerPop ophalen door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="8a596-123">Get Apache TinkerPop by doing hello following:</span></span>

1. <span data-ttu-id="8a596-124">Externe toohello hoofdknooppunt van het HDInsight-cluster Hallo `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="8a596-124">Remote toohello master node of hello HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="8a596-125">Hallo TinkerPop3 broncode klonen, lokaal bouwen en installeer deze tooMaven cache.</span><span class="sxs-lookup"><span data-stu-id="8a596-125">Clone hello TinkerPop3 source code, build it locally, and install it tooMaven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="8a596-126">Hallo Spark-Gremlin invoegtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="8a596-126">Install hello Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="8a596-127">a.</span><span class="sxs-lookup"><span data-stu-id="8a596-127">a.</span></span> <span data-ttu-id="8a596-128">Hallo-installatie van de invoegtoepassing hello wordt verwerkt door gedeeltelijk.</span><span class="sxs-lookup"><span data-stu-id="8a596-128">hello installation of hello plug-in is handled by Grape.</span></span> <span data-ttu-id="8a596-129">Hallo-opslagplaatsen informatie voor gedeeltelijk vullen zodat het kan worden gedownload Hallo invoegtoepassing en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="8a596-129">Populate hello repositories information for Grape so it can download hello plug-in and its dependencies.</span></span> 

      <span data-ttu-id="8a596-130">Hallo druivenmost-configuratiebestand maken als het is niet aanwezig zijn bij `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="8a596-130">Create hello grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="8a596-131">Gebruik Hallo volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="8a596-131">Use hello following settings:</span></span>

    ```xml
    <ivysettings>
    <settings defaultResolver="downloadGrapes"/>
    <resolvers>
        <chain name="downloadGrapes">
        <filesystem name="cachedGrapes">
            <ivy pattern="${user.home}/.groovy/grapes/[organisation]/[module]/ivy-[revision].xml"/>
            <artifact pattern="${user.home}/.groovy/grapes/[organisation]/[module]/[type]s/[artifact]-[revision].[ext]"/>
        </filesystem>
        <ibiblio name="codehaus" root="http://repository.codehaus.org/" m2compatible="true"/>
        <ibiblio name="central" root="http://central.maven.org/maven2/" m2compatible="true"/>
        <ibiblio name="jitpack" root="https://jitpack.io" m2compatible="true"/>
        <ibiblio name="java.net2" root="http://download.java.net/maven/2/" m2compatible="true"/>
        <ibiblio name="apache-snapshots" root="http://repository.apache.org/snapshots/" m2compatible="true"/>
        <ibiblio name="local" root="file:${user.home}/.m2/repository/" m2compatible="true"/>
        </chain>
    </resolvers>
    </ivysettings>
    ``` 

    <span data-ttu-id="8a596-132">b.</span><span class="sxs-lookup"><span data-stu-id="8a596-132">b.</span></span> <span data-ttu-id="8a596-133">Start de console Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="8a596-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="8a596-134">c.</span><span class="sxs-lookup"><span data-stu-id="8a596-134">c.</span></span> <span data-ttu-id="8a596-135">Hallo Spark-Gremlin invoegtoepassing installeren met versie 3.3.0-SNAPSHOT die u in de vorige stappen Hallo gebouwd:</span><span class="sxs-lookup"><span data-stu-id="8a596-135">Install hello Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in hello previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart hello console toouse [tinkerpop.spark]
    gremlin> :q
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :plugin use tinkerpop.spark
    ==>tinkerpop.spark activated
    ```

4. <span data-ttu-id="8a596-136">Controleer of de toosee `Hadoop-Gremlin` is geactiveerd met een `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="8a596-136">Check toosee whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="8a596-137">Schakel deze invoegtoepassing zijn, omdat deze Hallo Spark Gremlin invoegtoepassing verstoren kan `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="8a596-137">Disable this plug-in, because it could interfere with hello Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="8a596-138">TinkerPop3 afhankelijkheden voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8a596-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="8a596-139">Wanneer u TinkerPop3 in de vorige stap hello gemaakt, Hallo proces alle afhankelijkheden van de jar ook voor Spark en Hadoop in de doelmap Hallo opgehaald.</span><span class="sxs-lookup"><span data-stu-id="8a596-139">When you built TinkerPop3 in hello previous step, hello process also pulled all jar dependencies for Spark and Hadoop in hello target directory.</span></span> <span data-ttu-id="8a596-140">Gebruik Hallo potten die vooraf zijn geïnstalleerd met HDI en ophalen van extra afhankelijkheden alleen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="8a596-140">Use hello jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="8a596-141">Ga toohello Gremlin Console doelmap op `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="8a596-141">Go toohello Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="8a596-142">Verplaats alle potten onder `ext/` te`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="8a596-142">Move all jars under `ext/` too`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="8a596-143">Verwijder alle bibliotheken onder jar `lib/` dat niet in Hallo lijst volgt:</span><span class="sxs-lookup"><span data-stu-id="8a596-143">Remove all jar libraries under `lib/` that are not in hello following list:</span></span>

    ```bash
    # TinkerPop3
    gremlin-console-3.3.0-SNAPSHOT.jar
    gremlin-core-3.3.0-SNAPSHOT.jar       
    gremlin-groovy-3.3.0-SNAPSHOT.jar     
    gremlin-shaded-3.3.0-SNAPSHOT.jar     
    hadoop-gremlin-3.3.0-SNAPSHOT.jar     
    spark-gremlin-3.3.0-SNAPSHOT.jar      
    tinkergraph-gremlin-3.3.0-SNAPSHOT.jar

    # Gremlin depedencies
    asm-3.2.jar                                
    avro-1.7.4.jar                             
    caffeine-2.3.1.jar                         
    cglib-2.2.1-v20090111.jar                  
    gbench-0.4.3-groovy-2.4.jar                
    gprof-0.3.1-groovy-2.4.jar                 
    groovy-2.4.9-indy.jar                      
    groovy-2.4.9.jar                           
    groovy-console-2.4.9.jar                   
    groovy-groovysh-2.4.9-indy.jar             
    groovy-json-2.4.9-indy.jar                 
    groovy-jsr223-2.4.9-indy.jar               
    groovy-sql-2.4.9-indy.jar                  
    groovy-swing-2.4.9.jar                     
    groovy-templates-2.4.9.jar                 
    groovy-xml-2.4.9.jar                       
    hadoop-yarn-server-nodemanager-2.7.2.jar   
    hppc-0.7.1.jar                             
    javatuples-1.2.jar                         
    jaxb-impl-2.2.3-1.jar                      
    jbcrypt-0.4.jar                            
    jcabi-log-0.14.jar                         
    jcabi-manifests-1.1.jar                    
    jersey-core-1.9.jar                        
    jersey-guice-1.9.jar                       
    jersey-json-1.9.jar                        
    jettison-1.1.jar                           
    scalatest_2.11-2.2.6.jar                   
    servlet-api-2.5.jar                        
    snakeyaml-1.15.jar                         
    unused-1.0.0.jar                           
    xml-apis-1.3.04.jar                        
    ```

## <a name="get-hello-azure-cosmos-db-spark-connector"></a><span data-ttu-id="8a596-144">Hello Azure Cosmos DB Spark connector ophalen</span><span class="sxs-lookup"><span data-stu-id="8a596-144">Get hello Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="8a596-145">Hello Azure Cosmos DB Spark connector ophalen `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` en Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` van [Azure DB Spark Cosmos-Connector op GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="8a596-145">Get hello Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="8a596-146">U kunt ook kunt u deze lokaal.</span><span class="sxs-lookup"><span data-stu-id="8a596-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="8a596-147">Omdat de meest recente versie Hallo van Spark Gremlin is gebouwd met Spark 1.6.1 en niet compatibel met Spark 2.0.2 is, momenteel in hello Azure Cosmos DB Spark-connector gebruikt wordt, kunt u Hallo nieuwste TinkerPop3 code bouwen en Hallo potten handmatig installeren.</span><span class="sxs-lookup"><span data-stu-id="8a596-147">Because hello latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in hello Azure Cosmos DB Spark connector, you can build hello latest TinkerPop3 code and install hello jars manually.</span></span> <span data-ttu-id="8a596-148">Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="8a596-148">Do hello following:</span></span>

    <span data-ttu-id="8a596-149">a.</span><span class="sxs-lookup"><span data-stu-id="8a596-149">a.</span></span> <span data-ttu-id="8a596-150">Kloon hello Azure Cosmos DB Spark-connector.</span><span class="sxs-lookup"><span data-stu-id="8a596-150">Clone hello Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="8a596-151">b.</span><span class="sxs-lookup"><span data-stu-id="8a596-151">b.</span></span> <span data-ttu-id="8a596-152">Bouw TinkerPop3 (in de vorige stappen hebt).</span><span class="sxs-lookup"><span data-stu-id="8a596-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="8a596-153">Installeer alle TinkerPop 3.3.0-SNAPSHOT potten lokaal.</span><span class="sxs-lookup"><span data-stu-id="8a596-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="8a596-154">c.</span><span class="sxs-lookup"><span data-stu-id="8a596-154">c.</span></span> <span data-ttu-id="8a596-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` te`3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="8a596-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` too`3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="8a596-156">d.</span><span class="sxs-lookup"><span data-stu-id="8a596-156">d.</span></span> <span data-ttu-id="8a596-157">Bij het maken van Maven.</span><span class="sxs-lookup"><span data-stu-id="8a596-157">Build with Maven.</span></span> <span data-ttu-id="8a596-158">Hallo benodigde potten worden geplaatst `target` en `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="8a596-158">hello needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="8a596-159">Genoemde potten tooa lokale map op de kopie Hallo ~ / azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="8a596-159">Copy hello previously mentioned jars tooa local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a><span data-ttu-id="8a596-160">Hallo afhankelijkheden toohello Spark worker-knooppunten distribueren</span><span class="sxs-lookup"><span data-stu-id="8a596-160">Distribute hello dependencies toohello Spark worker nodes</span></span> 

1. <span data-ttu-id="8a596-161">Omdat Hallo transformatie van grafiekgegevens is afhankelijk van TinkerPop3, moet u distribueren Hallo gerelateerde afhankelijkheden tooall Spark worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="8a596-161">Because hello transformation of graph data depends on TinkerPop3, you must distribute hello related dependencies tooall Spark worker nodes.</span></span>

2. <span data-ttu-id="8a596-162">Kopiëren Hallo genoemde Gremlin afhankelijkheden, Hallo CosmosDB Spark connector jar en CosmosDB Java SDK toohello worker-knooppunten door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="8a596-162">Copy hello previously mentioned Gremlin dependencies, hello CosmosDB Spark connector jar, and CosmosDB Java SDK toohello worker nodes by doing hello following:</span></span>

    <span data-ttu-id="8a596-163">a.</span><span class="sxs-lookup"><span data-stu-id="8a596-163">a.</span></span> <span data-ttu-id="8a596-164">Kopieer alle Hallo potten in `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="8a596-164">Copy all hello jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="8a596-165">b.</span><span class="sxs-lookup"><span data-stu-id="8a596-165">b.</span></span> <span data-ttu-id="8a596-166">Hallo-lijst met alle Spark worker-knooppunten, kunt u vinden op Ambari-Dashboard in Hallo `Spark2 Clients` lijst in Hallo `Spark2` sectie.</span><span class="sxs-lookup"><span data-stu-id="8a596-166">Get hello list of all Spark worker nodes, which you can find on Ambari Dashboard, in hello `Spark2 Clients` list in hello `Spark2` section.</span></span>

    <span data-ttu-id="8a596-167">c.</span><span class="sxs-lookup"><span data-stu-id="8a596-167">c.</span></span> <span data-ttu-id="8a596-168">Kopieer deze directory tooeach Hallo knooppunten.</span><span class="sxs-lookup"><span data-stu-id="8a596-168">Copy that directory tooeach of hello nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a><span data-ttu-id="8a596-169">Hallo omgevingsvariabelen instellen</span><span class="sxs-lookup"><span data-stu-id="8a596-169">Set up hello environment variables</span></span>

1. <span data-ttu-id="8a596-170">Hallo HDP versie vinden van Hallo Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="8a596-170">Find hello HDP version of hello Spark cluster.</span></span> <span data-ttu-id="8a596-171">De mapnaam Hallo onder is `/usr/hdp/` (bijvoorbeeld 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="8a596-171">It is hello directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="8a596-172">Stel hdp.version voor alle knooppunten.</span><span class="sxs-lookup"><span data-stu-id="8a596-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="8a596-173">In de Ambari-Dashboard, gaat u te**YARN sectie** > **Configs** > **Geavanceerd**, en vervolgens Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="8a596-173">In Ambari Dashboard, go too**YARN section** > **Configs** > **Advanced**, and then do hello following:</span></span> 
 
    <span data-ttu-id="8a596-174">a.</span><span class="sxs-lookup"><span data-stu-id="8a596-174">a.</span></span> <span data-ttu-id="8a596-175">In `Custom yarn-site`, een nieuwe eigenschap toevoegen `hdp.version` met Hallo waarde Hallo HDP versie op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="8a596-175">In `Custom yarn-site`, add a new property `hdp.version` with hello value of hello HDP version on hello master node.</span></span> 
     
    <span data-ttu-id="8a596-176">b.</span><span class="sxs-lookup"><span data-stu-id="8a596-176">b.</span></span> <span data-ttu-id="8a596-177">Hallo configuraties opslaan.</span><span class="sxs-lookup"><span data-stu-id="8a596-177">Save hello configurations.</span></span> <span data-ttu-id="8a596-178">Er zijn waarschuwingen die u kunt negeren.</span><span class="sxs-lookup"><span data-stu-id="8a596-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="8a596-179">c.</span><span class="sxs-lookup"><span data-stu-id="8a596-179">c.</span></span> <span data-ttu-id="8a596-180">Hallo YARN en Oozie-services opnieuw starten als Hallo meldingspictogrammen geven.</span><span class="sxs-lookup"><span data-stu-id="8a596-180">Restart hello YARN and Oozie services as hello notification icons indicate.</span></span>

3. <span data-ttu-id="8a596-181">Set Hallo omgevingsvariabelen op Hallo hoofdknooppunt (vervangen Hallo waarden naar gelang van toepassing) te volgen:</span><span class="sxs-lookup"><span data-stu-id="8a596-181">Set hello following environment variables on hello master node (replace hello values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a><span data-ttu-id="8a596-182">Configuratie van de grafiek Hallo voorbereiden</span><span class="sxs-lookup"><span data-stu-id="8a596-182">Prepare hello graph configuration</span></span>

1. <span data-ttu-id="8a596-183">Een configuratiebestand maken door hello Azure Cosmos DB verbindingsparameters en instellingen Spark en plaatsen op `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="8a596-183">Create a configuration file with hello Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

    ```
    gremlin.graph=org.apache.tinkerpop.gremlin.hadoop.structure.HadoopGraph
    gremlin.hadoop.jarsInDistributedCache=true
    gremlin.hadoop.defaultGraphComputer=org.apache.tinkerpop.gremlin.spark.process.computer.SparkGraphComputer

    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    gremlin.hadoop.graphWriter=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBOutputRDD

    ####################################
    # SparkGraphComputer Configuration #
    ####################################
    spark.master=yarn
    spark.executor.memory=3g
    spark.executor.instances=6
    spark.serializer=org.apache.spark.serializer.KryoSerializer
    spark.kryo.registrator=org.apache.tinkerpop.gremlin.spark.structure.io.gryo.GryoRegistrator
    gremlin.spark.persistContext=true

    # Classpath for hello driver and executors
    spark.driver.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    spark.executor.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    
    ######################################
    # DocumentDB Spark connector         #
    ######################################
    spark.documentdb.connectionMode=Gateway
    spark.documentdb.schema_samplingratio=1.0
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    spark.documentdb.preferredRegions=FILLIN
    ```

2. <span data-ttu-id="8a596-184">Update Hallo `spark.driver.extraClassPath` en `spark.executor.extraClassPath` tooinclude Hallo-map van Hallo potten die u in de vorige stap hello, verdeeld in dit geval `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="8a596-184">Update hello `spark.driver.extraClassPath` and `spark.executor.extraClassPath` tooinclude hello directory of hello jars that you distributed in hello previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="8a596-185">Hallo volgende details voor Azure Cosmos DB bieden:</span><span class="sxs-lookup"><span data-stu-id="8a596-185">Provide hello following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a><span data-ttu-id="8a596-186">Hallo TinkerPop grafiek laden en sla het tooAzure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="8a596-186">Load hello TinkerPop graph, and save it tooAzure Cosmos DB</span></span>
<span data-ttu-id="8a596-187">toodemonstrate hoe toopersist een grafiek naar Azure Cosmos DB, in dit voorbeeld gebruikt Hallo TinkerPop vooraf gedefinieerde TinkerPop moderne grafiek.</span><span class="sxs-lookup"><span data-stu-id="8a596-187">toodemonstrate how toopersist a graph into Azure Cosmos DB, this example uses hello TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="8a596-188">Hallo grafiek wordt opgeslagen in de indeling Kryo en dit wordt geleverd in Hallo TinkerPop opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="8a596-188">hello graph is stored in Kryo format, and it's provided in hello TinkerPop repository.</span></span>

1. <span data-ttu-id="8a596-189">Omdat u Gremlin in de YARN-modus uitvoert, moet u Hallo grafiekgegevens in Hallo Hadoop-bestandssysteem beschikbaar maken.</span><span class="sxs-lookup"><span data-stu-id="8a596-189">Because you are running Gremlin in YARN mode, you must make hello graph data available in hello Hadoop file system.</span></span> <span data-ttu-id="8a596-190">Gebruik Hallo volgende opdrachten toomake een map en Hallo lokale graph-bestand kopiëren in de App.</span><span class="sxs-lookup"><span data-stu-id="8a596-190">Use hello following commands toomake a directory and copy hello local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="8a596-191">Tijdelijk bijwerken Hallo `gremlin-spark.properties` bestand toouse `GryoInputFormat` tooread Hallo grafiek.</span><span class="sxs-lookup"><span data-stu-id="8a596-191">Temporarily update hello `gremlin-spark.properties` file toouse `GryoInputFormat` tooread hello graph.</span></span> <span data-ttu-id="8a596-192">Ook duiden op `inputLocation` als Hallo map u maakt, zoals Hallo volgende in:</span><span class="sxs-lookup"><span data-stu-id="8a596-192">Also indicate `inputLocation` as hello directory you create, as in hello following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="8a596-193">Start Gremlin-Console en maak vervolgens Hallo berekening stappen toopersist toohello geconfigureerd Azure Cosmos DB gegevensverzameling te volgen:</span><span class="sxs-lookup"><span data-stu-id="8a596-193">Start Gremlin Console, and then create hello following computation steps toopersist data toohello configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="8a596-194">a.</span><span class="sxs-lookup"><span data-stu-id="8a596-194">a.</span></span> <span data-ttu-id="8a596-195">Hallo-grafiek maken `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="8a596-195">Create hello graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="8a596-196">b.</span><span class="sxs-lookup"><span data-stu-id="8a596-196">b.</span></span> <span data-ttu-id="8a596-197">SparkGraphComputer gebruiken om te schrijven `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="8a596-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[gryoinputformat->documentdboutputrdd]
    gremlin> hg = graph.
                compute(SparkGraphComputer.class).
                result(GraphComputer.ResultGraph.NEW).
                persist(GraphComputer.Persist.EDGES).
                program(TraversalVertexProgram.build().
                    traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)), "gremlin-groovy", "g.V()").
                    create(graph)).
                submit().
                get() 
    ==>result[hadoopgraph[documentdbinputrdd->documentdboutputrdd],memory[size:1]]
    ```

4. <span data-ttu-id="8a596-198">U kunt controleren die gegevens zijn Hallo persistent tooAzure Cosmos DB van Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="8a596-198">From Data Explorer, you can verify that hello data has been persisted tooAzure Cosmos DB.</span></span>

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="8a596-199">Hallo grafiek uit Azure Cosmos DB laden en Gremlin query's uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8a596-199">Load hello graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="8a596-200">tooload hello grafiek bewerken `gremlin-spark.properties` tooset `graphReader` te`DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="8a596-200">tooload hello graph, edit `gremlin-spark.properties` tooset `graphReader` too`DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="8a596-201">Hallo grafiek laden, bladeren door het Hallo-gegevens en Gremlin query's uitvoeren met het door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="8a596-201">Load hello graph, traverse hello data, and run Gremlin queries with it by doing hello following:</span></span>

    <span data-ttu-id="8a596-202">a.</span><span class="sxs-lookup"><span data-stu-id="8a596-202">a.</span></span> <span data-ttu-id="8a596-203">Hallo Gremlin Console starten `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="8a596-203">Start hello Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="8a596-204">b.</span><span class="sxs-lookup"><span data-stu-id="8a596-204">b.</span></span> <span data-ttu-id="8a596-205">Hallo-grafiek maken met Hallo configuratie `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="8a596-205">Create hello graph with hello configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="8a596-206">c.</span><span class="sxs-lookup"><span data-stu-id="8a596-206">c.</span></span> <span data-ttu-id="8a596-207">Een grafiek traversal maken met SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="8a596-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="8a596-208">d.</span><span class="sxs-lookup"><span data-stu-id="8a596-208">d.</span></span> <span data-ttu-id="8a596-209">Voer Hallo Gremlin grafiek query's te volgen:</span><span class="sxs-lookup"><span data-stu-id="8a596-209">Run hello following Gremlin graph queries:</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[documentdbinputrdd->documentdboutputrdd]
    gremlin> g = graph.traversal().withComputer(SparkGraphComputer)
    ==>graphtraversalsource[hadoopgraph[documentdbinputrdd->documentdboutputrdd], sparkgraphcomputer]
    gremlin> g.V().count()
    ==>6
    gremlin> g.E().count()
    ==>6
    gremlin> g.V(1).out().values('name')
    ==>josh
    ==>vadas
    ==>lop
    gremlin> g.V().hasLabel('person').coalesce(values('nickname'), values('name'))
    ==>josh
    ==>peter
    ==>vadas
    ==>marko
    gremlin> g.V().hasLabel('person').
            choose(values('name')).
                option('marko', values('age')).
                option('josh', values('name')).
                option('vadas', valueMap()).
                option('peter', label())
    ==>josh
    ==>person
    ==>[name:[vadas],age:[27]]
    ==>29
    ```

> [!NOTE]
> <span data-ttu-id="8a596-210">toosee meer gedetailleerde logboekregistratie Hallo logboekniveau ingesteld in `conf/log4j-console.properties` tooa uitgebreidere niveau.</span><span class="sxs-lookup"><span data-stu-id="8a596-210">toosee more detailed logging, set hello log level in `conf/log4j-console.properties` tooa more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="8a596-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a596-211">Next steps</span></span>

<span data-ttu-id="8a596-212">U hebt geleerd hoe toowork met grafieken door Azure Cosmos DB en Spark te combineren in dit artikel snel starten.</span><span class="sxs-lookup"><span data-stu-id="8a596-212">In this quick-start article, you've learned how toowork with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
