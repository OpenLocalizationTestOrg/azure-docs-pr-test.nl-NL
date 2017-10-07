---
title: aaaUse Apache Kafka met Storm op HDInsight - Azure | Microsoft Docs
description: "Apache Kafka wordt geïnstalleerd met Apache Storm op HDInsight. Meer informatie over hoe toowrite tooKafka en lees, met behulp van Hallo KafkaBolt en KafkaSpout-onderdelen met Storm. U leert ook hoe toouse Hallo lichtstroom framework toodefine en het verzenden van Storm-topologieën."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a>Apache Kafka (preview) met Storm op HDInsight gebruiken

Meer informatie over hoe toouse Apache Storm tooread van en schrijven tooApache Kafka. Dit voorbeeld wordt ook hoe toosave gegevens van een Storm-topologie toohello HDFS-compatibele bestandssysteem die door HDInsight worden gebruikt.

> [!NOTE]
> Hallo stappen in dit document wordt een Azure-resourcegroep met zowel een Storm op HDInsight en een Kafka op HDInsight-cluster maken Deze clusters zijn beide zich binnen een virtueel netwerk van Azure, waardoor Hallo Storm-cluster toodirectly communiceren met de Hallo Kafka-cluster.
> 
> Wanneer u klaar bent met de stappen in dit document Hallo onthouden toodelete Hallo clusters tooavoid overtollige kosten.

## <a name="get-hello-code"></a>Hallo code ophalen

Hallo-code voor Hallo-voorbeeld gebruikt in dit document is beschikbaar op [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).

toocompile dit project, moet u na de configuratie voor uw ontwikkelomgeving Hallo:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) of hoger. HDInsight 3.5 of hoger vereisen Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

* Een SSH-client (u moet Hallo `ssh` en `scp` opdrachten) - informatie, Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Een teksteditor of IDE.

Hallo kunnen volgende omgevingsvariabelen worden ingesteld wanneer u Java en Hallo JDK op uw ontwikkelwerkstation installeert. Echter, moet u controleren of ze bestaan en dat ze de juiste waarden voor uw systeem Hallo bevatten.

* `JAVA_HOME`-moet verwijzen toohello directory waarin hello JDK is geïnstalleerd.
* `PATH`-moet bevatten Hallo paden te volgen:
  
    * `JAVA_HOME`(of gelijkwaardige Hallo-pad).
    * `JAVA_HOME\bin`(of gelijkwaardige Hallo-pad).
    * Hallo-map is waarin Maven is geïnstalleerd.

## <a name="create-hello-clusters"></a>Hallo-clusters maken

Apache Kafka op HDInsight biedt geen toegang tot toohello Kafka beleggingsmakelaars via openbaar internet Hallo. Alles wat vertelt tooKafka moet zich in hetzelfde virtuele Azure-netwerk als knooppunten in Hallo HALLO hallo Kafka-cluster. In dit voorbeeld bevinden Hallo Kafka zowel Storm-clusters zich in een Azure-netwerk. Hallo volgende diagram ziet u hoe de communicatie tussen clusters met Hallo loopt:

