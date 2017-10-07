---
title: aaaPorts gebruikt met Hadoop op HDInsight - Azure-services | Microsoft Docs
description: Een lijst met poorten die worden gebruikt door services Hadoop op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd14aed9-ec25-4bb3-a20c-e29562735a7d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 0abc5c1c678aa79816e3e82a74538d2fb6db40ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ports-used-by-hadoop-services-on-hdinsight"></a>Poorten die worden gebruikt door services Hadoop in HDInsight

Dit document bevat een lijst met Hallo poorten gebruikt door services Hadoop op Linux gebaseerde HDInsight-clusters. Het bevat ook informatie over poorten gebruikt tooconnect toohello-cluster via SSH.

## <a name="public-ports-vs-non-public-ports"></a>Openbare poorten versus niet-openbaar poorten

Linux gebaseerde HDInsight-clusters alleen zichtbaar drie poorten openbaar op Hallo internet; 22, 23 en 443. Deze poorten zijn gebruikte toosecurely RAS Hallo-cluster via SSH en services die worden weergegeven via Hallo beveiligde HTTPS-protocol.

Intern HDInsight door verschillende Azure Virtual Machines (Hallo knooppunten binnen Hallo cluster) is geïmplementeerd op een virtuele Azure-netwerk worden uitgevoerd. Vanaf binnen het virtuele netwerk Hallo, u kunt toegang tot poorten niet weergegeven via Hallo internet. Bijvoorbeeld, als u tooone van hoofdknooppunten Hallo via SSH verbinding, vanaf het hoofdknooppunt Hallo van u kunt vervolgens rechtstreeks toegang tot services die worden uitgevoerd op de clusterknooppunten Hallo.

> [!IMPORTANT]
> Als u geen een Azure-netwerk als een configuratieoptie voor HDInsight opgeeft, wordt een automatisch gemaakt. U kunt niet echter andere machines (zoals andere Azure Virtual Machines of uw ontwikkelcomputer client) toothis virtueel netwerk koppelen.


toojoin aanvullende machines toohello virtueel netwerk, en u moet eerst Hallo virtueel netwerk maken en vervolgens bij het maken van uw HDInsight-cluster opgeven. Zie voor meer informatie [mogelijkheden uitbreiden HDInsight met behulp van een Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md)

## <a name="public-ports"></a>Openbare poorten

Alle Hallo knooppunten in een HDInsight-cluster bevinden zich in een Azure-netwerk en kunnen niet rechtstreeks toegankelijk zijn vanuit Hallo internet. Een openbare gateway biedt internet toegang toohello na poorten, die door alle HDInsight-clustertypen gedeeld worden.

| Service | Poort | Protocol | Beschrijving |
| --- | --- | --- | --- | --- |
| sshd |22 |SSH |Clients toosshd op Hallo primaire headnode verbindt. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie. |
| sshd |22 |SSH |Verbonden clients toosshd op Hallo edge-knooppunt. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie. |
| sshd |23 |SSH |Clients toosshd op Hallo secundaire headnode verbindt. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie. |
| Ambari |443 |HTTPS |Ambari-webgebruikersinterface. Zie [HDInsight beheren met behulp van Hallo Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md) |
| Ambari |443 |HTTPS |Ambari REST-API. Zie [HDInsight beheren met behulp van Hallo Ambari REST-API](hdinsight-hadoop-manage-ambari-rest-api.md) |
| WebHCat |443 |HTTPS |HCatalog REST-API. Zie [Hive gebruiken met Curl](hdinsight-hadoop-use-pig-curl.md), [Pig gebruiken met Curl](hdinsight-hadoop-use-pig-curl.md), [MapReduce gebruiken met Curl](hdinsight-hadoop-use-mapreduce-curl.md) |
| HiveServer2 |443 |ODBC |Maakt verbinding met ODBC tooHive. Zie [tooHDInsight Excel verbinding met ODBC-stuurprogramma Hallo](hdinsight-connect-excel-hive-odbc-driver.md). |
| HiveServer2 |443 |JDBC |Maakt verbinding met JDBC tooHive. Zie [verbinding tooHive op HDInsight met behulp van Hallo Hive JDBC-stuurprogramma](hdinsight-connect-hive-jdbc-driver.md) |

