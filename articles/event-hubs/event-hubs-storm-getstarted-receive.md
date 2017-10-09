---
title: gebeurtenissen van Azure Event Hubs met behulp van Apache Storm aaaReceive | Microsoft Docs
description: Aan de slag van Event Hubs met behulp van Apache Storm ontvangen
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: java
ms.devlang: multiple
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a0ab860ee8d504a28aac380c504c928f0d6dbc1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a>Gebeurtenissen van Event Hubs met behulp van Apache Storm ontvangen

[Apache Storm](https://storm.incubator.apache.org) is een gedistribueerde realtime berekeningssysteem die betrouwbare verwerking van unbounded gegevensstromen vereenvoudigt. Deze sectie wordt beschreven hoe een Azure Event Hubs Storm toouse spout tooreceive gebeurtenissen van Event Hubs. Apache Storm kunt u gebeurtenissen splitsen in meerdere processen die worden gehost in verschillende knooppunten. Hallo Event Hubs-integratie met Storm vereenvoudigt de gebeurtenis verbruik door transparant plaatsen van controlepunten de voortgang van Storm Zookeeper-installatie, het beheren van permanente controlepunten en parallelle ontvangst van Event Hubs.

Voor meer informatie over Event Hubs ontvangen patronen, Zie Hallo [overzicht van Event Hubs][Event Hubs overview].

## <a name="create-project-and-add-code"></a>Project maken en voeg code toe

In deze zelfstudie wordt een [HDInsight Storm] [ HDInsight Storm] installatie, die wordt geleverd met Event Hubs spout Hallo al beschikbaar.

1. Ga als volgt Hallo [HDInsight Storm - aan de slag](../hdinsight/hdinsight-storm-overview.md) toocreate procedure een nieuwe HDInsight-cluster en tooit via Extern bureaublad verbinding.
2. Kopiëren Hallo `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` bestand tooyour lokale ontwikkelingsomgeving. Dit document bevat Hallo gebeurtenissen-storm-spout.
3. Gebruik Hallo volgende opdracht tooinstall Hallo pakket aan Hallo lokale Maven-archief. Hiermee kunt u tooadd als een verwijzing in Hallo Storm-project in een later stadium.

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. Maak in Eclipse een nieuw Maven-project (Klik op **bestand**, klikt u vervolgens **nieuw**, klikt u vervolgens **Project**).
   
    ![][12]
5. Selecteer **standaard werkruimte gebruiken**, klikt u vervolgens op **volgende**
6. Selecteer Hallo **maven-archetype-Quick Start** archetype, klikt u vervolgens op **volgende**
7. Voeg een **GroupId** en **artefact-id**, klikt u vervolgens op **voltooien**
8. In **pom.xml**, toevoegen van de volgende afhankelijkheden in Hallo Hallo `<dependency>` knooppunt.

    ```xml  
    <dependency>
        <groupId>org.apache.storm</groupId>
        <artifactId>storm-core</artifactId>
        <version>0.9.2-incubating</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.microsoft.eventhubs</groupId>
        <artifactId>eventhubs-storm-spout</artifactId>
        <version>0.9</version>
    </dependency>
    <dependency>
        <groupId>com.netflix.curator</groupId>
        <artifactId>curator-framework</artifactId>
        <version>1.3.3</version>
        <exclusions>
            <exclusion>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
            </exclusion>
            <exclusion>
                <groupId>org.slf4j</groupId>
                <artifactId>slf4j-log4j12</artifactId>
            </exclusion>
        </exclusions>
        <scope>provided</scope>
    </dependency>
    ```

9. In Hallo **src** map maken van een bestand met de naam **Config.properties** en kopiëren Hallo inhoud te volgen, vervangen door Hallo `receive rule key` en `event hub name` waarden:

    ```java
    eventhubspout.username = ReceiveRule
    eventhubspout.password = {receive rule key}
    eventhubspout.namespace = ioteventhub-ns
    eventhubspout.entitypath = {event hub name}
    eventhubspout.partitions.count = 16
       
    # if not provided, will use storm's zookeeper settings
    # zookeeper.connectionstring=localhost:2181
       
    eventhubspout.checkpoint.interval = 10
    eventhub.receiver.credits = 10
    ```
    waarde voor Hallo **eventhub.receiver.credits** bepaalt hoeveel gebeurtenissen voordat toohello Storm pijplijn in batch worden opgenomen. Dit voorbeeld wordt voor Hallo mogelijk te houden van eenvoud, deze too10 waarde. In productie, meestal ingesteld toohigher waarden; bijvoorbeeld 1024.
10. Maak een nieuwe klasse aangeroepen **LoggerBolt** Hello code te volgen:
    
    ```java
    import java.util.Map;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import backtype.storm.task.OutputCollector;
    import backtype.storm.task.TopologyContext;
    import backtype.storm.topology.OutputFieldsDeclarer;
    import backtype.storm.topology.base.BaseRichBolt;
    import backtype.storm.tuple.Tuple;
    
    public class LoggerBolt extends BaseRichBolt {
        private OutputCollector collector;
        private static final Logger logger = LoggerFactory
                  .getLogger(LoggerBolt.class);
    
        @Override
        public void execute(Tuple tuple) {
            String value = tuple.getString(0);
            logger.info("Tuple value: " + value);
   
            collector.ack(tuple);
        }
   
        @Override
        public void prepare(Map map, TopologyContext context, OutputCollector collector) {
            this.collector = collector;
            this.count = 0;
        }
        
        @Override
        public void declareOutputFields(OutputFieldsDeclarer declarer) {
            // no output fields
        }
    
    }
    ```
    
    Deze bolt Storm Hiermee Hallo inhoud van Hallo ontvangen gebeurtenissen. Dit kan eenvoudig worden uitgebreid toostore tuples in een storage-service. Hallo [HDInsight sensor analysis zelfstudie] maakt gebruik van deze dezelfde benadering toostore gegevens in HBase.
11. Maak een klasse aangeroepen **LogTopology** Hello code te volgen:
    
    ```java
    import java.io.FileReader;
    import java.util.Properties;
    import backtype.storm.Config;
    import backtype.storm.LocalCluster;
    import backtype.storm.StormSubmitter;
    import backtype.storm.generated.StormTopology;
    import backtype.storm.topology.TopologyBuilder;
    import com.microsoft.eventhubs.samples.EventCount;
    import com.microsoft.eventhubs.spout.EventHubSpout;
    import com.microsoft.eventhubs.spout.EventHubSpoutConfig;
        
    public class LogTopology {
        protected EventHubSpoutConfig spoutConfig;
        protected int numWorkers;
        
        protected void readEHConfig(String[] args) throws Exception {
            Properties properties = new Properties();
            if (args.length > 1) {
                properties.load(new FileReader(args[1]));
            } else {
                properties.load(EventCount.class.getClassLoader()
                        .getResourceAsStream("Config.properties"));
            }
        
            String username = properties.getProperty("eventhubspout.username");
            String password = properties.getProperty("eventhubspout.password");
            String namespaceName = properties
                    .getProperty("eventhubspout.namespace");
            String entityPath = properties.getProperty("eventhubspout.entitypath");
            String zkEndpointAddress = properties
                    .getProperty("zookeeper.connectionstring"); // opt
            int partitionCount = Integer.parseInt(properties
                    .getProperty("eventhubspout.partitions.count"));
            int checkpointIntervalInSeconds = Integer.parseInt(properties
                    .getProperty("eventhubspout.checkpoint.interval"));
            int receiverCredits = Integer.parseInt(properties
                    .getProperty("eventhub.receiver.credits")); // prefetch count
                                                                // (opt)
            System.out.println("Eventhub spout config: ");
            System.out.println("  partition count: " + partitionCount);
            System.out.println("  checkpoint interval: "
                    + checkpointIntervalInSeconds);
            System.out.println("  receiver credits: " + receiverCredits);
     
            spoutConfig = new EventHubSpoutConfig(username, password,
                    namespaceName, entityPath, partitionCount, zkEndpointAddress,
                    checkpointIntervalInSeconds, receiverCredits);
        
            // set hello number of workers toobe hello same as partition number.
            // hello idea is toohave a spout and a logger bolt co-exist in one
            // worker tooavoid shuffling messages across workers in storm cluster.
            numWorkers = spoutConfig.getPartitionCount();
        
            if (args.length > 0) {
                // set topology name so that sample Trident topology can use it as
                // stream name.
                spoutConfig.setTopologyName(args[0]);
            }
        }
        
        protected StormTopology buildTopology() {
            TopologyBuilder topologyBuilder = new TopologyBuilder();
       
            EventHubSpout eventHubSpout = new EventHubSpout(spoutConfig);
            topologyBuilder.setSpout("EventHubsSpout", eventHubSpout,
                    spoutConfig.getPartitionCount()).setNumTasks(
                    spoutConfig.getPartitionCount());
            topologyBuilder
                    .setBolt("LoggerBolt", new LoggerBolt(),
                            spoutConfig.getPartitionCount())
                    .localOrShuffleGrouping("EventHubsSpout")
                    .setNumTasks(spoutConfig.getPartitionCount());
            return topologyBuilder.createTopology();
        }
        
        protected void runScenario(String[] args) throws Exception {
            boolean runLocal = true;
            readEHConfig(args);
            StormTopology topology = buildTopology();
            Config config = new Config();
            config.setDebug(false);
        
            if (runLocal) {
                config.setMaxTaskParallelism(2);
                LocalCluster localCluster = new LocalCluster();
                localCluster.submitTopology("test", config, topology);
                Thread.sleep(5000000);
                localCluster.shutdown();
            } else {
                config.setNumWorkers(numWorkers);
                StormSubmitter.submitTopology(args[0], config, topology);
            }
        }
        
        public static void main(String[] args) throws Exception {
            LogTopology topology = new LogTopology();
            topology.runScenario(args);
        }
    }
    ```

    Deze klasse wordt gemaakt van een nieuwe Event Hubs-spout met Hallo eigenschappen in Hallo configuration file tooinstantiate deze. Het is belangrijk toonote die in dit voorbeeld zo veel mogelijk maakt spouts taken als Hallo aantal partities in Hallo event hub, in volgorde toouse Hallo maximale parallelle uitvoering toegestaan door de event hub.

## <a name="next-steps"></a>Volgende stappen
U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Event Hubs-overzicht][Event Hubs overview]
* [Een Event Hub maken](event-hubs-create.md)
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[HDInsight sensor analysis zelfstudie]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
