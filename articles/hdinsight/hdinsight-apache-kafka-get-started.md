---
title: aaaStart met Apache Kafka - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe een Apache Kafka toocreate in Azure HDInsight-cluster. Meer informatie over hoe toocreate onderwerpen, abonnees en consumenten.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a>Met Apache Kafka (preview) in HDInsight beginnen

Meer informatie over hoe toocreate en gebruik een [Apache Kafka](https://kafka.apache.org) cluster in Azure HDInsight. Kafka is een open-source, gedistribueerd streamingplatform dat beschikbaar is met HDInsight. Dit wordt vaak gebruikt als broker bericht, aangezien deze vergelijkbare functionaliteit biedt tooa voor publiceren / abonneren berichtenwachtrij.

> [!NOTE]
> Er zijn momenteel twee versies van Kafka beschikbaar met HDInsight: 0.9.0 (HDInsight 3.4) en 0.10.0 (HDInsight 3.5 en 3.6). Hallo stappen in dit document wordt ervan uitgegaan dat u van Kafka op HDInsight 3.6 gebruikmaakt.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a>Een Kafka-cluster maken

Gebruik Hallo stappen toocreate een Kafka op HDInsight-cluster te volgen:

1. Van Hallo [Azure-portal](https://portal.azure.com), selecteer **+ nieuw**, **Intelligence en analyse**, en selecteer vervolgens **HDInsight**.
   
    ![Een HDInsight-cluster maken](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. Van **basisbeginselen**, Voer Hallo volgende informatie:

    * **Clusternaam**: Hallo-naam van Hallo HDInsight-cluster.
    * **Abonnement**: Hallo abonnement toouse selecteren.
    * **Gebruikersnaam voor aanmelding cluster** en **Cluster aanmeldingswachtwoord**: Hallo aanmelding bij het openen van Hallo-cluster via HTTPS. U gebruikt deze referenties tooaccess services zoals Hallo Ambari-Webgebruikersinterface of REST-API.
    * **Secure Shell (SSH) gebruikersnaam**: Hallo-aanmeldingsnaam die wordt gebruikt bij het openen van Hallo-cluster via SSH. Standaard is Hallo wachtwoord Hallo hetzelfde als Hallo aanmelding het wachtwoord van het cluster.
    * **Resourcegroep**: Hallo resource groep toocreate Hallo cluster in.
    * **Locatie**: hello Azure-regio toocreate Hallo cluster in.
   
 ![Abonnement selecteren](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. Selecteer **type Cluster**, en de volgende set Hallo waarden uit **clusterconfiguratie**:
   
    * **Clustertype**: Kafka

    * **Versie**: Kafka 0.10.0 (HDI 3.6)

    * **Clusterlaag**: standaard
     
 Gebruik tot slot Hallo **Selecteer** knop toosave instellingen.
     
 ![Clustertype selecteren](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. Gebruik na het selecteren van clustertype Hallo Hallo __Selecteer__ knoptype tooset Hallo-cluster. Gebruik vervolgens Hallo __volgende__ knop toofinish basisconfiguratie.

5. Selecteer of maak bij **Opslag** een opslagaccount. Laat Hallo andere velden op Hallo standaardwaarden voor Hallo stappen in dit document. Gebruik Hallo __volgende__ knop toosave opslagconfiguratie.

    ![Hallo-opslag-accountinstellingen voor HDInsight instellen](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. Van __toepassingen (optioneel)__, selecteer __volgende__ toocontinue. Er zijn geen toepassingen vereist voor dit voorbeeld.

7. Van __clustergrootte__, selecteer __volgende__ toocontinue.

    > [!WARNING]
    > de beschikbaarheid van de tooguarantee van Kafka op HDInsight, uw cluster moet ten minste drie worker-knooppunten bevatten.

    ![Set Hallo Kafka clustergrootte](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > Hallo **schijven per werkrolknooppunt** besturingselementen voor gegevensinvoer Hallo schaalbaarheid van Kafka op HDInsight. Zie voor meer informatie [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).

8. Van __geavanceerde instellingen__, selecteer __volgende__ toocontinue.

9. Van Hallo **samenvatting**, Controleer de configuratie van Hallo voor Hallo-cluster. Gebruik Hallo __bewerken__ koppelingen toochange alle instellingen die onjuist zijn. Gebruik tot slot the__Create__ knop toocreate Hallo cluster.
   
    ![Samenvatting clusterconfiguratie](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > Too20 minuten toocreate Hallo cluster kan duren.

## <a name="connect-toohello-cluster"></a>Verbinding maken met cluster toohello

> [!IMPORTANT]
> Bij het uitvoeren van Hallo stappen uit te voeren, moet u een SSH-client. Zie voor meer informatie, Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

Gebruik van de client SSH tooconnect toohello cluster:

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

Vervang **SSHUSER** met Hallo SSH gebruikersnaam die u hebt opgegeven tijdens het maken van het cluster. Vervang **CLUSTERNAME** met de naam van de cluster Hallo Hallo.

Voer desgevraagd Hallo wachtwoord die u voor Hallo SSH-account gebruikt.

Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

## <a id="getkafkainfo"></a>Hallo Zookeeper en Broker hostinformatie ophalen

Als u werkt met Kafka, moet u weten twee waarden van de host. Hallo *Zookeeper* hosts en Hallo *Broker* hosts. Deze hosts worden gebruikt met Hallo Kafka API en veel Hallo-hulpprogramma's die worden geleverd met Kafka.

Gebruik Hallo volgende stappen toocreate omgevingsvariabelen die Hallo hostinformatie bevatten. Deze omgevingsvariabelen worden gebruikt in Hallo stappen in dit document.

1. Van een cluster met SSH-verbinding toohello, gebruik Hallo volgende tooinstall Hallo opdracht `jq` hulpprogramma. Dit hulpprogramma is gebruikte tooparse JSON-documenten en is handig bij het ophalen van informatie over de host van de Hallo broker:
   
    ```bash
    sudo apt -y install jq
    ```

2. tooset hello omgevingsvariabelen met informatie opgehaald van Ambari, gebruik Hallo volgende opdrachten:

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > Stel `CLUSTERNAME=` toohello naam Hallo Kafka-cluster. Stel `PASSWORD=` toohello (admin) aanmeldingswachtwoord u hebt gebruikt bij het maken van Hallo-cluster.

    Hallo volgende tekst is een voorbeeld van de inhoud van Hallo `$KAFKAZKHOSTS`:
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    Hallo volgende tekst is een voorbeeld van de inhoud van Hallo `$KAFKABROKERS`:
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > Hallo `cut` opdracht gebruikte tootrim Hallo lijst met hosts tootwo hostvermeldingen is. U hoeft niet tooprovide Hallo volledige lijst met hosts die bij het maken van een consumer Kafka of de producent.
   
    > [!WARNING]
    > Vertrouw niet op Hallo informatie geretourneerd door deze sessie tooalways nauwkeurig worden. Als u Hallo-cluster schaalt, worden nieuwe beleggingsmakelaars toegevoegd of verwijderd. Als een fout optreedt en een knooppunt wordt vervangen, kan Hallo-hostnaam voor het Hallo-knooppunt veranderen.
    >
    > Kort voordat u deze tooensure die u hebt geldige informatie gebruiken, moet u Hallo Zookeeper en broker hosts informatie ophalen.

## <a name="create-a-topic"></a>Een onderwerp maken

Kafka slaat gegevensstromen op in categorieën, zogenaamde *onderwerpen*. Gebruik van een SSH-verbinding tooa cluster headnode, een script Kafka toocreate voorzien van een onderwerp:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

Met deze opdracht verbindt met behulp van Hallo hostinformatie opgeslagen in tooZookeeper `$KAFKAZKHOSTS`, en maak vervolgens met de naam Kafka-onderwerp **testen**. U kunt controleren dat onderwerp Hallo is gemaakt met behulp van de volgende onderwerpen voor script toolist Hallo:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

Hallo uitvoer van deze opdracht geeft een lijst van Kafka-onderwerpen die Hallo bevat **testen** onderwerp.

## <a name="produce-and-consume-records"></a>Records maken en gebruiken

Kafka slaat *records* op in onderwerpen. Records worden geproduceerd door *producenten* en worden gebruikt door *consumenten*. Producenten halen records op uit Kafka-*brokers*. Elk werkrolknooppunt in uw HDInsight-cluster is een Kafka-broker.

Gebruik Hallo stappen toostore records in Hallo test-onderwerp dat u eerder hebt gemaakt en leest u deze met een consumer te volgen:

1. Van Hallo SSH-sessie, gebruikt u een script met Kafka toowrite records toohello onderwerp:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    U geen resultaten op toohello vragen na deze opdracht. In plaats daarvan, typt u een paar tekstberichten en gebruik vervolgens **Ctrl + c drukken** toostop toohello onderwerp verzenden. Elke regel wordt als een afzonderlijke record verzonden.

2. Gebruik een script met Kafka tooread records uit Hallo onderwerp:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    Met deze opdracht haalt Hallo records van Hallo onderwerp en weergegeven. Met behulp van `--from-beginning` vertelt Hallo consumer toostart vanaf Hallo Hallo stream, zodat alle records worden opgehaald.

3. Gebruik __Ctrl + c drukken__ toostop Hallo consumer.

## <a name="producer-and-consumer-api"></a>Producent- en consument-API

U kunt ook programmatisch produceren en te gebruiken van records met behulp van Hallo [Kafka-API's](http://kafka.apache.org/documentation#api). toobuild een producent Java en de consument gebruik Hallo volgende stappen uit uw ontwikkelomgeving.

> [!IMPORTANT]
> Hiervoor hebt u Hallo componenten zijn geïnstalleerd in uw ontwikkelomgeving te volgen:
>
> * [Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) of een equivalent, zoals OpenJDK.
>
> * [Apache Maven](http://maven.apache.org/)
>
> * Een SSH-client en het Hallo `scp` opdracht. Zie voor meer informatie, Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

1. Voorbeelden van Hallo downloaden [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started). Hallo producent/consumer bijvoorbeeld Hallo-project in hello gebruiken `Producer-Consumer` directory. In dit voorbeeld bevat Hallo klassen te volgen:
   
    * **Voer** -Hallo consumer of producent wordt gestart.

    * **Producent** -stores 1.000.000 records toohello onderwerp.

    * **Consumer** -records van Hallo onderwerp leest.

2. een pakket jar toocreate mappen toohello locatie Hallo wijzigen `Producer-Consumer` directory en gebruik Hallo volgende opdracht:

    ```
    mvn clean package
    ```

    Met deze opdracht maakt u een directory met de naam `target`, die een bestand met de naam `kafka-producer-consumer-1.0-SNAPSHOT.jar` bevat.

3. Gebruik Hallo deze opdrachten toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` bestand tooyour HDInsight-cluster:
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    Vervang **SSHUSER** met Hallo SSH-gebruiker voor uw cluster, en vervang **CLUSTERNAME** met Hallo-naam van het cluster. Als u wordt gevraagd Hallo wachtwoord invoeren voor Hallo SSH-gebruiker.

4. Eenmaal Hallo `scp` opdracht kopiëren van het Hallo-bestand is voltooid, toohello-cluster via SSH verbinding. Gebruik Hallo opdracht toowrite records toohello Testonderwerp te volgen:

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. Zodra Hallo is voltooid, gebruikt u de volgende opdracht tooread uit Hallo onderwerp Hallo:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    Hallo-records lezen, samen met een telling van records, wordt weergegeven. Mogelijk ziet u enkele van meer dan 1.000.000 geregistreerd als u meerdere records toohello onderwerp met een script in een eerdere stap hebt verzonden.

6. Gebruik __Ctrl + c drukken__ tooexit Hallo consumer.

### <a name="multiple-consumers"></a>Meerdere consumenten

Kafka-consumenten gebruiken een consumentengroep bij het lezen van records. Met behulp van dezelfde groep Hallo met meerdere gebruikers, die balanced resulteert in een load leesbewerkingen van een onderwerp. Elke consumer in Hallo groep ontvangt een deel van het Hallo-records. toosee dit proces in actie, gebruik Hallo volgende stappen:

1. Open een nieuw SSH-sessie toohello cluster, zodat er twee van deze. Gebruik in elke sessie Hallo na toostart Hallo een consumer met dezelfde consumer groeps-ID:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    Deze opdracht start een consumer Hallo groeps-ID met `mygroup`.

    > [!NOTE]
    > Hallo-opdrachten gebruiken in Hallo [hello Zookeeper en Broker host informatie](#getkafkainfo) sectie tooset `$KAFKABROKERS` voor deze SSH-sessie.

2. Als elke sessie aantallen Hallo records die wordt ontvangen van Hallo onderwerp volgen. Hallo totaal van beide-sessies moet dezelfde worden Hallo als u eerder hebt ontvangen van een consumer.

Verbruik door clients binnen dezelfde groep wordt verwerkt door Hallo partities voor Hallo onderwerp Hallo. Voor Hallo `test` onderwerp eerder hebt gemaakt, heeft acht partities. Als u acht SSH-sessies openen en een gebruiker worden gestart in alle sessies, leest de elke consumer records uit één partitie voor Hallo onderwerp.

> [!IMPORTANT]
> Een consumentengroep kan niet meer consumentexemplaren dan partities bevatten. In dit voorbeeld kan een consumergroep up tooeight consumenten bevatten, omdat dat Hallo aantal partities in Hallo onderwerp. U kunt ook meerdere consumentengroepen hebben, waarvan elke groep niet meer dan acht consumenten bevat.

Records die zijn opgeslagen in Kafka worden opgeslagen in Hallo volgorde die binnen een partitie worden ontvangen. tooachieve-gerangschikt leveringsmethode voor records *binnen een partitie*, een consumergroep waarbij Hallo aantal exemplaren van de consument van overeenkomt met het aantal partities Hallo maken. tooachieve-gerangschikt leveringsmethode voor records *Hallo onderwerp*, een consumergroep te maken met een consumer slechts één exemplaar.

## <a name="streaming-api"></a>Streaming-API

Hallo streaming API is tooKafka toegevoegd in versie 0.10.0; eerdere versies zijn afhankelijk van Apache Spark of Storm voor de verwerking van de stroom.

1. Als u dit nog niet hebt gedaan, downloaden Hallo voorbeelden van [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour ontwikkelomgeving. Gebruik voor Hallo streaming-voorbeeld, Hallo-project in Hallo `streaming` directory.
   
    Dit project bevat slechts één klasse `Stream`, die records leest uit Hallo `test` onderwerp eerder hebt gemaakt. Het Hallo woorden lezen geteld en verzendt van elk woord en het aantal tooa onderwerp met de naam `wordcounts`. Hallo `wordcounts` onderwerp in een latere stap in deze sectie wordt gemaakt.

2. Vanaf de opdrachtregel Hallo in uw ontwikkelomgeving, wijzig mappen toohello locatie Hallo `Streaming` directory en gebruik Hallo opdracht toocreate een jar-pakket te volgen:

    ```bash
    mvn clean package
    ```

    Met deze opdracht maakt u een directory met de naam `target`, die een bestand met de naam `kafka-streaming-1.0-SNAPSHOT.jar` bevat.

3. Gebruik Hallo deze opdrachten toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` bestand tooyour HDInsight-cluster:
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    Vervang **SSHUSER** met Hallo SSH-gebruiker voor uw cluster, en vervang **CLUSTERNAME** met Hallo-naam van het cluster. Als u wordt gevraagd Hallo wachtwoord invoeren voor Hallo SSH-gebruiker.

4. Eenmaal Hallo `scp` opdracht kopiëren van het Hallo-bestand is voltooid, toohello-cluster via SSH verbinding maken met en gebruik vervolgens de volgende opdracht toocreate Hallo Hallo `wordcounts` onderwerp:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. Vervolgens start Hallo streaming-proces met behulp van de volgende opdracht Hallo:
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    Deze opdracht start Hallo proces op de achtergrond Hallo streaming.

6. Gebruik Hallo volgende opdracht toosend berichten toohello `test` onderwerp. Deze berichten worden verwerkt door Hallo streaming-voorbeeld:
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. Gebruik Hallo tooview Hallo uitvoer van de opdracht die is geschreven toohello na `wordcounts` onderwerp door Hallo streaming proces:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > tooview hello gegevens, moet u Hallo consumer tooprint Hallo sleutel en Hallo deserializer toouse voor Hallo-sleutel en waarde zien. Hallo sleutelnaam is Hallo word en Hallo sleutelwaarde bevat Hallo count.
   
    Hallo uitvoer is vergelijkbaar toohello de volgende tekst:
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > Hallo aantal oploopt telkens wanneer een woord wordt aangetroffen.

7. Gebruik Hallo __Ctrl + c drukken__ tooexit Hallo consumer en gebruik vervolgens Hallo `fg` opdracht toobring Hallo streaming achtergrond taak back toohello voorgrond. Gebruik __Ctrl + c drukken__ tooexit deze ook.

## <a name="delete-hello-cluster"></a>Hallo-cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Problemen oplossen

Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.

## <a name="next-steps"></a>Volgende stappen

In dit document, kunt u Hallo basisbeginselen van het werken met Apache Kafka op HDInsight hebt geleerd. Hallo toolearn meer informatie over het werken met Kafka volgende gebruiken:

* [Hoge beschikbaarheid van uw gegevens met Kafka in HDInsight](hdinsight-apache-kafka-high-availability.md)
* [De schaalbaarheid verhogen door beheerde schijven met Kafka in HDInsight te configureren](hdinsight-apache-kafka-scalability.md)
* [Documentatie voor Apache Kafka](http://kafka.apache.org/documentation.html) op kafka.apache.org.
* [MirrorMaker toocreate een replica van Kafka op HDInsight gebruiken](hdinsight-apache-kafka-mirroring.md)
* [Apache Storm gebruiken met Kafka in HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Apache Spark gebruiken met Kafka in HDInsight](hdinsight-apache-spark-with-kafka.md)
* [TooKafka verbinding via een virtueel Azure-netwerk](hdinsight-apache-kafka-connect-vpn-gateway.md)
