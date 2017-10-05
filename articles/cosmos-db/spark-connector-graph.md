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
ms.openlocfilehash: 27c4d945e418b130c68cfde845571eb93658101e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="fff2a-103">Azure Cosmos DB: Grafiek analyses uitvoeren met behulp van Spark en Apache TinkerPop Gremlin</span><span class="sxs-lookup"><span data-stu-id="fff2a-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="fff2a-104">[Azure Cosmos DB](introduction.md) is de globaal gedistribueerd en modellen database-service van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fff2a-104">[Azure Cosmos DB](introduction.md) is the globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="fff2a-105">U kunt maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van de mogelijkheden voor algemene distributie en horizontale schaal de kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="fff2a-105">You can create and query document, key/value, and graph databases, all of which benefit from the global-distribution and horizontal-scale capabilities at the core of Azure Cosmos DB.</span></span> <span data-ttu-id="fff2a-106">Azure Cosmos DB ondersteunt online transactieverwerking (OLTP) grafiek werkbelastingen die gebruikmaken van [Apache TinkerPop Gremlin](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fff2a-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="fff2a-107">[Spark](http://spark.apache.org/) is een Apache Software Foundation-project dat gericht op het verwerken van gegevens voor algemene doeleinden online analytical processing (OLAP).</span><span class="sxs-lookup"><span data-stu-id="fff2a-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="fff2a-108">Spark biedt een hybride in-memory/op basis van schijven gedistribueerde computermodel die vergelijkbaar is met het Hadoop MapReduce-model.</span><span class="sxs-lookup"><span data-stu-id="fff2a-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar to the Hadoop MapReduce model.</span></span> <span data-ttu-id="fff2a-109">U kunt een Apache Spark in de cloud implementeren met behulp van [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="fff2a-109">You can deploy Apache Spark in the cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="fff2a-110">U kunt door een combinatie van Azure DB die Cosmos en Spark OLTP- en OLAP-werkbelastingen uitvoeren wanneer u Gremlin gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fff2a-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="fff2a-111">In dit artikel snel starten laat zien hoe Gremlin query's uitvoeren op Azure Cosmos DB op een Azure HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="fff2a-111">This quick-start article demonstrates how to run Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fff2a-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fff2a-112">Prerequisites</span></span>

<span data-ttu-id="fff2a-113">Voordat u met dit voorbeeld aan de slag gaat, moet u aan de volgende vereisten voldoen:</span><span class="sxs-lookup"><span data-stu-id="fff2a-113">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="fff2a-114">Azure HDInsight Spark-cluster 2.0</span><span class="sxs-lookup"><span data-stu-id="fff2a-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="fff2a-115">JDK 1.8 + (als u geen JDK, voert u `apt-get install default-jdk`.)</span><span class="sxs-lookup"><span data-stu-id="fff2a-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="fff2a-116">Maven (als u geen Maven, voert u `apt-get install maven`.)</span><span class="sxs-lookup"><span data-stu-id="fff2a-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="fff2a-117">Een Azure-abonnement ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="fff2a-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="fff2a-118">Zie voor meer informatie over het instellen van een Azure HDInsight Spark-cluster [inrichten van HDInsight-clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="fff2a-118">For information about how to set up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="fff2a-119">Een Azure DB die Cosmos-databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="fff2a-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="fff2a-120">Maak eerst een databaseaccount met de Graph API als volgt:</span><span class="sxs-lookup"><span data-stu-id="fff2a-120">First, create a database account with the Graph API by doing the following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="fff2a-121">Een verzameling toevoegen</span><span class="sxs-lookup"><span data-stu-id="fff2a-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="fff2a-122">Apache TinkerPop ophalen</span><span class="sxs-lookup"><span data-stu-id="fff2a-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="fff2a-123">Apache TinkerPop ophalen door het volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="fff2a-123">Get Apache TinkerPop by doing the following:</span></span>

1. <span data-ttu-id="fff2a-124">Extern naar het hoofdknooppunt van het HDInsight-cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-124">Remote to the master node of the HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="fff2a-125">De broncode TinkerPop3 klonen, lokaal bouwen en installeer deze met Maven-cache.</span><span class="sxs-lookup"><span data-stu-id="fff2a-125">Clone the TinkerPop3 source code, build it locally, and install it to Maven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="fff2a-126">De Spark-Gremlin invoegtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="fff2a-126">Install the Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="fff2a-127">a.</span><span class="sxs-lookup"><span data-stu-id="fff2a-127">a.</span></span> <span data-ttu-id="fff2a-128">De installatie van de invoegtoepassing wordt verwerkt door gedeeltelijk.</span><span class="sxs-lookup"><span data-stu-id="fff2a-128">The installation of the plug-in is handled by Grape.</span></span> <span data-ttu-id="fff2a-129">Vul de informatie opslagplaatsen voor gedeeltelijk zodat het kan worden gedownload de invoegtoepassing en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="fff2a-129">Populate the repositories information for Grape so it can download the plug-in and its dependencies.</span></span> 

      <span data-ttu-id="fff2a-130">Het druivensap configuratiebestand maken als het is niet aanwezig zijn bij `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-130">Create the grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="fff2a-131">Gebruik de volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="fff2a-131">Use the following settings:</span></span>

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

    <span data-ttu-id="fff2a-132">b.</span><span class="sxs-lookup"><span data-stu-id="fff2a-132">b.</span></span> <span data-ttu-id="fff2a-133">Start de console Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="fff2a-134">c.</span><span class="sxs-lookup"><span data-stu-id="fff2a-134">c.</span></span> <span data-ttu-id="fff2a-135">De Spark-Gremlin invoegtoepassing installeren met versie 3.3.0-SNAPSHOT die u in de vorige stappen hebt gebouwd:</span><span class="sxs-lookup"><span data-stu-id="fff2a-135">Install the Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in the previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart the console to use [tinkerpop.spark]
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

4. <span data-ttu-id="fff2a-136">Controleer of `Hadoop-Gremlin` is geactiveerd met een `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-136">Check to see whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="fff2a-137">Schakel deze invoegtoepassing zijn, omdat dit ertoe dat de invoegtoepassing Spark-Gremlin leiden kan `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-137">Disable this plug-in, because it could interfere with the Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="fff2a-138">TinkerPop3 afhankelijkheden voorbereiden</span><span class="sxs-lookup"><span data-stu-id="fff2a-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="fff2a-139">Wanneer u TinkerPop3 in de vorige stap hebt gemaakt, het proces alle afhankelijkheden van de jar ook voor Spark en Hadoop in de doelmap opgehaald.</span><span class="sxs-lookup"><span data-stu-id="fff2a-139">When you built TinkerPop3 in the previous step, the process also pulled all jar dependencies for Spark and Hadoop in the target directory.</span></span> <span data-ttu-id="fff2a-140">Gebruik de potten die vooraf zijn geïnstalleerd met HDI en ophalen van extra afhankelijkheden alleen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="fff2a-140">Use the jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="fff2a-141">Ga naar de doelmap Gremlin Console op `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-141">Go to the Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="fff2a-142">Verplaats alle potten onder `ext/` naar `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-142">Move all jars under `ext/` to `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="fff2a-143">Verwijder alle bibliotheken onder jar `lib/` die niet zijn opgenomen in de volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="fff2a-143">Remove all jar libraries under `lib/` that are not in the following list:</span></span>

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

## <a name="get-the-azure-cosmos-db-spark-connector"></a><span data-ttu-id="fff2a-144">Ophalen van de Azure Cosmos DB Spark-connector</span><span class="sxs-lookup"><span data-stu-id="fff2a-144">Get the Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="fff2a-145">Ophalen van de connector Azure Cosmos DB Spark `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` en Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` van [Azure DB Spark Cosmos-Connector op GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="fff2a-145">Get the Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="fff2a-146">U kunt ook kunt u deze lokaal.</span><span class="sxs-lookup"><span data-stu-id="fff2a-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="fff2a-147">Omdat de nieuwste versie van Spark Gremlin is gebouwd met Spark 1.6.1 en niet compatibel met Spark 2.0.2, die momenteel in de Azure Cosmos DB Spark-connector wordt gebruikt is, kunt u de meest recente TinkerPop3 code bouwen en de potten handmatig installeren.</span><span class="sxs-lookup"><span data-stu-id="fff2a-147">Because the latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in the Azure Cosmos DB Spark connector, you can build the latest TinkerPop3 code and install the jars manually.</span></span> <span data-ttu-id="fff2a-148">Ga als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="fff2a-148">Do the following:</span></span>

    <span data-ttu-id="fff2a-149">a.</span><span class="sxs-lookup"><span data-stu-id="fff2a-149">a.</span></span> <span data-ttu-id="fff2a-150">Kloon van de Azure Cosmos DB Spark-connector.</span><span class="sxs-lookup"><span data-stu-id="fff2a-150">Clone the Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="fff2a-151">b.</span><span class="sxs-lookup"><span data-stu-id="fff2a-151">b.</span></span> <span data-ttu-id="fff2a-152">Bouw TinkerPop3 (in de vorige stappen hebt).</span><span class="sxs-lookup"><span data-stu-id="fff2a-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="fff2a-153">Installeer alle TinkerPop 3.3.0-SNAPSHOT potten lokaal.</span><span class="sxs-lookup"><span data-stu-id="fff2a-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="fff2a-154">c.</span><span class="sxs-lookup"><span data-stu-id="fff2a-154">c.</span></span> <span data-ttu-id="fff2a-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` naar `3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` to `3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="fff2a-156">d.</span><span class="sxs-lookup"><span data-stu-id="fff2a-156">d.</span></span> <span data-ttu-id="fff2a-157">Bij het maken van Maven.</span><span class="sxs-lookup"><span data-stu-id="fff2a-157">Build with Maven.</span></span> <span data-ttu-id="fff2a-158">De benodigde potten worden geplaatst `target` en `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-158">The needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="fff2a-159">De eerder genoemde potten kopiëren naar een lokale map op ~ / azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="fff2a-159">Copy the previously mentioned jars to a local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-the-dependencies-to-the-spark-worker-nodes"></a><span data-ttu-id="fff2a-160">De afhankelijkheden met de werkrolknooppunten Spark distribueren</span><span class="sxs-lookup"><span data-stu-id="fff2a-160">Distribute the dependencies to the Spark worker nodes</span></span> 

1. <span data-ttu-id="fff2a-161">Omdat de transformatie van grafiekgegevens is afhankelijk van TinkerPop3, moet u de bijbehorende afhankelijkheden om alle Spark worker-knooppunten te distribueren.</span><span class="sxs-lookup"><span data-stu-id="fff2a-161">Because the transformation of graph data depends on TinkerPop3, you must distribute the related dependencies to all Spark worker nodes.</span></span>

2. <span data-ttu-id="fff2a-162">Kopieer de eerder genoemde Gremlin afhankelijkheden, CosmosDB Spark connector jar en CosmosDB Java SDK met de werkrolknooppunten als volgt:</span><span class="sxs-lookup"><span data-stu-id="fff2a-162">Copy the previously mentioned Gremlin dependencies, the CosmosDB Spark connector jar, and CosmosDB Java SDK to the worker nodes by doing the following:</span></span>

    <span data-ttu-id="fff2a-163">a.</span><span class="sxs-lookup"><span data-stu-id="fff2a-163">a.</span></span> <span data-ttu-id="fff2a-164">Kopieer alle potten in `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-164">Copy all the jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="fff2a-165">b.</span><span class="sxs-lookup"><span data-stu-id="fff2a-165">b.</span></span> <span data-ttu-id="fff2a-166">De lijst met alle Spark worker-knooppunten, kunt u vinden op Ambari-Dashboard in de `Spark2 Clients` lijst de `Spark2` sectie.</span><span class="sxs-lookup"><span data-stu-id="fff2a-166">Get the list of all Spark worker nodes, which you can find on Ambari Dashboard, in the `Spark2 Clients` list in the `Spark2` section.</span></span>

    <span data-ttu-id="fff2a-167">c.</span><span class="sxs-lookup"><span data-stu-id="fff2a-167">c.</span></span> <span data-ttu-id="fff2a-168">Kopieer de map aan elk van de knooppunten.</span><span class="sxs-lookup"><span data-stu-id="fff2a-168">Copy that directory to each of the nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-the-environment-variables"></a><span data-ttu-id="fff2a-169">De omgevingsvariabelen instellen</span><span class="sxs-lookup"><span data-stu-id="fff2a-169">Set up the environment variables</span></span>

1. <span data-ttu-id="fff2a-170">Zoek de HDP-versie van het Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="fff2a-170">Find the HDP version of the Spark cluster.</span></span> <span data-ttu-id="fff2a-171">Het is de naam van de map onder `/usr/hdp/` (bijvoorbeeld 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="fff2a-171">It is the directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="fff2a-172">Stel hdp.version voor alle knooppunten.</span><span class="sxs-lookup"><span data-stu-id="fff2a-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="fff2a-173">Ga in de Ambari-Dashboard naar **YARN-sectie** > **Configs** > **Geavanceerd**, en voer de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="fff2a-173">In Ambari Dashboard, go to **YARN section** > **Configs** > **Advanced**, and then do the following:</span></span> 
 
    <span data-ttu-id="fff2a-174">a.</span><span class="sxs-lookup"><span data-stu-id="fff2a-174">a.</span></span> <span data-ttu-id="fff2a-175">In `Custom yarn-site`, een nieuwe eigenschap toevoegen `hdp.version` met de waarde van de versie HDP op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="fff2a-175">In `Custom yarn-site`, add a new property `hdp.version` with the value of the HDP version on the master node.</span></span> 
     
    <span data-ttu-id="fff2a-176">b.</span><span class="sxs-lookup"><span data-stu-id="fff2a-176">b.</span></span> <span data-ttu-id="fff2a-177">Sla de configuraties.</span><span class="sxs-lookup"><span data-stu-id="fff2a-177">Save the configurations.</span></span> <span data-ttu-id="fff2a-178">Er zijn waarschuwingen die u kunt negeren.</span><span class="sxs-lookup"><span data-stu-id="fff2a-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="fff2a-179">c.</span><span class="sxs-lookup"><span data-stu-id="fff2a-179">c.</span></span> <span data-ttu-id="fff2a-180">De YARN en Oozie-services opnieuw starten als de meldingspictogrammen geven.</span><span class="sxs-lookup"><span data-stu-id="fff2a-180">Restart the YARN and Oozie services as the notification icons indicate.</span></span>

3. <span data-ttu-id="fff2a-181">De volgende omgevingsvariabelen worden ingesteld op het hoofdknooppunt (Vervang de waarden waar nodig):</span><span class="sxs-lookup"><span data-stu-id="fff2a-181">Set the following environment variables on the master node (replace the values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-the-graph-configuration"></a><span data-ttu-id="fff2a-182">Voorbereiden van de configuratie van de grafiek</span><span class="sxs-lookup"><span data-stu-id="fff2a-182">Prepare the graph configuration</span></span>

1. <span data-ttu-id="fff2a-183">Een configuratiebestand met de Azure DB die Cosmos verbindingsparameters en Spark-instellingen maken en plaatsen op `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-183">Create a configuration file with the Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

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

    # Classpath for the driver and executors
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

2. <span data-ttu-id="fff2a-184">Update de `spark.driver.extraClassPath` en `spark.executor.extraClassPath` om op te nemen van de map van de potten die u in de vorige stap hebt gedistribueerd, in dit geval `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-184">Update the `spark.driver.extraClassPath` and `spark.executor.extraClassPath` to include the directory of the jars that you distributed in the previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="fff2a-185">Azure Cosmos DB bieden de volgende details:</span><span class="sxs-lookup"><span data-stu-id="fff2a-185">Provide the following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-the-tinkerpop-graph-and-save-it-to-azure-cosmos-db"></a><span data-ttu-id="fff2a-186">Laden van de grafiek TinkerPop en sla deze op Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="fff2a-186">Load the TinkerPop graph, and save it to Azure Cosmos DB</span></span>
<span data-ttu-id="fff2a-187">Als u wilt laten zien hoe u een grafiek behouden in Azure Cosmos DB, in dit voorbeeld voorgedefinieerde gebruikt de TinkerPop TinkerPop moderne grafiek.</span><span class="sxs-lookup"><span data-stu-id="fff2a-187">To demonstrate how to persist a graph into Azure Cosmos DB, this example uses the TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="fff2a-188">De grafiek wordt opgeslagen in Kryo indeling en in de opslagplaats TinkerPop opgegeven.</span><span class="sxs-lookup"><span data-stu-id="fff2a-188">The graph is stored in Kryo format, and it's provided in the TinkerPop repository.</span></span>

1. <span data-ttu-id="fff2a-189">Omdat u Gremlin in de YARN-modus uitvoert, moet u de grafiekgegevens in het Hadoop-bestandssysteem beschikbaar maken.</span><span class="sxs-lookup"><span data-stu-id="fff2a-189">Because you are running Gremlin in YARN mode, you must make the graph data available in the Hadoop file system.</span></span> <span data-ttu-id="fff2a-190">Gebruik de volgende opdrachten om te maken van een map en kopieer het bestand lokaal grafiek naar het.</span><span class="sxs-lookup"><span data-stu-id="fff2a-190">Use the following commands to make a directory and copy the local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="fff2a-191">Tijdelijk bijwerken de `gremlin-spark.properties` om te gebruiken bestand `GryoInputFormat` lezen van de grafiek.</span><span class="sxs-lookup"><span data-stu-id="fff2a-191">Temporarily update the `gremlin-spark.properties` file to use `GryoInputFormat` to read the graph.</span></span> <span data-ttu-id="fff2a-192">Ook duiden op `inputLocation` als de map u maakt, zoals in het volgende:</span><span class="sxs-lookup"><span data-stu-id="fff2a-192">Also indicate `inputLocation` as the directory you create, as in the following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="fff2a-193">Start Gremlin-Console en maak vervolgens de volgende berekening stappen voor het behouden van gegevens naar de geconfigureerde Azure DB die Cosmos-verzameling:</span><span class="sxs-lookup"><span data-stu-id="fff2a-193">Start Gremlin Console, and then create the following computation steps to persist data to the configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="fff2a-194">a.</span><span class="sxs-lookup"><span data-stu-id="fff2a-194">a.</span></span> <span data-ttu-id="fff2a-195">Maken van de grafiek `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-195">Create the graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="fff2a-196">b.</span><span class="sxs-lookup"><span data-stu-id="fff2a-196">b.</span></span> <span data-ttu-id="fff2a-197">SparkGraphComputer gebruiken om te schrijven `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

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

4. <span data-ttu-id="fff2a-198">U kunt controleren dat de gegevens heeft is opgeslagen in Azure Cosmos DB uit Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="fff2a-198">From Data Explorer, you can verify that the data has been persisted to Azure Cosmos DB.</span></span>

## <a name="load-the-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="fff2a-199">De grafiek uit Azure Cosmos DB laden en Gremlin query's uitvoeren</span><span class="sxs-lookup"><span data-stu-id="fff2a-199">Load the graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="fff2a-200">Als u wilt laden van de grafiek bewerken `gremlin-spark.properties` instellen `graphReader` naar `DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="fff2a-200">To load the graph, edit `gremlin-spark.properties` to set `graphReader` to `DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="fff2a-201">Laden van de grafiek, bladeren door de gegevens en Gremlin query's uitvoeren met dit als volgt:</span><span class="sxs-lookup"><span data-stu-id="fff2a-201">Load the graph, traverse the data, and run Gremlin queries with it by doing the following:</span></span>

    <span data-ttu-id="fff2a-202">a.</span><span class="sxs-lookup"><span data-stu-id="fff2a-202">a.</span></span> <span data-ttu-id="fff2a-203">Start de Console Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-203">Start the Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="fff2a-204">b.</span><span class="sxs-lookup"><span data-stu-id="fff2a-204">b.</span></span> <span data-ttu-id="fff2a-205">De grafiek te maken met de configuratie `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-205">Create the graph with the configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="fff2a-206">c.</span><span class="sxs-lookup"><span data-stu-id="fff2a-206">c.</span></span> <span data-ttu-id="fff2a-207">Een grafiek traversal maken met SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="fff2a-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="fff2a-208">d.</span><span class="sxs-lookup"><span data-stu-id="fff2a-208">d.</span></span> <span data-ttu-id="fff2a-209">Voer de volgende query's voor Gremlin-grafiek:</span><span class="sxs-lookup"><span data-stu-id="fff2a-209">Run the following Gremlin graph queries:</span></span>

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
> <span data-ttu-id="fff2a-210">Ga voor meer gedetailleerde logboekregistratie, stelt u het logboek niveau in `conf/log4j-console.properties` naar een uitgebreidere niveau.</span><span class="sxs-lookup"><span data-stu-id="fff2a-210">To see more detailed logging, set the log level in `conf/log4j-console.properties` to a more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="fff2a-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fff2a-211">Next steps</span></span>

<span data-ttu-id="fff2a-212">U kunt het werken met grafieken door een combinatie van Azure DB die Cosmos en Spark hebt geleerd in dit artikel snel starten.</span><span class="sxs-lookup"><span data-stu-id="fff2a-212">In this quick-start article, you've learned how to work with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
