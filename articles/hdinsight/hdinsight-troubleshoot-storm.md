---
title: aaaTroubleshoot Storm met behulp van Azure HDInsight | Microsoft Docs
description: Vind antwoorden op vragen over het gebruik van Apache Storm met Azure HDInsight toocommon.
keywords: HDInsight, Storm, veelgestelde vragen over Azure, handleiding worden veelvoorkomende problemen oplossen
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a>Storm oplossen met behulp van Azure HDInsight

Meer informatie over de meestvoorkomende problemen Hallo en hun oplossingen voor het werken met Apache Storm-nettoladingen in Apache Ambari.

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a>Hoe krijg ik toegang tot Hallo Storm-gebruikersinterface op een cluster
U hebt twee opties voor toegang tot Hallo Storm-gebruikersinterface vanuit een browser:

### <a name="ambari-ui"></a>Ambari-gebruikersinterface
1. Ga toohello Ambari-dashboard.
2. Selecteer in de lijst met services Hallo **Storm**.
3. In Hallo **snelkoppelingen** selecteert u **Storm-gebruikersinterface**.

### <a name="direct-link"></a>Directe koppeling
U kunt openen Hallo Storm-gebruikersinterface op Hallo URL te volgen:

https://\<cluster DNS-naam\>/stormui

Voorbeeld:

 https://stormcluster.azurehdinsight.NET/stormui

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a>Hoe moet ik Storm event hub spout controlepunt informatie overbrengen van een topologie tooanother

Wanneer u topologieën die lezen uit Azure Event Hubs met Hallo HDInsight Storm event hub spout JAR-bestand ontwikkelt, moet u een topologie met dezelfde naam op een nieuw cluster Hallo implementeren. U moet echter Hallo controlepuntgegevens die doorgevoerd tooApache ZooKeeper op het oude cluster Hallo was behouden.

### <a name="where-checkpoint-data-is-stored"></a>Waar controlepuntgegevens worden opgeslagen
Controlepuntgegevens voor offsets worden opgeslagen door Hallo event hub spout in ZooKeeper in twee hoofdmappen:
- Niet-transactionele spout controlepunten worden opgeslagen in /eventhubspout.
- Transactionele spout controlepuntgegevens worden opgeslagen in / transactionele.

### <a name="how-toorestore"></a>Hoe toorestore
Zie tooget Hallo scripts en bibliotheken tooexport gegevens buiten ZooKeeper te gebruiken en vervolgens importeren Hallo gegevens back tooZooKeeper met een nieuwe naam [HDInsight Storm voorbeelden](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).

Hallo lib map bevat de JAR-bestanden die Hallo-implementatie voor Hallo exporteren/importeren bewerking bevatten. Hallo bash map heeft een voorbeeldscript dat laat zien hoe gegevens van tooexport ZooKeeper server op het oude cluster Hallo Hallo en importeer vervolgens back toohello ZooKeeper server op Hallo nieuwe cluster.

