---
title: onderwerpen over aaaMirror Apache Kafka - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe een replica van een Kafka op HDInsight-cluster toomaintain door mirroring van onderwerpen tooa secundaire cluster toouse Apache Kafka spiegelen functie.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a>Gebruik MirrorMaker tooreplicate Apache Kafka onderwerpen met Kafka op HDInsight (preview)

Meer informatie over hoe toouse Apache Kafka het spiegelen van de functie tooreplicate onderwerpen tooa secundaire cluster. Het spiegelen kan worden uitgevoerd als een continu proces of af en toe worden gebruikt als een methode voor het migreren van gegevens uit een cluster tooanother.

In dit voorbeeld is het spiegelen gebruikte tooreplicate onderwerpen tussen twee clusters met HDInsight. Beide clusters zijn in een Azure-netwerk in Hallo dezelfde regio.

> [!WARNING]
> Spiegeling moet niet worden beschouwd als een manier tooachieve fouttolerantie. Hallo offset tooitems binnen een onderwerp zijn de verschillen tussen clusters van Hallo bron- en doelserver, zodat clients kunnen niet door elkaar Hallo twee gebruiken.
>
> Als u zich zorgen over fouttolerantie, stelt u replicatie voor Hallo onderwerpen binnen het cluster. Zie voor meer informatie [aan de slag met Kafka op HDInsight](hdinsight-apache-kafka-get-started.md).

## <a name="how-kafka-mirroring-works"></a>De werking van Kafka spiegelen

Mirroring werkt met behulp van Hallo MirrorMaker hulpprogramma (onderdeel van Apache Kafka) tooconsume records van de onderwerpen in de broncluster hello en maak vervolgens een lokale kopie op Hallo doelcluster. MirrorMaker maakt gebruik van een (of meer) *consumenten* die gelezen van Hallo broncluster, en een *producent* die schrijft toohello lokale (doel) cluster.

Hallo volgende diagram illustreert Hallo spiegelen proces:

![Diagram van Hallo proces spiegelen](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

Apache Kafka op HDInsight biedt geen toegang tot toohello Kafka service ten opzichte van Hallo openbare internet. Moeten in Hallo Kafka producenten en consumenten hetzelfde virtuele Azure-netwerk als Hallo knooppunten in Hallo Kafka-cluster. Bijvoorbeeld, bevinden zowel Hallo Kafka bron en bestemming clusters zich in een Azure-netwerk. Hallo volgende diagram ziet u hoe de communicatie tussen clusters met Hallo loopt:

![Diagram van de bron en bestemming Kafka-clusters in een Azure-netwerk](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

de bron- en doelserver clusters Hallo kunnen afwijken van Hallo aantal knooppunten en partities en offsets binnen Hallo onderwerpen zijn ook verschillend. Hallo-sleutelwaarde die wordt gebruikt voor het partitioneren, mirroring worden bijgehouden, zodat de volgorde van de records op basis van de per-sleutel wordt behouden.

### <a name="mirroring-across-network-boundaries"></a>Spiegelen buiten de netwerkgrenzen van

Als u toomirror tussen clusters met Kafka in verschillende netwerken moet, zijn er aanvullende overwegingen na Hallo:

* **Gateways**: Hallo-netwerken kunnen toocommunicate op Hallo TCPIP niveau zijn.

* **Naamomzetting**: Hallo Kafka-clusters in elk netwerk moet kunnen tooconnect tooeach andere met behulp van hostnamen. Hiervoor moet mogelijk een Domain Name System (DNS)-server in elk netwerk dat is geconfigureerd tooforward aanvragen toohello andere netwerken.

    Bij het maken van een virtueel netwerk van Azure, in plaats van automatische DNS opgegeven Hallo met Hallo netwerk, moet u een aangepaste DNS-server en Hallo IP-adres voor Hallo-server. Na Hallo die virtueel netwerk is gemaakt, moet u vervolgens maken een Azure-virtuele Machine die wordt gebruikt dat IP-adres, en vervolgens installeren en configureren van DNS-software op deze.

    > [!WARNING]
    > Maak en configureer Hallo aangepaste DNS-server voordat u HDInsight installeert in Hallo virtueel netwerk. Er is geen aanvullende configuratie vereist voor HDInsight toouse Hallo DNS-server is geconfigureerd voor Hallo virtueel netwerk.

Zie voor meer informatie over het verbinden van twee virtuele netwerken van Azure [een VNet-naar-VNet-verbinding configureren](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

## <a name="create-kafka-clusters"></a>Kafka-clusters maken

U kunt een virtuele Azure-netwerk maken en handmatig Kafka-clusters, zijn maar er eenvoudiger toouse een Azure Resource Manager-sjabloon. Gebruik Hallo volgende stap toodeploy een Azure-netwerk en twee Kafka clusters tooyour Azure-abonnement.

1. Hallo na de knop toosign in tooAzure en open Hallo-sjabloon in hello Azure-portal gebruiken.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello Azure Resource Manager-sjabloon bevindt zich op **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > de beschikbaarheid van de tooguarantee van Kafka op HDInsight, uw cluster moet ten minste drie worker-knooppunten bevatten. Deze sjabloon maakt een Kafka-cluster dat drie worker-knooppunten bevat.

2. Gebruik Hallo informatie toopopulate Hallo vermeldingen op Hallo volgen **aangepaste implementatie** blade:
    
    ![Aangepaste HDInsight-implementatie](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * **Resourcegroep**: Maak een groep of een bestaande set selecteren. Deze groep bevat Hallo HDInsight-cluster.

    * **Locatie**: Selecteer een locatie geografisch sluiten tooyou.
     
    * **Clusternaam baseren**: deze waarde wordt gebruikt als basisnaam van Hallo voor Hallo Kafka-clusters. Bijvoorbeeld, voeren **hdi** wordt gemaakt met de naam clusters **bron hdi** en **dest hdi**.

    * **Aanmeldingsnaam van gebruiker cluster**: Hallo beheerder gebruikersnaam op voor het Hallo-bron- en doelserver Kafka-clusters.

    * **Aanmeldingswachtwoord cluster**: Hallo beheerderswachtwoord voor het Hallo-bron- en doelserver Kafka-clusters.

    * **SSH-gebruikersnaam**: Hallo SSH gebruiker toocreate voor Hallo bron- en doelserver Kafka-clusters.

    * **SSH-wachtwoord**: Hallo-wachtwoord voor Hallo SSH-gebruiker voor het Hallo-bron- en doelserver Kafka-clusters.

3. Lees Hallo **voorwaarden en bepalingen**, en selecteer vervolgens **ik ga akkoord toohello voorwaarden bovengenoemde**.

4. Controleer ten slotte **pincode toodashboard** en selecteer vervolgens **aankoop**. Het duurt ongeveer 20 minuten toocreate Hallo-clusters.

Zodra het Hallo-resources zijn gemaakt, bent u omgeleide tooa blade voor de resourcegroep Hallo Hallo clusters en webdashboard met.

![Resourcegroepblade voor Hallo vnet en clusters](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> Merk op dat de namen van HDInsight-clusters Hallo Hallo zijn **bron BASENAME** en **dest BASENAME**, waarbij BASENAME Hallo-naam die u hebt opgegeven toohello sjabloon. U deze namen in latere stappen gebruiken om verbinding te maken van clusters toohello.

## <a name="create-topics"></a>Help-onderwerpen maken

1. Verbinding maken met toohello **bron** cluster via SSH:

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    Vervang **sshuser** met Hallo SSH-gebruikersnaam gebruikt bij het Hallo-cluster maken. Vervang **BASENAME** met Hallo basisnaam gebruikt bij het Hallo-cluster maken.

    Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

2. Gebruik Hallo volgende toofind hello Zookeeper hosts voor broncluster Hallo-opdrachten:

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. Gebruik Hallo opdracht tooverify die Hallo onderwerp te volgen is gemaakt:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    Hallo-antwoord bevat `testtopic`.

4. Gebruik Hallo tooview hello Zookeeper informatie over de host voor deze volgen (Hallo **bron**) cluster:

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    Hiermee wordt informatie vergelijkbare toohello volgende tekst:

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    Deze gegevens worden opgeslagen. Het wordt gebruikt in de volgende sectie Hallo.

## <a name="configure-mirroring"></a>Configureer het spiegelen

1. Verbinding maken met toohello **bestemming** cluster met behulp van een andere SSH-sessie:

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    Vervang **sshuser** met Hallo SSH-gebruikersnaam gebruikt bij het Hallo-cluster maken. Vervang **BASENAME** met Hallo basisnaam gebruikt bij het Hallo-cluster maken.

    Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

2. Gebruik Hallo volgende opdracht toocreate een `consumer.properties` -bestand dat wordt beschreven hoe toocommunicate Hello **bron** cluster:

    ```bash
    nano consumer.properties
    ```

    Gebruik Hallo na de tekst hello inhoud Hallo `consumer.properties` bestand:

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    Vervang **SOURCE_ZKHOSTS** Hello Zookeeper fungeert als host voor gegevens van Hallo **bron** cluster.

    Dit bestand wordt Hallo consumer informatie toouse beschreven bij het lezen van Hallo bron Kafka-cluster. Zie voor meer informatie consumer-configuratie [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) op kafka.apache.org.

    Gebruik-bestand Hallo toosave **Ctrl + X**, **Y**, en vervolgens **Enter**.

3. Voordat u configureert Hallo producent die communiceert met het doelcluster hello, u moet Hallo broker hosts vinden voor Hallo **bestemming** cluster. Hallo opdrachten tooretrieve na deze informatie gebruiken:

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    Vervang `$PASSWORD` met Hallo aanmeldingswachtwoord account (admin) voor Hallo-cluster.

    Vervang `$CLUSTERNAME` met de naam van het doelcluster Hallo Hallo.

    Deze opdrachten retourneren informatie vergelijkbare toohello volgende:

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. Gebruik Hallo toocreate na een `producer.properties` -bestand dat wordt beschreven hoe toocommunicate Hello **bestemming** cluster:

    ```bash
    nano producer.properties
    ```

    Gebruik Hallo na de tekst hello inhoud Hallo `producer.properties` bestand:

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    Vervang **DEST_BROKERS** met Hallo broker informatie uit de vorige stap Hallo.

    Zie voor meer informatie producent configuratie, [producent Configs](https://kafka.apache.org/documentation#producerconfigs) op kafka.apache.org.

## <a name="start-mirrormaker"></a>MirrorMaker starten

1. Van Hallo SSH-verbinding toohello **bestemming** cluster, Hallo opdracht toostart hello MirrorMaker proces volgende gebruiken:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    in dit voorbeeld gebruikt Hallo-parameters zijn:

    * **--consumer.config**: Hiermee geeft u Hallo-bestand dat de consument eigenschappen bevat. Deze eigenschappen zijn gebruikte toocreate een consumer die uit Hallo leest *bron* Kafka-cluster.

    * **--producer.config**: Hiermee geeft u Hallo-bestand dat de producent eigenschappen bevat. Deze eigenschappen zijn gebruikte toocreate een producent die toohello schrijft *bestemming* Kafka-cluster.

    * **--geaccepteerde**: een lijst met onderwerpen die MirrorMaker van Hallo bron cluster toohello doel repliceert.

    * **--num.streams**: aantal consumer threads toocreate Hallo.

 Bij het opstarten retourneert MirrorMaker informatie vergelijkbare toohello volgende tekst:

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. Van Hallo SSH-verbinding toohello **bron** cluster, gebruikt u Hallo opdracht toostart producent te volgen en verzenden van berichten toohello onderwerp:

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    Vervang `$PASSWORD` met hello (admin) aanmeldingswachtwoord voor Hallo broncluster.

    Vervang `$CLUSTERNAME` met de naam van het broncluster Hallo Hallo.

     Wanneer u bij een lege regel met een cursor aankomt, typt u in een paar tekstberichten. Dit onderwerp toohello worden verzonden op Hallo **bron** cluster. Wanneer u klaar bent, gebruikt u **Ctrl + c drukken** tooend Hallo producent proces.

3. Van Hallo SSH-verbinding toohello **bestemming** cluster, gebruikt u **Ctrl + c drukken** tooend hello MirrorMaker proces. Vervolgens gebruik Hallo deze tooverify die Hallo opdrachten `testtopic` onderwerp is gemaakt en die gegevens in Hallo onderwerp gerepliceerde toothis mirror is:

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    Vervang `$PASSWORD` met hello (admin) aanmeldingswachtwoord voor Hallo doelcluster.

    Vervang `$CLUSTERNAME` met de naam van het doelcluster Hallo Hallo.

    Hallo lijst met onderwerpen bevat nu `testtopic`, die wordt gemaakt wanneer MirrorMaster Hallo onderwerp uit Hallo bron cluster toohello doel weerspiegelt. Hallo-berichten die zijn opgehaald uit het Hallo-onderwerp zijn hetzelfde als ingevoerd in de broncluster Hallo Hallo.

## <a name="delete-hello-cluster"></a>Hallo-cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Aangezien Hallo stappen in dit document beide maken clusters in dezelfde Azure-resourcegroep hello, kunt u de resourcegroep Hallo in hello Azure-portal verwijderen. Verwijderen van het Hallo-resourcegroep Hiermee verwijdert u alle resources die zijn gemaakt op basis van dit document, hello Azure Virtual Network en storage-account door Hallo clusters worden gebruikt.

## <a name="next-steps"></a>Volgende stappen

In dit document hebt u geleerd hoe toouse MirrorMaker toocreate een replica van een Kafka-cluster. Hallo toodiscover koppelingen volgen andere manieren toowork met Kafka gebruiken:

* [Apache Kafka MirrorMaker documentatie](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) op cwiki.apache.org.
* [Aan de slag met Apache Kafka in HDInsight](hdinsight-apache-kafka-get-started.md)
* [Apache Spark gebruiken met Kafka in HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Apache Storm gebruiken met Kafka in HDInsight](hdinsight-apache-storm-with-kafka.md)
* [TooKafka verbinding via een virtueel Azure-netwerk](hdinsight-apache-kafka-connect-vpn-gateway.md)