de volgende Hallo zijn beschikbaar voor specifieke clustertypen:

| Service | Poort | Protocol | Clustertype | Beschrijving |
| --- | --- | --- | --- | --- |
| Stargate |443 |HTTPS |HBase |HBase REST-API. Zie [aan de slag met HBase](hdinsight-hbase-tutorial-get-started-linux.md) |
| Livy |443 |HTTPS |Spark |Spark REST-API. Zie [Spark verzenden van taken op afstand met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md) |
| Storm |443 |HTTPS |Storm |Storm-webgebruikersinterface. Zie [implementeren en beheren van Storm-topologieën op HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md) |

### <a name="authentication"></a>Authentication

Alle services openbaar zichtbaar op Hallo die Internet moet worden geverifieerd:

| Poort | Referenties |
| --- | --- |
| 22 of 23 |Hallo SSH-gebruikersreferenties opgegeven tijdens het maken van het cluster |
| 443 |Hallo-aanmeldingsnaam (standaard: admin) en het wachtwoord die zijn ingesteld tijdens het maken van het cluster |

## <a name="non-public-ports"></a>Niet-openbaar poorten

> [!NOTE]
> Sommige services zijn alleen beschikbaar op specifieke clustertypen. Bijvoorbeeld: HBase is alleen beschikbaar op de HBase-clustertypen.

> [!IMPORTANT]
> Sommige services wordt alleen uitgevoerd op één headnode tegelijk. Als u tooconnect toohello-service op de primaire headnode hello probeert en een 404-fout ontvangt, probeert u opnieuw met behulp van de secundaire headnode Hallo.

### <a name="ambari"></a>Ambari

| Service | Knooppunten | Poort | URL-pad | Protocol | 
| --- | --- | --- | --- | --- |
| Ambari-webgebruikersinterface | HEAD-knooppunten | 8080 | / | HTTP |
| Ambari REST-API | HEAD-knooppunten | 8080 | / api/v1 | HTTP |

Voorbeelden:

* Ambari REST-API:`curl -u admin "http://10.0.0.11:8080/api/v1/clusters"`

### <a name="hdfs-ports"></a>HDFS-poorten

| Service | Knooppunten | Poort | Protocol | Beschrijving |
| --- | --- | --- | --- | --- |
| NameNode webgebruikersinterface |HEAD-knooppunten |30070 |HTTPS |Web UI tooview status |
| Service voor NameNode metagegevens |HEAD-knooppunten |8020 |IPC |Metagegevens van het systeem |
| DataNode |Alle worker-knooppunten |30075 |HTTPS |Web UI tooview status, logboekbestanden, enzovoort. |
| DataNode |Alle worker-knooppunten |30010 |&nbsp; |Gegevensoverdracht |
| DataNode |Alle worker-knooppunten |30020 |IPC |Bewerkingen voor metagegevens |
| Secundaire NameNode |HEAD-knooppunten |50090 |HTTP |Controlepunt voor NameNode metagegevens |

### <a name="yarn-ports"></a>YARN-poorten

| Service | Knooppunten | Poort | Protocol | Beschrijving |
| --- | --- | --- | --- | --- |
| Resource Manager-webgebruikersinterface |HEAD-knooppunten |8088 |HTTP |Webgebruikersinterface voor Resource Manager |
| Resource Manager-webgebruikersinterface |HEAD-knooppunten |8090 |HTTPS |Webgebruikersinterface voor Resource Manager |
| Resource Manager-beheerinterface |HEAD-knooppunten |8141 |IPC |Voor voorbeelden van de toepassing (Hive, Pig, Hive server enz.) |
| Planner van Resource Manager |HEAD-knooppunten |8030 |HTTP |Beheerinterface |
| Toepassingsinterface van de Resource Manager |HEAD-knooppunten |8050 |HTTP |Adres van de interface van de manager Hallo toepassingen |
| NodeManager |Alle worker-knooppunten |30050 |&nbsp; |Hallo-adres van Hallo container manager |
| NodeManager webgebruikersinterface |Alle worker-knooppunten |30060 |HTTP |Resource manager-interface |
| Adres van de tijdlijn |HEAD-knooppunten |10200 |RPC |Hallo tijdlijn service RPC-service. |
| Tijdlijn webgebruikersinterface |HEAD-knooppunten |8181 |HTTP |Hallo tijdlijn service-webgebruikersinterface |

