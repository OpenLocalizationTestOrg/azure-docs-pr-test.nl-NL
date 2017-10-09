---
title: aaaWhat zijn HDInsight, Hallo Hadoop-technologiestack & clusters? - Azure | Microsoft Docs
description: Een inleiding tooHDInsight en Hallo Hadoop-technologiestack en onderdelen, waaronder Spark, Kafka, Hive, HBase voor big data-analyse.
keywords: Azure hadoop, azure hadoop, hadoop intro, hadoop inleiding, hadoop-technologiestack, intro toohadoop, inleiding toohadoop, wat is er een hadoop-cluster, wat is hadoop-cluster, wat is hadoop gebruikt voor
services: hdinsight
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: e56a396a-1b39-43e0-b543-f2dee5b8dd3a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: cgronlun
ms.openlocfilehash: 0aed3d1a6cf3c0cdc3b036cfa4865a2e0b58e2c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-hdinsight-hello-hadoop-technology-stack-and-hadoop-clusters"></a>Inleiding tooAzure HDInsight Hadoop-technologiestack Hallo en Hadoop-clusters
 Dit artikel bevat een inleiding tooAzure HDInsight, een cloud-distributie van Hadoop-technologiestack Hallo. Er wordt ook uitgelegd wat een Hadoop-cluster is en wanneer dit van pas komt. 

