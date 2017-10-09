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
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a>Azure Cosmos DB: Grafiek analyses uitvoeren met behulp van Spark en Apache TinkerPop Gremlin

[Azure Cosmos DB](introduction.md) is Hallo globaal gedistribueerd en modellen database-service van Microsoft. U kunt maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van de algemene distributie en het horizontale schaal mogelijkheden Hallo Hallo kern van Azure DB die Cosmos profiteren. Azure Cosmos DB ondersteunt online transactieverwerking (OLTP) grafiek werkbelastingen die gebruikmaken van [Apache TinkerPop Gremlin](graph-introduction.md).

[Spark](http://spark.apache.org/) is een Apache Software Foundation-project dat gericht op het verwerken van gegevens voor algemene doeleinden online analytical processing (OLAP). Spark biedt een hybride in-memory/op basis van schijven gedistribueerde computermodel dat vergelijkbare toohello Hadoop MapReduce-model. U kunt een Apache Spark in Hallo cloud implementeren met behulp van [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).

U kunt door een combinatie van Azure DB die Cosmos en Spark OLTP- en OLAP-werkbelastingen uitvoeren wanneer u Gremlin gebruikt. In dit artikel snel starten laat zien hoe toorun Gremlin query's op basis van Azure DB die Cosmos in een Azure HDInsight Spark-cluster.

## <a name="prerequisites"></a>Vereisten

Voordat u dit voorbeeld uitvoeren kunt, hebt u Hallo volgende vereisten:
* Azure HDInsight Spark-cluster 2.0
* JDK 1.8 + (als u geen JDK, voert u `apt-get install default-jdk`.)
* Maven (als u geen Maven, voert u `apt-get install maven`.)
* Een Azure-abonnement ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])