### <a name="hive-ports"></a>Hive-poorten

| Service | Knooppunten | Poort | Protocol | Beschrijving |
| --- | --- | --- | --- | --- |
| HiveServer2 |HEAD-knooppunten |10001 |Thrift |Service voor het verbinden van tooHive (Thrift/JDBC) |
| Hive-Metastore |HEAD-knooppunten |9083 |Thrift |Service voor het maken van verbinding tooHive metagegevens (Thrift/JDBC) |

### <a name="webhcat-ports"></a>WebHCat-poorten

| Service | Knooppunten | Poort | Protocol | Beschrijving |
| --- | --- | --- | --- | --- |
| WebHCat-server |HEAD-knooppunten |30111 |HTTP |Web-API boven op HCatalog en andere Hadoop-services |

### <a name="mapreduce-ports"></a>MapReduce-poorten

| Service | Knooppunten | Poort | Protocol | Beschrijving |
| --- | --- | --- | --- | --- |
| JobHistory |HEAD-knooppunten |19888 |HTTP |MapReduce JobHistory webgebruikersinterface |
| JobHistory |HEAD-knooppunten |10020 |&nbsp; |MapReduce JobHistory server |
| ShuffleHandler |&nbsp; |13562 |&nbsp; |Overdrachten tussenliggende kaart levert toorequesting verkleiningstoestellen |

### <a name="oozie"></a>Oozie

| Service | Knooppunten | Poort | Protocol | Beschrijving |
| --- | --- | --- | --- | --- |
| Oozie-server |HEAD-knooppunten |11000 |HTTP |URL voor Oozie-service |
| Oozie-server |HEAD-knooppunten |11001 |HTTP |Poort voor Oozie-beheerder |

### <a name="ambari-metrics"></a>Ambari metrische gegevens

| Service | Knooppunten | Poort | Protocol | Beschrijving |
| --- | --- | --- | --- | --- |
| Tijdlijn (toepassingsrevisies) |HEAD-knooppunten |6188 |HTTP |Hallo tijdlijn service-webgebruikersinterface |
| Tijdlijn (toepassingsrevisies) |HEAD-knooppunten |30200 |RPC |Hallo tijdlijn service-webgebruikersinterface |

### <a name="hbase-ports"></a>HBase-poorten

| Service | Knooppunten | Poort | Protocol | Beschrijving |
| --- | --- | --- | --- | --- |
| HMaster |HEAD-knooppunten |16000 |&nbsp; |&nbsp; |
| HMaster info Webgebruikersinterface |HEAD-knooppunten |16010 |HTTP |Hallo-poort voor Hallo HBase Master webgebruikersinterface |
| Regio-server |Alle worker-knooppunten |16020 |&nbsp; |&nbsp; |
| &nbsp; |&nbsp; |2181 |&nbsp; |Hallo-poort die clients tooconnect tooZooKeeper gebruiken |

### <a name="kafka-ports"></a>Kafka-poorten

| Service | Knooppunten | Poort | Protocol | Beschrijving |
| --- | --- | --- | --- | --- |
| Broker |Worker-knooppunten |9092 |[Protocol voor Kafka-kabel](http://kafka.apache.org/protocol.html) |Gebruikt voor communicatie van clients |
| &nbsp; |Zookeeper-knooppunten |2181 |&nbsp; |Hallo-poort die clients tooconnect tooZookeeper gebruiken |

### <a name="spark-ports"></a>Spark-poorten

| Service | Knooppunten | Poort | Protocol | URL-pad | Beschrijving |
| --- | --- | --- | --- | --- | --- |
| Spark Thrift-servers |HEAD-knooppunten |10002 |Thrift | &nbsp; | Service voor het verbinden van tooSpark SQL (Thrift/JDBC) |
| Livy server | HEAD-knooppunten | 8998 | HTTP | /batches | Service voor het uitvoeren van instructies, taken en toepassingen |

Voorbeelden:

* Livy: `curl "http://10.0.0.11:8998/batches"`. In dit voorbeeld `10.0.0.11` Hallo IP-adres van Hallo headnode die als host fungeert voor Hallo Livy service.