## <a name="what-is-hdinsight-and-hello-hadoop-technology-stack"></a>Wat is HDInsight en Hadoop-technologiestack Hallo? 
Azure HDInsight is een cloud-distributiepunt Hallo Hadoop-onderdelen op Hallo [Hortonworks Data Platform HDP ()](https://hortonworks.com/products/data-center/hdp/). [Apache Hadoop](http://hadoop.apache.org/) Hallo oorspronkelijke open-source framework voor gedistribueerde verwerking en analyse van grote gegevenssets op clusters of computers is. 


Hallo Hadoop-technologiestack omvat verwante software en -hulpprogramma's, waaronder Apache Hive, HBase, Spark, Kafka en vele andere. toosee beschikbaar Hadoop technologie stack-onderdelen in HDInsight, Zie [onderdelen en versies beschikbaar met HDInsight][component-versioning]. tooread meer informatie over Hadoop in HDInsight, Zie Hallo [Azure-functies voor HDInsight pagina](https://azure.microsoft.com/services/hdinsight/).

## <a name="what-is-a-hadoop-cluster-and-when-do-you-use-it"></a>Wat is een Hadoop-cluster en wanneer gebruikt u het?
*Hadoop* is ook een clustertype dat beschikt over:

* YARN voor taakplanning en resourcebeheer
* MapReduce voor parallelle verwerking
* Hallo Hadoop distributed file system (HDFS)
  
Hadoop-clusters worden het meest gebruikt voor batchverwerking van opgeslagen gegevens. Andere soorten clusters in HDInsight hebben extra mogelijkheden. Zo is Spark steeds populairder geworden vanwege de snellere, in-memory verwerking. Zie [Clustertypen in HDInsight](#overview) voor meer informatie.

## <a name="what-is-big-data"></a>Wat is big data?
Big data verwijst naar een grote hoeveelheid digitale gegevens van verschillende typen, zoals:

* Sensorgegevens van industriële apparatuur
* Klantenactiviteit verzameld op een website
* Een Twitter-nieuwsfeed

Big data wordt verzameld in steeds sneller groeiende volumes, met een steeds hogere snelheid en in een steeds groter wordend aantal indelingen. Het kan zijn historische (dat wil zeggen opgeslagen) of realtime (dat wil zeggen gestreamd vanaf Hallo bron). 

## <a name="overview"></a>Clustertypen in HDInsight
HDInsight omvat specifieke clustertypen en opties voor clusteraanpassing, zoals het toevoegen van onderdelen, hulpprogramma's en talen.

### <a name="spark-kafka-interactive-hive-hbase-customized-and-other-cluster-types"></a>Clusters van Spark, Kafka, Interactive Hive, HBase, aangepaste clusters en andere clustertypen
HDInsight biedt Hallo clustertypen te volgen:

* **[Apache Hadoop](https://wiki.apache.org/hadoop)**: maakt gebruik van [HDFS](#hdfs), [YARN](#yarn) resourcebeheer en een eenvoudige [MapReduce](#mapreduce) programming model tooprocess en batch gegevens parallel analyseren.
* **[Apache Spark](http://spark.apache.org/)**: een framework voor parallelle verwerking dat ondersteuning biedt voor in-memory verwerking tooboost Hallo prestaties van toepassingen voor big data-analyse, Spark werkt voor SQL, streamen van gegevens en machine learning. Zie [Wat is Apache Spark in HDInsight?](hdinsight-apache-spark-overview.md)
* **[Apache HBase](http://hbase.apache.org/)**: een NoSQL-database gebouwd op Hadoop. Deze biedt willekeurige toegang en sterke consistentie voor grote hoeveelheden (mogelijk miljarden rijen bij miljoenen kolommen) ongestructureerde en semi-gestructureerde gegevens. Zie [Wat is HBase in HDInsight?](hdinsight-hbase-overview.md)
* **[Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)**: een server voor de hosting van websites en het beheren van parallelle, gedistribueerde R-processen. Het biedt gegevenswetenschappers en statistici R programmeurs op aanvraag toegang tooscalable, gedistribueerde methoden van analyses in HDInsight. Zie [Overzicht van R Server in HDInsight](hdinsight-hadoop-r-server-overview.md).
* **[Apache Storm](https://storm.incubator.apache.org/)**: een gedistribueerd, realtime berekeningssysteem voor het snel verwerken van grote gegevensstromen. Storm wordt aangeboden als beheerd cluster in HDInsight. Zie [Realtime-sensorgegevens analyseren met Storm en Hadoop](hdinsight-storm-sensor-data-analysis.md).
* **[Voorbeeld van Apache Interactive Hive (ook bekend onder de naam: Live Long and Process)](https://cwiki.apache.org/confluence/display/Hive/LLAP)**: caching in geheugen voor interactieve en snellere Hive-query's. Zie [Interactive Hive gebruiken in HDInsight](hdinsight-hadoop-use-interactive-hive.md).
* **[Apache Kafka](https://kafka.apache.org/)**: een open-source platform dat wordt gebruikt voor het bouwen van pijplijnen en toepassingen voor het streamen van gegevens. Kafka biedt ook-berichtenwachtrij-functionaliteit die kunt u toopublish en zich abonneren toodata stromen. Zie [inleiding tooApache Kafka op HDInsight](hdinsight-apache-kafka-introduction.md).

U kunt ook configureren met behulp van de volgende methoden Hallo clusters:
* **[Domein-clusters preview](hdinsight-domain-joined-introduction.md)**: een cluster die lid zijn van de Active Directory-domein tooan zodat u kunt toegangsbeheer en ten behoeve van gegevens vormen.
* **[Aangepaste clusters met scriptacties](hdinsight-hadoop-customize-cluster-linux.md)**: clusters met scripts die extra onderdelen installeren en worden uitgevoerd tijdens de inrichting.

### <a name="example-cluster-customization-scripts"></a>Voorbeeldscripts voor het aanpassen van clusters
Scriptacties zijn Bash-scripts op Linux die tijdens de clusterinrichting worden uitgevoerd en die kunnen worden extra onderdelen van de gebruikte tooinstall op Hallo cluster. 

Hallo worden volgende voorbeeldscripts geleverd door HDInsight-team Hallo:

* **[HUE](hdinsight-hadoop-hue-linux.md)**: toointeract voor web-toepassingen die worden gebruikt met een cluster met een set. Alleen voor Linux-clusters.
* **[Giraph](hdinsight-hadoop-giraph-install-linux.md)**: Grafiekverwerking toomodel relaties tussen items of personen.
* **[Solr](hdinsight-hadoop-solr-install-linux.md)**: een bedrijfszoekplatform dat zoeken naar volledige tekst in gegevens mogelijk maakt.

Zie [Ontwikkeling van scriptacties met HDInsight](hdinsight-hadoop-script-actions-linux.md) voor informatie over het ontwikkelen van uw eigen scriptacties.

## <a name="components-and-utilities-on-hdinsight-clusters"></a>Onderdelen en hulpprogramma's in HDInsight-clusters
Hallo zijn volgende onderdelen en hulpprogramma's opgenomen op HDInsight-clusters:

* **[Ambari](#ambari)**: inrichting, beheer, controle en hulpprogramma's voor clusters.
* **[Avro](#avro)**  (Microsoft .NET-bibliotheek voor Avro): serialisatie van gegevens voor Hallo Microsoft .NET-omgeving. 
* **[Hive & HCatalog](#hive)**: uitvoeren van query‘s op basis van SQL, en een beheerlaag voor tabellen en opslag.
* **[Mahout](#mahout)**: voor schaalbare machine learning-toepassingen.
* **[MapReduce](#mapreduce)**: een ouder framework voor Hadoop, gedistribueerde verwerking en resourcebeheer. Zie [YARN](#yarn).
* **[Oozie](#oozie)**: werkstroombeheer.
* **[Phoenix](#phoenix)**: relationele databaselaag over HBase.
* **[Pig](#pig)**: eenvoudiger scripts uitvoeren voor MapReduce-transformaties.
* **[Sqoop](#sqoop)**: gegevens importeren en exporteren.
* **[Tez](#tez)**: Hiermee kunt u toorun van gegevensintensieve processen efficiënt op schaal.
* **[YARN](#yarn)**: bronbeheer die deel uitmaakt van de kernbibliotheek van Hadoop Hallo.
* **[ZooKeeper](#zookeeper)**: coördinatie van de processen in gedistribueerde systemen.

> [!NOTE]
> Zie voor meer informatie over specifieke onderdelen Hallo en versie-informatie [Hadoop-onderdelen en -versies in HDInsight][component-versioning]
>
>

### <a name="ambari"></a>Ambari
Apache Ambari is bedoeld voor het inrichten, beheren en controleren van Apache Hadoop-clusters. Bevat een intuïtieve verzameling hulpprogramma's voor operators en een krachtige reeks API's die verbergen Hallo complexiteit van Hadoop Hallo werking van clusters vereenvoudigen. HDInsight-clusters op Linux bieden beide Ambari-webgebruikersinterface Hallo en Hallo Ambari REST-API. Ambari-weergaven op HDInsight-clusters bieden interfacemogelijkheden voor invoegtoepassingen.
Zie [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md) (HDInsight-clusters beheren met Ambari) en <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">Ambari API Reference</a> (Ambari API-naslaghandleiding).

### <a name="avro"></a>Avro (Microsoft .NET-bibliotheek voor Avro)
Hallo Microsoft .NET-bibliotheek voor Avro implementeert Hallo Apache Avro compacte binaire gegevens DIF-indeling voor serialisatie Hallo Microsoft .NET-omgeving. Het betreft een taal-agnostisch schema waarmee gegevens die zijn geserialiseerd in de ene taal in een andere taal kunnen worden gelezen. Gedetailleerde informatie over het Hallo-indeling vindt u in Hallo < target = _ "blank" href = "http://avro.apache.org/docs/current/spec.html" > Apache Avro-specificatie</a>. Hallo-indeling van het Avro-bestanden ondersteunt Hallo gedistribueerde MapReduce-programmeermodel: bestanden zijn 'splittable', wat betekent dat u kunt elk punt in een bestand en beginnen met lezen van een bepaald blok. toofind hoe, Zie [gegevens serialiseren met Hallo Microsoft .NET-bibliotheek voor Avro](hdinsight-dotnet-avro-serialization.md). Cluster op basis van Linux-ondersteuning toocome.

### <a name="hdfs"></a>HDFS
Hadoop Distributed File System (HDFS) is een bestandssysteem dat met YARN en MapReduce, is het Hallo-core van Hadoop-technologie. Het Hallo standaardbestandssysteem voor Hadoop-clusters op HDInsight's. Zie [Use Azure storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md) (Azure-opslag gebruiken met Azure HDInsight-clusters).

### <a name="hive"></a>Hive & HCatalog
<a target="_blank" href="http://hive.apache.org/">Apache Hive</a> is gebouwd op Hadoop waarmee u tooquery datawarehouse op en grote gegevenssets in gedistribueerde opslag beheren met behulp van een SQL-achtige taal genaamd HiveQL. Hive is, net zoals Pig, een abstractielaag bovenop MapReduce en zet query's om in een reeks MapReduce-taken. Hive dichter tooa relationeel databasebeheersysteem dan Pig is en wordt gebruikt met meer gestructureerde gegevens. Voor ongestructureerde gegevens is Pig Hallo betere keuze. Zie [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md).

<a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a> is een tabel- en opslagbeheerlaag voor Hadoop die u een relationele weergave van gegevens biedt. In HCatalog kunt u lees- en schrijfbewerkingen uitvoeren op bestanden in elke indeling die compatibel is met een Hive SerDe (serializer-deserializer).

### <a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a> is een bibliotheek met machine learning-algoritmen die worden uitgevoerd in Hadoop. Met behulp van statistieken, systemen toolearn van gegevens en toouse voorbij resultaten toodetermine toekomstig gedrag leren gebruiken machine learning-toepassingen. Zie [Filmaanbevelingen genereren met Mahout op Hadoop](hdinsight-mahout.md).

### <a name="mapreduce"></a>MapReduce
MapReduce is Hallo oudere softwareframework voor Hadoop voor schrijftoepassingen toobatch proces grote gegevenssets parallel. Een MapReduce-taak worden grote gegevenssets gesplitst en Hallo gegevens georganiseerd in sleutel-waardeparen voor verwerking. MapReduce-taken worden uitgevoerd in [YARN](#yarn). Zie <a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> in Hallo Hadoop-Wiki.

### <a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a> is een coördinatiesysteem voor werkstromen waarmee Hadoop-taken worden beheerd. Het is geïntegreerd met Hallo Hadoop-stack en biedt ondersteuning voor Hadoop-taken voor MapReduce, Pig, Hive en Sqoop. Het kan ook worden de gebruikte tooschedule taken specifieke tooa systeem, zoals Java-programma's of shell-scripts. Zie [Use Oozie with Hadoop](hdinsight-use-oozie-linux-mac.md) (Oozie gebruiken met Hadoop).

### <a name="phoenix"></a>Phoenix
<a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a> is een relationele databaselaag over HBase. Phoenix bevat een JDBC-stuurprogramma dat kunt u tooquery en SQL-tabellen rechtstreeks beheren. Phoenix vertaalt query‘s en andere instructies naar systeemeigen NoSQL API-aanroepen (in plaats van gebruik te maken van MapReduce). Hierdoor worden snellere toepassingen mogelijk die zijn gebouwd op NoSQL-opslag. Zie [Apache Phoenix en SQuirreL gebruiken met HBase-clusters](hdinsight-hbase-phoenix-squirrel.md).

### <a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a> is een platform van hoog niveau waarmee u complexe MapReduce-transformaties tooperform op grote gegevenssets met behulp van een eenvoudige scripttaal genaamd Pig Latin. Pig vertaalt de Pig Latin-scripts Hallo zodat ze kunnen worden uitgevoerd in Hadoop. U kunt door de gebruiker gedefinieerde functies (UDF's) tooextend Pig Latin maken. Zie [Use Pig with Hadoop](hdinsight-use-pig.md) (Pig gebruiken met Hadoop).

### <a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a> is een hulpprogramma waarmee zo efficiënt mogelijk bulksgewijs gegevens kunnen worden overgebracht tussen Hadoop en relationele databases, zoals SQL of andere gestructureerde gegevensopslag. Zie [Sqoop gebruiken met Hadoop](hdinsight-use-sqoop.md).

### <a name="tez"></a>Tez
<a  target="_blank" href="http://tez.apache.org/">Apache Tez</a> is een toepassingsframework dat is gebouwd op Hadoop YARN. Hiermee kunnen complexe, acyclische grafieken voor algemene gegevensverwerking worden uitgevoerd. Het is een flexibelere en krachtigere opvolger toohello MapReduce-framework waarmee gegevensintensieve processen, zoals Hive, toorun efficiënter op schaal. Zie [het gedeelte 'Apache Tez gebruiken voor verbeterde prestaties' in het artikel 'Hive en HiveQL gebruiken'](hdinsight-use-hive.md#usetez).

### <a name="yarn"></a>YARN
Apache YARN is Hallo volgende generatie van MapReduce (MapReduce 2.0 of MRv2) en biedt ondersteuning voor scenario's voor gegevensverwerking dan MapReduce met grotere schaalbaarheid en realtime verwerking. YARN biedt resourcebeheer en een gedistribueerd toepassingsframework. MapReduce-taken worden uitgevoerd op YARN. Zie <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop YARN</a>.

### <a name="zookeeper"></a>ZooKeeper
<a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a> coördineert processen in grote gedistribueerde systemen met behulp van een gedeelde hiërarchische naamruimte met gegevensregisters (znodes). Znodes bevatten kleine hoeveelheden metagegevens informatie die nodig is toocoordinate processen: status, locatie en configuratie. Bekijk een voorbeeld van [ZooKeeper met een HBase-cluster en Apache Phoenix](hdinsight-hbase-phoenix-squirrel-linux.md). 

## <a name="programming-languages-on-hdinsight"></a>Programmeertalen in HDInsight
HDInsight-clusters (Spark, HBase, Kafka, Hadoop en andere clusters) bieden ondersteuning voor een aantal programmeertalen, maar sommige hiervan worden niet standaard geïnstalleerd. Voor bibliotheken, modules of pakketten niet standaard geïnstalleerd, [gebruik van een script actie tooinstall Hallo onderdeel](hdinsight-hadoop-script-actions-linux.md). 

### <a name="default-programming-language-support"></a>Standaardondersteuning voor programmeertalen
Standaard bieden HDInsight-clusters ondersteuning voor:

* Java
* Python

Extra talen kunnen worden geïnstalleerd via [scriptacties](hdinsight-hadoop-script-actions-linux.md).

### <a name="java-virtual-machine-jvm-languages"></a>JVM-talen (Java Virtual Machine)
Veel andere talen dan Java kunnen worden uitgevoerd op een virtuele Java-machine (JVM); uitvoeren van sommige talen kan echter extra onderdelen worden geïnstalleerd op Hallo cluster nodig.

De volgende JVM-talen worden op HDInsight-clusters ondersteund: 

* Clojure
* Jython (Python voor Java)
* Scala

### <a name="hadoop-specific-languages"></a>Hadoop-specifieke talen
HDInsight-clusters bieden ondersteuning voor talen die specifieke toohello Hadoop-technologiestack zijn na Hallo:

* Pig Latin voor Pig-taken
* HiveQL voor Hive-taken en SparkSQL

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard en HDInsight Premium
HDInsight heeft twee categorieën aanbiedingen voor big data-clouds: Standard en Premium. HDInsight Standard biedt een bedrijfscluster dat organisaties toorun hun big data-werkbelastingen gebruiken kunnen. HDInsight Premium bouwt voort op de Standard-uitvoering en biedt geavanceerde mogelijkheden voor analyse en beveiliging voor een HDInsight-cluster. Zie [Azure HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium) voor meer informatie.

## <a name="microsoft-business-intelligence-and-hdinsight"></a>Microsoft Business Intelligence en HDInsight
Bekend business intelligence (BI)-hulpprogramma's ophalen, analyseren, en gegevens die zijn geïntegreerd met HDInsight met behulp van beide Hallo Power Query-invoegtoepassing of stuurprogramma Microsoft Hive ODBC Hallo:

* [Verbinding maken met Excel tooHadoop met Power Query](hdinsight-connect-excel-power-query.md): meer informatie over hoe tooconnect Excel toohello Azure Storage-account worden opgeslagen gegevens van uw HDInsight-cluster Hallo met behulp van Microsoft Power Query voor Excel. Windows-werkstation is vereist. 
* [Verbinding maken met Excel tooHadoop Hello stuurprogramma Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md): meer informatie over hoe tooimport gegevens uit HDInsight met Hallo Microsoft Hive ODBC-stuurprogramma. Windows-werkstation is vereist. 
* [Microsoft Cloud Platform](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx): meer informatie over Power BI voor Office 365, SQL Server-proefversie Hallo downloaden en instellen van SharePoint Server 2013 en SQL Server BI.
* [SQL Server Analysis Services](http://msdn.microsoft.com/library/hh231701.aspx)
* [SQL Server Reporting Services](http://msdn.microsoft.com/library/ms159106.aspx)


## <a name="next-steps"></a>Volgende stappen

* [Aan de slag met Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md): een Snel starten-zelfstudie voor het inrichten van HDInsight Hadoop-clusters en het uitvoeren van Hive-voorbeeldquery‘s.
* [Aan de slag met Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md): een Snel starten-zelfstudie voor het maken van een Spark-cluster en het uitvoeren van interactieve Spark SQL-query's.
* [R Server gebruiken op HDInsight](hdinsight-hadoop-r-server-get-started.md): informatie over het gebruik van R Server in HDInsight Premium.
* [HDInsight-clusters inrichten](hdinsight-hadoop-provision-linux-clusters.md): meer informatie over hoe een HDInsight Hadoop-cluster via tooprovision hello Azure-portal, Azure CLI of Azure PowerShell.


[component-versioning]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/