Voor informatie over het tooset van een Azure HDInsight Spark-cluster, Zie [inrichten van HDInsight-clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

## <a name="create-an-azure-cosmos-db-database-account"></a>Een Azure DB die Cosmos-databaseaccount maken

Maak eerst een databaseaccount Hello Graph API door Hallo volgende te doen:

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Een verzameling toevoegen

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a>Apache TinkerPop ophalen

Apache TinkerPop ophalen door Hallo volgende te doen:

1. Externe toohello hoofdknooppunt van het HDInsight-cluster Hallo `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.

2. Hallo TinkerPop3 broncode klonen, lokaal bouwen en installeer deze tooMaven cache.

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. Hallo Spark-Gremlin invoegtoepassing installeren 

    a. Hallo-installatie van de invoegtoepassing hello wordt verwerkt door gedeeltelijk. Hallo-opslagplaatsen informatie voor gedeeltelijk vullen zodat het kan worden gedownload Hallo invoegtoepassing en de bijbehorende afhankelijkheden. 

      Hallo druivenmost-configuratiebestand maken als het is niet aanwezig zijn bij `~/.groovy/grapeConfig.xml`. Gebruik Hallo volgende instellingen:

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

    b. Start de console Gremlin `bin/gremlin.sh`.
        
    c. Hallo Spark-Gremlin invoegtoepassing installeren met versie 3.3.0-SNAPSHOT die u in de vorige stappen Hallo gebouwd:

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

4. Controleer of de toosee `Hadoop-Gremlin` is geactiveerd met een `:plugin list`. Schakel deze invoegtoepassing zijn, omdat deze Hallo Spark Gremlin invoegtoepassing verstoren kan `:plugin unuse tinkerpop.hadoop`.

## <a name="prepare-tinkerpop3-dependencies"></a>TinkerPop3 afhankelijkheden voorbereiden

Wanneer u TinkerPop3 in de vorige stap hello gemaakt, Hallo proces alle afhankelijkheden van de jar ook voor Spark en Hadoop in de doelmap Hallo opgehaald. Gebruik Hallo potten die vooraf zijn geïnstalleerd met HDI en ophalen van extra afhankelijkheden alleen indien nodig.

1. Ga toohello Gremlin Console doelmap op `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`. 

2. Verplaats alle potten onder `ext/` te`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.

3. Verwijder alle bibliotheken onder jar `lib/` dat niet in Hallo lijst volgt:

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

## <a name="get-hello-azure-cosmos-db-spark-connector"></a>Hello Azure Cosmos DB Spark connector ophalen

1. Hello Azure Cosmos DB Spark connector ophalen `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` en Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` van [Azure DB Spark Cosmos-Connector op GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).

2. U kunt ook kunt u deze lokaal. Omdat de meest recente versie Hallo van Spark Gremlin is gebouwd met Spark 1.6.1 en niet compatibel met Spark 2.0.2 is, momenteel in hello Azure Cosmos DB Spark-connector gebruikt wordt, kunt u Hallo nieuwste TinkerPop3 code bouwen en Hallo potten handmatig installeren. Hallo te volgen:

    a. Kloon hello Azure Cosmos DB Spark-connector.

    b. Bouw TinkerPop3 (in de vorige stappen hebt). Installeer alle TinkerPop 3.3.0-SNAPSHOT potten lokaal.

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    c. Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` te`3.3.0-SNAPSHOT`.
    
    d. Bij het maken van Maven. Hallo benodigde potten worden geplaatst `target` en `target/alternateLocation`.

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. Genoemde potten tooa lokale map op de kopie Hallo ~ / azure-documentdb-spark:

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a>Hallo afhankelijkheden toohello Spark worker-knooppunten distribueren 

1. Omdat Hallo transformatie van grafiekgegevens is afhankelijk van TinkerPop3, moet u distribueren Hallo gerelateerde afhankelijkheden tooall Spark worker-knooppunten.

2. Kopiëren Hallo genoemde Gremlin afhankelijkheden, Hallo CosmosDB Spark connector jar en CosmosDB Java SDK toohello worker-knooppunten door Hallo volgende te doen:

    a. Kopieer alle Hallo potten in `~/azure-documentdb-spark`.

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    b. Hallo-lijst met alle Spark worker-knooppunten, kunt u vinden op Ambari-Dashboard in Hallo `Spark2 Clients` lijst in Hallo `Spark2` sectie.

    c. Kopieer deze directory tooeach Hallo knooppunten.

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a>Hallo omgevingsvariabelen instellen

1. Hallo HDP versie vinden van Hallo Spark-cluster. De mapnaam Hallo onder is `/usr/hdp/` (bijvoorbeeld 2.5.4.2-7).

2. Stel hdp.version voor alle knooppunten. In de Ambari-Dashboard, gaat u te**YARN sectie** > **Configs** > **Geavanceerd**, en vervolgens Hallo te volgen: 
 
    a. In `Custom yarn-site`, een nieuwe eigenschap toevoegen `hdp.version` met Hallo waarde Hallo HDP versie op Hallo hoofdknooppunt. 
     
    b. Hallo configuraties opslaan. Er zijn waarschuwingen die u kunt negeren. 
     
    c. Hallo YARN en Oozie-services opnieuw starten als Hallo meldingspictogrammen geven.

3. Set Hallo omgevingsvariabelen op Hallo hoofdknooppunt (vervangen Hallo waarden naar gelang van toepassing) te volgen:

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a>Configuratie van de grafiek Hallo voorbereiden

1. Een configuratiebestand maken door hello Azure Cosmos DB verbindingsparameters en instellingen Spark en plaatsen op `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.

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

2. Update Hallo `spark.driver.extraClassPath` en `spark.executor.extraClassPath` tooinclude Hallo-map van Hallo potten die u in de vorige stap hello, verdeeld in dit geval `/home/sshuser/azure-documentdb-spark/*`.

3. Hallo volgende details voor Azure Cosmos DB bieden:

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a>Hallo TinkerPop grafiek laden en sla het tooAzure Cosmos-DB
toodemonstrate hoe toopersist een grafiek naar Azure Cosmos DB, in dit voorbeeld gebruikt Hallo TinkerPop vooraf gedefinieerde TinkerPop moderne grafiek. Hallo grafiek wordt opgeslagen in de indeling Kryo en dit wordt geleverd in Hallo TinkerPop opslagplaats.

1. Omdat u Gremlin in de YARN-modus uitvoert, moet u Hallo grafiekgegevens in Hallo Hadoop-bestandssysteem beschikbaar maken. Gebruik Hallo volgende opdrachten toomake een map en Hallo lokale graph-bestand kopiëren in de App. 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. Tijdelijk bijwerken Hallo `gremlin-spark.properties` bestand toouse `GryoInputFormat` tooread Hallo grafiek. Ook duiden op `inputLocation` als Hallo map u maakt, zoals Hallo volgende in:

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. Start Gremlin-Console en maak vervolgens Hallo berekening stappen toopersist toohello geconfigureerd Azure Cosmos DB gegevensverzameling te volgen:  

    a. Hallo-grafiek maken `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.

    b. SparkGraphComputer gebruiken om te schrijven `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.

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

4. U kunt controleren die gegevens zijn Hallo persistent tooAzure Cosmos DB van Data Explorer.

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a>Hallo grafiek uit Azure Cosmos DB laden en Gremlin query's uitvoeren

1. tooload hello grafiek bewerken `gremlin-spark.properties` tooset `graphReader` te`DocumentDBInputRDD`:

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. Hallo grafiek laden, bladeren door het Hallo-gegevens en Gremlin query's uitvoeren met het door Hallo volgende te doen:

    a. Hallo Gremlin Console starten `bin/gremlin.sh`.

    b. Hallo-grafiek maken met Hallo configuratie `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.

    c. Een grafiek traversal maken met SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.

    d. Voer Hallo Gremlin grafiek query's te volgen:

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
> toosee meer gedetailleerde logboekregistratie Hallo logboekniveau ingesteld in `conf/log4j-console.properties` tooa uitgebreidere niveau.
>

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe toowork met grafieken door Azure Cosmos DB en Spark te combineren in dit artikel snel starten.

> [!div class="nextstepaction"]