![Diagram van Storm en Kafka clusters in een Azure-netwerk](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> Andere services op Hallo cluster Hallo zoals SSH en Ambari toegankelijk is via internet. Zie voor meer informatie over Hallo openbare poorten beschikbaar met HDInsight [poorten en URI's die worden gebruikt door HDInsight](hdinsight-hadoop-port-settings-for-services.md).

U kunt een Azure-netwerk Kafka, maken en Storm-clusters handmatig, zijn maar er eenvoudiger toouse een Azure Resource Manager-sjabloon. Gebruik Hallo volgende stappen uit voor een Azure-netwerk Kafka, toodeploy en Storm-clusters tooyour Azure-abonnement.

1. Hallo na de knop toosign in tooAzure en open Hallo-sjabloon in hello Azure-portal gebruiken.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello Azure Resource Manager-sjabloon bevindt zich op **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**. Hiermee maakt u Hallo resources te volgen:
    
    * Azure-resourcegroep
    * Azure Virtual Network
    * Azure-opslagaccount
    * Kafka op HDInsight versie 3.6 (drie worker-knooppunten)
    * Storm op HDInsight versie 3.6 (drie worker-knooppunten)

  > [!WARNING]
  > de beschikbaarheid van de tooguarantee van Kafka op HDInsight, uw cluster moet ten minste drie worker-knooppunten bevatten. Deze sjabloon maakt een Kafka-cluster dat drie worker-knooppunten bevat.

2. Gebruik Hallo volgen richtlijnen toopopulate Hallo vermeldingen op Hallo **aangepaste implementatie** blade:
   
    ![Aangepaste HDInsight-implementatie](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * **Resourcegroep**: Maak een groep of een bestaande set selecteren. Deze groep bevat Hallo HDInsight-cluster.
   
    * **Locatie**: Selecteer een locatie geografisch sluiten tooyou.

    * **Clusternaam baseren**: deze waarde wordt gebruikt als basisnaam voor clusters met Storm en Kafka Hallo Hallo. Bijvoorbeeld, voeren **hdi** maakt een Storm-cluster met de naam **storm hdi** en een Kafka-cluster met de naam **kafka hdi**.
   
    * **Aanmeldingsnaam van gebruiker cluster**: Hallo-beheerdersgebruikersnaam voor Hallo Storm en Kafka-clusters.
   
    * **Aanmeldingswachtwoord cluster**: Hallo beheerder gebruikerswachtwoord voor Hallo Storm en Kafka-clusters.
    
    * **SSH-gebruikersnaam**: Hallo SSH gebruiker toocreate voor Hallo Storm en Kafka-clusters.
    
    * **SSH-wachtwoord**: Hallo-wachtwoord voor Hallo SSH-gebruiker voor Hallo Storm en Kafka-clusters.

3. Lees Hallo **voorwaarden en bepalingen**, en selecteer vervolgens **ik ga akkoord toohello voorwaarden bovengenoemde**.

4. Controleer ten slotte **pincode toodashboard** en selecteer vervolgens **aankoop**. Het duurt ongeveer 20 minuten toocreate Hallo-clusters.

Zodra het Hallo-resources zijn gemaakt, wordt Hallo blade voor de resourcegroep Hallo weergegeven.

![Resourcegroepblade voor Hallo vnet en clusters](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> Merk op dat de namen van HDInsight-clusters Hallo Hallo zijn **storm BASENAME** en **kafka BASENAME**, waarbij BASENAME Hallo-naam die u hebt opgegeven toohello sjabloon. U deze namen in latere stappen gebruiken om verbinding te maken van clusters toohello.

## <a name="understanding-hello-code"></a>Understanding Hallo code

Dit project bevat twee topologieën:

* **KafkaWriter**: gedefinieerd door Hallo **writer.yaml** , deze topologie schrijft willekeurig zinnen tooKafka hello KafkaBolt opgegeven met Apache Storm gebruiken.

    Deze topologie maakt gebruik van een aangepaste **SentenceSpout** onderdeel toogenerate willekeurig zinnen.

* **KafkaReader**: gedefinieerd door Hallo **reader.yaml** -bestand, deze topologie leest de gegevens uit Kafka hello KafkaSpout opgegeven met Apache Storm gebruiken en klik vervolgens logboeken Hallo toostdout gegevens.

    Deze topologie gebruikt Hallo Storm HdfsBolt toowrite-gegevensopslag toodefault voor Hallo Storm-cluster.
### <a name="flux"></a>Lichtstroom

Hallo-topologieën worden gedefinieerd met [lichtstroom](https://storm.apache.org/releases/1.1.0/flux.html). Lichtstroom werd geïntroduceerd in 0.10.x Storm en kunt u tooseparate hello topologieconfiguratie vanuit Hallo-code. Hallo-topologie is voor de topologieën die gebruikmaken van Hallo lichtstroom framework, gedefinieerd in een YAML-bestand. Hallo YAML-bestand kan worden opgenomen als onderdeel van het Hallo-topologie. Het kan ook een zelfstandig bestand gebruikt bij het verzenden van Hallo topologie zijn. Lichtstroom ondersteunt ook het vervangen van de variabelen tijdens runtime, die wordt gebruikt in dit voorbeeld.

Hallo zijn volgende parameters ingesteld tijdens de uitvoering voor deze topologieën:

* `${kafka.topic}`: de naam van de Hallo Hallo Kafka-onderwerp dat Hallo topologieën lezen/schrijven naar.

* `${kafka.broker.hosts}`: Hallo die Hallo Kafka makelaars die worden uitgevoerd op host. Hallo broker informatie wordt gebruikt door Hallo KafkaBolt bij het schrijven van tooKafka.

* `${kafka.zookeeper.hosts}`: Hallo-hosts die Zookeeper op wordt uitgevoerd in Hallo Kafka-cluster.

Zie voor meer informatie over topologieën lichtstroom [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="download-and-compile-hello-project"></a>Download en Hallo project compileren

1. Op uw ontwikkelomgeving downloaden Hallo-project uit [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), opent u een opdrachtregel en de locatie van de toohello mappen dat u hebt gedownload Hallo project wijzigen.

2. Van Hallo **hdinsight, storm, java, kafka** map gebruik Hallo volgende opdracht toocompile Hallo-project en maak een pakket voor implementatie:

  ```bash
  mvn clean package
  ```

    Hallo pakket proces maakt een bestand met de naam `KafkaTopology-1.0-SNAPSHOT.jar` in Hallo `target` directory.

3. Gebruik Hallo volgende opdrachten toocopy Hallo pakket tooyour Storm op HDInsight-cluster. Vervang **gebruikersnaam** met Hallo SSH-gebruikersnaam voor Hallo-cluster. Vervang **BASENAME** met Hallo basisnaam die u hebt gebruikt bij het Hallo-cluster maken.

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    Voer desgevraagd Hallo het wachtwoord waarmee u bij het maken van clusters Hallo.

## <a name="configure-hello-topology"></a>Hallo-topologie configureren

1. Gebruik een van de methoden toodiscover na Hallo Hallo Kafka broker hosts:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Hallo Bash-voorbeeld wordt ervan uitgegaan dat `$CLUSTERNAME` Hallo naam bevat van Hallo HDInsight-cluster. Ook wordt ervan uitgegaan dat [jq](https://stedolan.github.io/jq/) is geïnstalleerd. Wanneer u wordt gevraagd, voert u Hallo wachtwoord voor aanmeldingsaccount Hallo-cluster.

    Hallo-waarde die het resultaat is vergelijkbaar toohello volgende tekst:

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > Hoewel er mogelijk meer dan twee broker hosts voor uw cluster, hoeft u niet een volledige lijst met alle hosts tooclients tooprovide. Een of twee is voldoende.

2. Gebruik een van de Hallo methoden toodiscover hello Kafka Zookeeper hosts te volgen:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Hallo Bash-voorbeeld wordt ervan uitgegaan dat `$CLUSTERNAME` Hallo naam bevat van Hallo HDInsight-cluster. Ook wordt ervan uitgegaan dat [jq](https://stedolan.github.io/jq/) is geïnstalleerd. Wanneer u wordt gevraagd, voert u Hallo wachtwoord voor aanmeldingsaccount Hallo-cluster.

    Hallo-waarde die het resultaat is vergelijkbaar toohello volgende tekst:

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > Hoewel er meer dan twee Zookeeper-knooppunten, hoeft u niet een volledige lijst met alle hosts tooclients tooprovide. Een of twee is voldoende.

    Deze waarde niet opslaan omdat het wordt later gebruikt.

3. Hallo bewerken `dev.properties` bestand in de hoofdmap Hallo van Hallo-project. Hallo Broker en Zookeeper hosts informatie toohello overeenkomende regels in dit bestand toevoegen. Hallo is volgende voorbeeld geconfigureerd met behulp van voorbeeldwaarden Hallo uit de vorige stappen Hallo:

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. Hallo opslaan `dev.properties` bestands- en gebruik vervolgens Hallo na de opdracht tooupload het toohello Storm-cluster:

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    Vervang **gebruikersnaam** met Hallo SSH-gebruikersnaam voor Hallo-cluster. Vervang **BASENAME** met Hallo basisnaam die u hebt gebruikt bij het Hallo-cluster maken.

## <a name="start-hello-writer"></a>Hallo writer starten

1. Gebruik hello tooconnect toohello Storm-cluster via SSH te volgen. Vervang **gebruikersnaam** met Hallo SSH-gebruikersnaam gebruikt bij het Hallo-cluster maken. Vervang **BASENAME** met Hallo basisnaam gebruikt bij het Hallo-cluster maken.

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    Voer desgevraagd Hallo het wachtwoord waarmee u bij het maken van clusters Hallo.
   
    Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

2. Gebruik van Hallo SSH-verbinding, Hallo opdracht toocreate hello Kafka onderwerp gebruikt door Hallo topologie te volgen:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    Vervang `$KAFKAZKHOSTS` Hello Zookeeper hosten informatie die u in de vorige sectie Hallo opgehaald.

2. Gebruik van Hallo SSH-verbinding toohello Storm-cluster Hallo opdracht toostart Hallo writer topologie te volgen:

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    Hallo-parameters gebruikt met deze opdracht zijn:

    * `org.apache.storm.flux.Flux`: Gebruik lichtstroom tooconfigure en voer deze topologie.

    * `--remote`: Hallo topologie tooNimbus verzenden. Hallo-topologie wordt verdeeld over Hallo worker-knooppunten in cluster Hallo.

    * `-R /writer.yaml`: Gebruik Hallo `writer.yaml` bestand tooconfigure Hallo topologie. `-R`Hiermee wordt aangegeven dat deze bron wordt opgenomen in Hallo jar-bestand. Het is in de hoofdmap Hallo van Hallo jar, dus `/writer.yaml` Hallo pad tooit is.

    * `--filter`: Vullen vermeldingen in Hallo `writer.yaml` topologie met behulp van de waarden in Hallo `dev.properties` bestand. Bijvoorbeeld: waarde van Hallo Hallo `kafka.topic` vermelding in Hallo-bestand is gebruikte tooreplace hello `${kafka.topic}` vermelding in de definitie van de topologie Hallo.

5. Zodra het Hallo-topologie is gestart, gebruikt u Hallo opdracht tooverify dat het wegschrijven van gegevens toohello Kafka onderwerp te volgen:

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    Vervang `$KAFKAZKHOSTS` Hello Zookeeper hosten informatie die u in de vorige sectie Hallo opgehaald.

    Met deze opdracht maakt gebruik van een script met Kafka toomonitor Hallo onderwerp verzonden. Na korte tijd, moet het eerst willekeurig zinnen die zijn geschreven toohello onderwerp retourneren. Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    Gebruik Ctrl + c toostop Hallo script.

## <a name="start-hello-reader"></a>Hallo lezer starten

1. Gebruik van Hallo SSH-sessie toohello Storm-cluster Hallo opdracht toostart Hallo lezer topologie te volgen:

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. Zodra het Hallo-topologie wordt gestart, opent u Hallo Storm-gebruikersinterface. Deze web-UI bevindt zich op https://storm-BASENAME.azurehdinsight.net/stormui. Vervang __BASENAME__ met Hallo basisnaam gebruikt bij het Hallo-cluster is gemaakt. 

    Wanneer u wordt gevraagd, Hallo beheerder aanmeldingsnaam gebruiken (standaard `admin`) en het wachtwoord als Hallo-cluster is gemaakt. Er is een webpagina vergelijkbare toohello installatiekopie te volgen:

    ![Storm-gebruikersinterface](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. Hallo Storm-gebruikersinterface, selecteer Hallo __kafka-lezer__ koppeling in Hallo __Topology Summary__ toodisplay informatie over Hallo sectie __kafka-lezer__ topologie.

    ![Samenvatting van Hallo Storm-webgebruikersinterface topologie](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. toodisplay informatie over exemplaren van Hallo berichtenlogboek bolt onderdeel, selecteer Hallo Hallo __berichtenlogboek bolt__ koppeling in Hallo __Bolts (alle tijd)__ sectie.

    ![Berichtenlogboek bolt koppeling in Hallo bolts sectie](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. In Hallo __Executor__ sectie, selecteert u een koppeling in Hallo __poort__ kolom toodisplay logboekregistratie informatie over dit exemplaar van het Hallo-onderdeel.

    ![Executor koppelen](./media/hdinsight-apache-storm-with-kafka/executors.png)

    Hallo-logboek bevat een logboek van Hallo-gegevens lezen uit Hallo Kafka onderwerp. Hallo-informatie in Hallo-logboek is vergelijkbaar toohello volgende tekst:

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a>Hallo topologieën stoppen

Gebruik van een SSH-sessie toohello Storm-cluster Hallo opdrachten toostop Hallo Storm-topologieën te volgen:

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a>Hallo-cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Aangezien Hallo stappen in dit document beide maken clusters in dezelfde Azure-resourcegroep hello, kunt u de resourcegroep Hallo in hello Azure-portal verwijderen. Verwijderen van het Hallo-resourcegroep Hiermee verwijdert u alle resources die zijn gemaakt op basis van dit document.

## <a name="next-steps"></a>Volgende stappen

Zie voor meer voorbeeldtopologieën die kunnen worden gebruikt met Storm op HDInsight [voorbeeld Storm-topologieën en -onderdelen](hdinsight-storm-example-topology.md).

Zie voor meer informatie over de implementatie en controle-topologieën op Linux gebaseerde HDInsight [implementeren en beheren van Apache Storm-topologieën op HDInsight op basis van Linux](hdinsight-storm-deploy-monitor-topology-linux.md)