Voer Hallo [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script uit Hallo ZooKeeper-knooppunten tooexport en importeer gegevens. Hallo script toohello juist Hortonworks Data Platform HDP ()-versie bijwerken. (We werken over het maken van deze scripts algemene in HDInsight. Algemene scripts kunnen uitvoeren vanaf elk knooppunt op Hallo cluster zonder wijzigingen door de gebruiker Hallo.)

de opdracht exporteren Hallo schrijft Hallo tooan Apache Hadoop Distributed File System (HDFS) metagegevenspad (in een store Azure Blob Storage of Azure Data Lake Store) op een locatie die u instelt.

### <a name="examples"></a>Voorbeelden

#### <a name="export-offset-metadata"></a>Offset metagegevens exporteren
1. SSH toogo toohello ZooKeeper-cluster op Hallo-cluster vanaf het controlepunt van welke Hallo offset toobe geëxporteerd moet gebruiken.
2. Voer Hallo volgende opdracht (na het bijwerken van Hallo HDP versietekenreeks) tooexport ZooKeeper offset gegevens toohello /stormmetadta/zkdata HDFS pad:

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a>Offset metagegevens importeren
1. SSH toogo toohello ZooKeeper-cluster op Hallo-cluster vanaf het controlepunt van welke Hallo offset toobe geëxporteerd moet gebruiken.
2. Voer hello volgende opdracht (na het bijwerken van Hallo HDP versietekenreeks) tooimport ZooKeeper gegevens van Hallo HDFS pad/stormmetadata/zkdata toohello ZooKeeper server op Hallo doelcluster offset:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a>Offset metagegevens verwijderen zodat topologieën kunnen beginnen met het verwerken van gegevens vanaf het begin van de Hallo of van een tijdstempel die gebruiker Hallo kiest
1. SSH toogo toohello ZooKeeper-cluster op Hallo-cluster vanaf het controlepunt van welke Hallo offset toobe geëxporteerd moet gebruiken.
2. Voer hello volgende opdracht (na het bijwerken van Hallo HDP versietekenreeks) toodelete alle ZooKeeper gegevens in de huidige cluster Hallo offset:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a>Hoe ik Storm binaire bestanden vinden op een cluster
Storm-binaire bestanden voor de huidige HDP stack Hallo zijn in /usr/hdp/current/storm-client. Hallo-locatie wordt Hallo dezelfde hoofdknooppunten en voor worker-knooppunten.
 
Er is mogelijk meerdere binaire bestanden voor specifieke HDP versies in /usr/hdp (bijvoorbeeld /usr/hdp/2.5.0.1233/storm). Hallo /usr/hdp/current/storm-client map is symlinked toohello meest recente versie die wordt uitgevoerd op Hallo-cluster.

Zie voor meer informatie [Connect tooan HDInsight-cluster via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) en [Storm](http://storm.apache.org/).
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a>Hoe bepaal ik implementatietopologie Hallo van een Storm-cluster
Bepaal eerst alle onderdelen die zijn geïnstalleerd met HDInsight Storm. Een Storm-cluster bestaat uit vier categorieën van knooppunt:

* Gateway-knooppunten
* HEAD-knooppunten
* ZooKeeper-knooppunten
* Worker-knooppunten
 
### <a name="gateway-nodes"></a>Gateway-knooppunten
Een gateway-knooppunt is een gateway en de reverse proxyservice waarmee openbare toegang tooan active Ambari management-service. Ambari opvulteken keuze ook verwerkt.
 
### <a name="head-nodes"></a>HEAD-knooppunten
Storm-hoofdknooppunten Voer Hallo volgende services:
* Nimbus
* Ambari-server
* Metrische gegevens Ambari-server
* Ambari metrische gegevens verzamelen
 
### <a name="zookeeper-nodes"></a>ZooKeeper-knooppunten
HDInsight wordt geleverd met een quorum van de ZooKeeper drie knooppunten. Hallo quorum grootte is vast en kan niet worden geconfigureerd.
 
Storm-services in Hallo cluster zijn geconfigureerd tooautomatically gebruik Hallo ZooKeeper quorum.
 
### <a name="worker-nodes"></a>Worker-knooppunten
Storm worker-knooppunten uitvoeren Hallo volgende services:
* Supervisor
* Werknemer Java virtuele machines (JVMs) voor het uitvoeren van topologieën
* Ambari-agent
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a>Hoe ik Storm event hub spout binaire bestanden voor de ontwikkeling van vinden
 
Zie voor meer informatie over het gebruik van Storm event hub spout JAR-bestanden met uw topologie Hallo resources te volgen.
 
### <a name="java-based-topology"></a>Op basis van Java-topologie
[Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a>C#-topologie (Mono op HDInsight 3.4 + Linux Storm-clusters) gebaseerd
[Process events from Azure Event Hubs with Storm on HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology) (Gebeurtenissen uit Azure Event Hubs verwerken met Storm op HDInsight (C#))
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a>Meest recente Storm event hub spout binaire bestanden voor HDInsight 3.5 + Linux Storm-clusters
toolearn hoe toouse Hallo nieuwste Storm event hub spout die met HDInsight 3.5 werkt + Linux Storm-clusters, raadpleegt u Hallo mvn-opslagplaats [Leesmij-bestand](https://github.com/hdinsight/mvn-repo/blob/master/README.md).
 
### <a name="source-code-examples"></a>Bron-codevoorbeelden
Zie [voorbeelden](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) van hoe tooread en schrijven van Azure Event Hub met behulp van een Apache Storm-topologie (geschreven in Java) op een Azure HDInsight-cluster.
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a>Hoe ik Storm Log4J configuratiebestanden op clusters vinden
 
configuratiebestanden tooidentify Apache-Log4J voor Storm-services.
 
### <a name="on-head-nodes"></a>Over hoofdknooppunten
Hallo Nimbus Log4J configuratie wordt gelezen uit /usr/hdp/\<HDP versie\>/storm/log4j2/cluster.xml.
 
### <a name="on-worker-nodes"></a>Op de worker-knooppunten
Hallo supervisor Log4J configuratie wordt gelezen uit /usr/hdp/\<HDP versie\>/storm/log4j2/cluster.xml.
 
Hallo worker Log4J-configuratiebestand is gelezen uit /usr/hdp/\<HDP versie\>/storm/log4j2/worker.xml.
 
Voorbeelden: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml

