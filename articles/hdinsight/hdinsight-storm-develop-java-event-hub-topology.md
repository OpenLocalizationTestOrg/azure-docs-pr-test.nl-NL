---
title: aaaProcess gebeurtenissen van Event Hubs met Storm op HDInsight met behulp van Java | Microsoft Docs
description: Meer informatie over hoe tooprocess Event Hubs-gegevens met een Storm Java-topologie met Maven gemaakt.
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a>Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)

Meer informatie over hoe toouse Azure Event Hubs met Storm op HDInsight. In dit voorbeeld maakt gebruik van Java-onderdelen tooread en write-gegevens in Azure Event Hubs.

Azure Event Hubs kunt u tooprocess enorme hoeveelheden gegevens van websites, apps en apparaten. Hallo Event Hub spout maakt het eenvoudig toouse Apache Storm op HDInsight tooanalyze deze gegevens in realtime. U kunt ook gegevens tooEvent Hubs van Storm schrijven met behulp van Hallo Event Hubs Bolts.

## <a name="prerequisites"></a>Vereisten

* Een Apache Storm op HDInsight-cluster versie 3.6. Zie voor meer informatie [aan de slag met Storm op HDInsight-cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).

    > [!IMPORTANT]
    > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* Een [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* [Oracle Java Developer Kit (JDK) versie 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) of gelijkwaardig, zoals [OpenJDK](http://openjdk.java.net/).

* [Maven](https://maven.apache.org/download.cgi): Maven is een project build-systeem voor Java-projecten.

* Een teksteditor of geïntegreerde ontwikkelomgeving (IDE).

    > [!NOTE]
    > Uw editor of IDE mogelijk specifieke functionaliteit voor het werken met Maven die niet in dit document wordt besproken. Zie voor informatie over het Hallo-mogelijkheden van uw omgeving voor het bewerken, Hallo-documentatie voor Hallo product dat u gebruikt.

    * Een SSH-client. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

* Hallo `ssh` en `scp` opdrachten. Dit zijn de gebruikte toocopy bestanden toohello HDInsight-cluster. Op Windows, kunt u deze via Bash op Windows 10 krijgen.

## <a name="understanding-hello-example"></a>Understanding Hallo-voorbeeld

Hallo [hdinsight, java, storm, eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) voorbeeld bevat twee topologieën:

Hallo `resources/writer.yaml` topologie schrijft willekeurige gegevens tooan Azure Event Hub. Hallo-gegevens worden gegenereerd door Hallo `DeviceSpout` onderdeel, en is een willekeurige apparaat-ID en de waarde van apparaat. Het wordt dus bepaalde hardware die een tekenreeks-ID en een numerieke waarde verzendt simuleren.

Thee `resources/reader.yaml` topologie leest gegevens uit Event Hub (Hallo gegevens geschreven door EventHubWriter,) parseert Hallo JSON-gegevens en meldt zich dan Hallo `deviceId` en `deviceValue` gegevens.

Hallo-gegevens zijn opgemaakt als een JSON-document voordat deze wordt tooEvent Hub geschreven en door Hallo reader gelezen dit wordt geparseerd uit JSON en in tuples. Hallo JSON-indeling is als volgt:

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a>Project-configuratie

Hallo `POM.xml` bestand bevat configuratiegegevens voor dit Maven-project. Hallo interessante stukken zijn:

#### <a name="event-hub-components"></a>Event Hub-onderdelen

Hallo-component die leest en schrijft tooAzure Event Hubs bevindt zich in Hallo [HDInsight opslagplaats](https://github.com/hdinsight/mvn-rep). Hallo volgende secties in Hallo `POM.xml` bestand laden Hallo onderdelen uit deze opslagplaats

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a>Hallo EventHubs Storm Spout afhankelijkheid

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

Deze xml definieert een afhankelijkheid voor Hallo eventhubs, dit pakket bevat een spout om te lezen uit Event Hubs en een bolt voor het schrijven van tooit.

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

Deze xml configureert Hallo project toogenerate uitvoer voor Java 8, die wordt gebruikt door HDInsight 3.5 of hoger.

#### <a name="hello-maven-shade-plugin"></a>Hallo maven-schaduw-invoegtoepassing

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

Deze xml configureert Hallo oplossing toopackage Hallo uitvoer in een jar uber. Hallo jar bevat Hallo projectcode en vereiste afhankelijkheden. Dit wordt ook gebruikt voor:

* Wijzig de naam licentiebestanden voor Hallo afhankelijkheden.
* Uitsluiten van beveiliging/handtekeningen.
* Zorg ervoor dat meerdere implementaties van dezelfde Hallo interface worden samengevoegd tot één post.

Deze configuratie-instellingen voorkomen dat er fouten tijdens runtime.

#### <a name="topology-definitions"></a>Topologie definities

In dit voorbeeld wordt Hallo [lichtstroom](https://storm.apache.org/releases/1.1.0/flux.html) framework. Dit framework gebruikt YAML toodefine Hallo topologieën. Hallo belangrijkste voordeel is dat u niet harde coderen Hallo-topologie in Java-code. Omdat de definitie van Hallo YAML is, kunt u deze vóór het verzenden van Hallo-topologie, zonder toorecompile Alles wijzigen.

__Writer.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

__Reader.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a>Hallo-topologie vertellen over Event Hub

Tijdens runtime, Hallo `dev.properties` bestand gebruikte toopass Hallo Event Hub configuratie toohello topologie is. Hallo is volgende voorbeeld de Standaardinhoud Hallo van Hallo-bestand:

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a>Omgevingsvariabelen configureren

Hallo kunnen volgende omgevingsvariabelen worden ingesteld wanneer u Java en Hallo JDK op uw ontwikkelwerkstation installeert. Echter, moet u controleren of ze bestaan en dat ze de juiste waarden voor uw systeem Hallo bevatten.

* **JAVA_HOME** -toohello directory waar Hallo Java runtime environment (JRE) is geïnstalleerd moet verwijzen. Bijvoorbeeld in een Unix- of Linux-distributie, heeft een waarde gelijkaardig te`/usr/lib/jvm/java-7-oracle`. In Windows, zou er een waarde gelijkaardig te`c:\Program Files (x86)\Java\jre1.7`
* **PAD** -moet bevatten Hallo paden te volgen:

  * **JAVA_HOME** (of equivalente paden Hallo)
  * **JAVA_HOME\bin** (of equivalente paden Hallo)
  * Hallo-directory waar Maven is geïnstalleerd

## <a name="configure-event-hub"></a>Event Hub configureren

Event Hubs is Hallo gegevensbron voor dit voorbeeld. Volgende stappen toocreate een Event Hub hello gebruiken.

1. Van Hallo [klassieke Azure-Portal](https://manage.windowsazure.com), selecteer **nieuw** > **Service Bus** > **Event Hub**  >  **Aangepast maken**.

2. Op Hallo **toevoegen van nieuwe Event Hub** scherm, voert u een **naam Event Hub**. Selecteer Hallo **regio** toocreate Hallo-hub in, en vervolgens een naamruimte maken of een bestaande set selecteren. Tot slot op Hallo **pijl** toocontinue.

    ![wizardpagina 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > Selecteer dezelfde Hallo **locatie** als uw Storm op HDInsight-server tooreduce latentie en kosten.

3. Op Hallo **configureren Event Hub** scherm, voert u Hallo **aantal partitie** en **bericht bewaren** waarden. Gebruik voor dit voorbeeld wordt een aantal partities van 10 en de retentie van een bericht van 1. Houd er rekening mee Hallo partitie aantal omdat u deze waarde later nodig.

    ![wizardpagina 2 van de](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. Nadat u Hallo event hub hebt gemaakt, selecteer Hallo naamruimte, selecteer **Event Hubs**, en selecteer vervolgens Hallo event hub die u eerder hebt gemaakt.
5. Selecteer **configureren**, maakt u twee nieuwe beleidsregels voor toegang met behulp van Hallo volgende informatie:

    <table>
    <tr><th>Naam</th><th>Machtigingen</th></tr>
    <tr><td>schrijver</td><td>Verzenden</td></tr>
    <tr><td>Lezer</td><td>Luisteren</td></tr>
    </table>

    Nadat u Hallo machtigingen hebt gemaakt, selecteert u Hallo **opslaan** pictogram Hallo Hallo pagina onderaan in. Deze beleidsregels voor gedeelde toegang zijn gebruikte tooread en tooEvent Hub schrijven.

    ![beleid](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. Nadat u Hallo beleid opslaat, gebruikt u Hallo **codegenerator voor gedeelde toegang** onderin Hallo van Hallo pagina tooretrieve Hallo sleutel voor Hallo **writer** en **lezer** beleid. Sla deze sleutels.

## <a name="download-and-build-hello-project"></a>Download en bouw Hallo-project

1. Hallo-project hebt gedownload van GitHub: [hdinsight, java, storm, eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub). U kunt het downloadpakket Hallo als een zip-archief of gebruik [git](https://git-scm.com/) tooclone Hallo-project lokaal.

2. Hallo wijzigen `dev.properties` bestand met de Hallo-configuratie voor uw Event Hub.

3. Gebruik Hallo toobuild en pakket Hallo-project te volgen:

        mvn package

    Met deze opdracht vereiste afhankelijkheden, builds gedownload en vervolgens de pakketten project Hallo. Hallo-uitvoer wordt opgeslagen in Hallo **/target** map als **EventHubExample-1.0-SNAPSHOT.jar**.

## <a name="test-locally"></a>Lokaal testen

Aangezien deze topologieën alleen lezen en tooEvent Hubs schrijven, kunt u deze testen lokaal hebt u een [Storm-ontwikkelomgeving](http://storm.apache.org/releases/current/Setting-up-development-environment.html). Gebruik Hallo toorun lokaal in Hallo dev omgeving stappen te volgen:

1. Hallo writer uitvoeren:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. Hallo lezer uitvoeren:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * `--local`: Voer Hallo-topologie in de lokale modus (niet-gedistribueerd).
> * `-R /writer.yaml`: Definitie van de topologie Hallo laden uit Hallo `resources` verpakt in Hallo jar. Als een bestand op het lokale bestandssysteem Hallo Hallo topologie is Hallo pad tooit opgeven als de laatste parameter Hallo.
> * `--filter dev.properties`: Gebruik Hallo inhoud van `dev.properties` toofill Hallo-waarden in Hallo topologie definities. Bijvoorbeeld `${eventhub.read.policy.name}`.

Uitvoer is vastgelegd toohello console bij lokale uitvoering. Gebruik __Ctrl + C__ toostop Hallo topologie.

## <a name="deploy-hello-topologies"></a>Hallo-topologieën implementeren

1. SCP toocopy Hallo jar pakket tooyour HDInsight-cluster gebruiken. GEBRUIKERSNAAM vervangen door Hallo SSH-gebruiker voor uw cluster. Vervang CLUSTERNAME door Hallo-naam van uw HDInsight-cluster:

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    Als u een wachtwoord voor uw SSH-account gebruikt, zijn na vragen aan gebruiker tooenter Hallo wachtwoord. Als u een SSH-sleutel met Hallo account gebruikt, moet u mogelijk toouse hello `-i` parameter toospecify Hallo pad toohello sleutelbestand. Bijvoorbeeld: `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`

    Deze opdracht kopieert Hallo bestand toohello basismap van uw SSH-gebruiker op Hallo-cluster.

2. Zodra het Hallo-bestand is klaar met uploaden, gebruikt u SSH tooconnect toohello HDInsight-cluster. Vervang **gebruikersnaam** Hallo-naam van uw SSH-aanmelding. Vervang **CLUSTERNAME** met de naam van uw HDInsight-cluster:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > Als u een wachtwoord voor uw SSH-account gebruikt, zijn na vragen aan gebruiker tooenter Hallo wachtwoord. Als u een SSH-sleutel met Hallo account gebruikt, moet u mogelijk toouse hello `-i` parameter toospecify Hallo pad toohello sleutelbestand. Hallo volgende voorbeeld wordt geladen Hallo persoonlijke sleutel uit `~/.ssh/id_rsa`:
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. Gebruik Hallo opdracht toostart Hallo topologieën te volgen:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * `--remote`: Hallo topologie toohello Nimbus-service op Hallo worker-knooppunten in cluster Hallo gestart verzendt.

4. gegevens van tooview Hallo geregistreerd, gaat u toohttps://CLUSTERNAME.azurehdinsight.net/stormui, waar __CLUSTERNAME__ Hallo-naam van uw HDInsight-cluster. Selecteer Hallo topologieën en inzoomen toohello onderdelen. Selecteer Hallo __poort__ vermelding voor een exemplaar van een onderdeel tooview informatie in het logboek geregistreerd.

5. Gebruik Hallo opdrachten toostop Hallo topologieën te volgen:

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a>Uw cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Volgende stappen

* [Voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md)
