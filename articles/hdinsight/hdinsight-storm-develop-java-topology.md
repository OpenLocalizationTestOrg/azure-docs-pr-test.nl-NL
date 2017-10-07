---
title: aaaApache Storm-voorbeeld Java-topologie - Azure HDInsight | Microsoft Docs
description: "Meer informatie over hoe toocreate Apache Storm-topologieën in Java door het maken van een voorbeeldwoord topologie tellen."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: Apache storm, apache storm bijvoorbeeld storm java, storm-topologie-voorbeeld
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a>Maken van een Apache Storm-topologie in Java

Meer informatie over hoe toocreate een op Java gebaseerde topologie voor Apache Storm. U maakt een Storm-topologie die een word-count-toepassing implementeert. U Maven toobuild en pakket Hallo-project. Vervolgens leert u hoe toodefine Hallo topologie gebruik Hallo lichtstroom framework.

> [!NOTE]
> Hallo lichtstroom framework is beschikbaar in Storm 0.10.0 of hoger. Storm 0.10.0 is beschikbaar met HDInsight 3.3 en 3.4.

U kunt na het voltooien van de stappen in dit document Hallo Hallo topologie tooApache Storm op HDInsight implementeren.

> [!NOTE]
> Er is een voltooide versie van Hallo Storm-topologie voorbeelden gemaakt in dit document beschikbaar op [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).

## <a name="prerequisites"></a>Vereisten

* [Java Developer Kit (JDK) versie 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* [Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is een project build-systeem voor Java-projecten.

* Een teksteditor of IDE.

## <a name="configure-environment-variables"></a>Omgevingsvariabelen configureren

Hallo kunnen volgende omgevingsvariabelen worden ingesteld wanneer u Java en Hallo JDK installeert. Echter, moet u controleren of ze bestaan en dat ze de juiste waarden voor uw systeem Hallo bevatten.

* **JAVA_HOME** -toohello directory waar Hallo Java runtime environment (JRE) is geïnstalleerd moet verwijzen. Bijvoorbeeld in een Unix- of Linux-distributie, heeft een waarde gelijkaardig te`/usr/lib/jvm/java-7-oracle`. In Windows, zou er een waarde gelijkaardig te`c:\Program Files (x86)\Java\jre1.7`

* **PAD** -moet bevatten Hallo paden te volgen:

  * **JAVA_HOME** (of equivalente paden Hallo)

  * **JAVA_HOME\bin** (of equivalente paden Hallo)

  * Hallo-directory waar Maven is geïnstalleerd

## <a name="create-a-maven-project"></a>Een Maven-project maken

Vanaf de opdrachtregel Hallo gebruik Hallo volgende opdracht toocreate een Maven-project met de naam **WordCount**:

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> Als u met behulp van PowerShell, moet u tussen de`-D` parameters met dubbele aanhalingstekens.
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

Deze opdracht maakt u een map met de naam `WordCount` op Hallo huidige locatie, die een basic Maven-project bevat. Hallo `WordCount` map bevat Hallo volgende items:

* `pom.xml`: Bevat instellingen voor Hallo Maven-project.
* `src\main\java\com\microsoft\example`: Bevat de toepassingscode van uw.
* `src\test\java\com\microsoft\example`: Bevat de tests voor uw toepassing. 

### <a name="remove-hello-generated-example-code"></a>Voorbeeldcode Hallo gegenereerd verwijderen

Hallo gegenereerd test en toepassingsbestanden Hallo verwijderen:

* **src\test\java\com\microsoft\example\AppTest.Java**
* **src\main\java\com\microsoft\example\App.Java**

## <a name="add-maven-repositories"></a>Maven-opslagplaatsen toevoegen

HDInsight is gebaseerd op Hallo Hortonworks Data Platform HDP (), zodat u wordt aangeraden Hallo Hortonworks opslagplaats toodownload afhankelijkheden voor uw Apache Storm-projecten. In Hallo __pom.xml__ bestand, het toevoegen van XML te volgen nadat Hallo Hallo `<url>http://maven.apache.org</url>` regel:

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a>Eigenschappen toevoegen

Maven kunt u toodefine projectniveau waarden ' Eigenschappen ' genoemd. In Hallo __pom.xml__, toevoegen na tekst na Hallo Hallo `</repositories>` regel:

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

U kunt deze waarde nu gebruiken in andere gedeelten van Hallo `pom.xml`. Bijvoorbeeld, wanneer u opgeeft Hallo-versie van Storm-onderdelen, kunt u `${storm.version}` in plaats van een vaste waarde coderen.

## <a name="add-dependencies"></a>Afhankelijkheden toevoegen

Een afhankelijkheid voor Storm-onderdelen toevoegen. Open Hallo `pom.xml` bestands- en toevoegen van de volgende code in Hallo Hallo `<dependencies>` sectie:

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

Tijdens het compileren Maven maakt gebruik van deze informatie toolook up `storm-core` in Hallo Maven-opslagplaats. Eerst wordt gezocht in de opslagplaats Hallo op uw lokale computer. Als er niet zijn Hallo-bestanden, wordt Maven downloadt deze vanuit openbare opslagplaats met Maven Hallo en opgeslagen in de lokale Hallo-opslagplaats.

> [!NOTE]
> Kennisgeving Hallo `<scope>provided</scope>` regel in deze sectie. Deze instelling geeft Maven tooexclude **storm-core** van JAR-bestanden die zijn gemaakt, omdat dit wordt geleverd door Hallo-systeem.

## <a name="build-configuration"></a>Configuratie maken

Maven-invoegtoepassingen toestaan toocustomize Hallo build fasen van Hallo-project. Bijvoorbeeld, hoe Hallo project is gecompileerd of hoe toopackage in een JAR-bestand. Open Hallo `pom.xml` bestands- en toevoegen van de volgende code direct boven Hallo Hallo `</project>` regel.

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

Deze sectie is gebruikte tooadd invoegtoepassingen, bronnen en andere configuratieopties build. Voor een volledige beschrijving van Hallo **pom.xml** bestand, Zie [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).

### <a name="add-plug-ins"></a>Invoegtoepassingen toevoegen

Hallo voor Apache Storm-topologieën die zijn geïmplementeerd in Java [Exec Maven-invoegtoepassing](http://www.mojohaus.org/exec-maven-plugin/) is nuttig omdat hiermee tooeasily Hallo topologie lokaal uitvoeren in uw ontwikkelomgeving. Hallo na toohello toevoegen `<plugins>` sectie Hallo `pom.xml` bestand tooinclude Hallo Exec Maven-invoegtoepassing:

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

Andere nuttige invoegtoepassing is Hallo [Apache Maven-Compiler-invoegtoepassing](http://maven.apache.org/plugins/maven-compiler-plugin/), die is gebruikt toochange compilatie-opties. Hallo wijzigingen Hallo Java-versie die Maven voor het Hallo-bron en doel voor uw toepassing gebruikt.

* Voor HDInsight __3,4 of eerder__, Hallo bron instellen en Java-versie too__1.7__ als doel.

* Voor HDInsight __3.5__, Hallo bron instellen en Java-versie too__1.8__ als doel.

Toevoegen van de volgende tekst in Hallo Hallo `<plugins>` sectie Hallo `pom.xml` bestand tooinclude Hallo Apache Maven Compiler-invoegtoepassing. In dit voorbeeld bevat 1.8, zodat Hallo doel HDInsight versie 3.5 is.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a>Resources configureren

Hallo resources sectie kunt u tooinclude met niet-gecodeerde resources zoals configuratiebestanden die nodig is voor de onderdelen in Hallo-topologie. In dit voorbeeld toevoegen na de tekst in Hallo Hallo `<resources>` sectie Hallo ' bestand pom.xml.

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

In dit voorbeeld wordt Hallo resources directory in de hoofdmap Hallo van Hallo-project (`${basedir}`) als een locatie die resources bevat en omvat het Hallo-bestand met de naam `log4j2.xml`. Dit bestand is gebruikte tooconfigure welke gegevens worden geregistreerd door Hallo-topologie.

## <a name="create-hello-topology"></a>Hallo-topologie maken

Een Java gebaseerde Apache Storm-topologie bestaat uit drie onderdelen die u moet schrijven (of een verwijzing) als een afhankelijkheid.

* **Spouts**: leest gegevens uit externe gegevensbronnen en verzendt gegevensstromen in Hallo-topologie.

* **Bolts**: voert verwerkingstaken op streams verzonden door spouts of andere bolts en verzendt een of meer stromen.

* **Topologie**: Hiermee bepaalt u hoe Hallo spouts en bolts gerangschikte en biedt een invoerpunt voor Hallo voor Hallo-topologie.

### <a name="create-hello-spout"></a>Hallo spout maken

vereisten voor het instellen van externe gegevensbronnen, tooreduce Hallo na spout verzendt gewoon willekeurig zinnen. Het is een gewijzigde versie van een spout die wordt geleverd met Hallo [Storm Starter-voorbeelden](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).

> [!NOTE]
> Zie voor een voorbeeld van een spout die uit een externe gegevensbron kan lezen, een Hallo volgen voorbeelden:
>
> * [TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): een voorbeeld spout die uit Twitter lezen
> * [Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): een spout die uit Kafka lezen

Maak een bestand met de naam voor Hallo-spout `RandomSentenceSpout.java` in Hallo `src\main\java\com\microsoft\example` directory en gebruik Hallo Java-code als Hallo inhoud na:

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> Hoewel deze topologie wordt slechts één spout gebruikt, kunnen andere gebruikers verschillende die gegevens uit verschillende bronnen naar de topologie Hallo hebben.

### <a name="create-hello-bolts"></a>Hallo bolts maken

Bolts verwerken Hallo gegevensverwerking. Deze topologie maakt gebruik van twee bolts:

* **SplitSentence**: splitst Hallo zinnen gegenereerd door **RandomSentenceSpout** in afzonderlijke woorden.

* **WordCount**: telt het aantal keren dat elk woord is opgetreden.

> [!NOTE]
> Bolts kunnen doen alles zijn, bijvoorbeeld berekening, persistentie of tooexternal onderdelen communiceren.

Twee nieuwe bestanden maken `SplitSentence.java` en `WordCount.java` in Hallo `src\main\java\com\microsoft\example` directory. Gebruik Hallo tekst hello inhoud voor Hallo-bestanden te volgen:

#### <a name="splitsentence"></a>SplitSentence

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a>WordCount

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a>Hallo-topologie definiëren

Hallo-topologie bindt Hallo spouts en bolts samen in een grafiek, waarmee wordt gedefinieerd hoe gegevens stromen tussen Hallo-onderdelen. Het bevat ook parallelle uitvoering hints die gebruikmaakt van Storm bij het maken van exemplaren van Hallo onderdelen binnen Hallo-cluster.

Hallo is volgende afbeelding een eenvoudige diagram van de grafiek Hallo van onderdelen voor deze topologie.

![diagram waarin Hallo spouts en bolts regeling](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

tooimplement Hallo topologie, maakt u een bestand met de naam `WordCountTopology.java` in Hallo `src\main\java\com\microsoft\example` directory. Gebruik Hallo Java-code als Hallo inhoud van Hallo-bestand te volgen:

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a>Logboekregistratie configureren

Storm Apache-Log4j toolog gegevens gebruikt. Als u logboekregistratie niet configureert, verzendt Hallo topologie diagnostische gegevens. toocontrol wat wordt geregistreerd, maak een bestand met de naam `log4j2.xml` in Hallo `resources` directory. Gebruik hello XML als Hallo inhoud van Hallo-bestand te volgen.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

Deze XML configureert u een nieuwe berichtenlogboek voor Hallo `com.microsoft.example` klasse, waaronder het Hallo-onderdelen in dit voorbeeldtopologie. Hallo-niveau is tootrace ingesteld voor dit logboek bevat informatie die door onderdelen in deze topologie logboekregistratie.

Hallo `<Root level="error">` sectie configureert u Hallo hoogste niveau van logboekregistratie (alles wat u niet in `com.microsoft.example`) tooonly logboek foutgegevens.

Zie voor meer informatie over het configureren van logboekregistratie voor Log4j [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).

> [!NOTE]
> Storm-versie 0.10.0 en hoger gebruiken Log4j 2.x. Oudere versies van storm gebruikt Log4j 1.x, die een andere indeling voor logboekbestanden-configuratie gebruikt. Zie voor informatie over oudere configuratie hello, [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).

## <a name="test-hello-topology-locally"></a>Lokaal testen Hallo-topologie

Nadat u Hallo bestanden opslaat, gebruikt u Hallo opdracht tootest Hallo topologie lokaal te volgen.

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

Als dit wordt uitgevoerd, geeft Hallo topologie starten van de informatie. Hallo is volgende tekst een voorbeeld van Hallo word aantal uitvoer:

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

Dit voorbeeld logboek geeft aan dat woord Hallo ' en ' heeft 113 keer is verzonden. Hallo blijft toogo up, zolang het Hallo-topologie wordt uitgevoerd, omdat Hallo spout continu Hallo verzendt dezelfde zinnen.

Er is een interval van 5 seconden tussen uitstoot van woorden en aantallen. Hallo **WordCount** -onderdeel is geconfigureerd tooonly informatie verzenden wanneer een tick tuple binnenkomt. Deze aanvragen die tick tuples worden alleen gedownload voor elke vijf seconden.

## <a name="convert-hello-topology-tooflux"></a>Hallo-topologie tooFlux converteren

Lichtstroom is een nieuw framework beschikbaar met Storm 0.10.0 en hoger, zodat u tooseparate configuratie van de toepassing. Onderdelen van uw nog steeds in Java zijn gedefinieerd, maar Hallo-topologie wordt gedefinieerd met een YAML-bestand. U kunt de definitie van een standaard-topologie van het pakket met uw project, of een zelfstandig bestand gebruiken bij het indienen van Hallo-topologie. Bij het indienen van Hallo topologie tooStorm, kunt u omgevingsvariabelen of configuratiewaarden bestanden toopopulate in Hallo YAML-topologie-definitie.

Hallo YAML-bestand definieert Hallo onderdelen toouse voor Hallo topologie en Hallo gegevensstroom ertussen. U kunt een bestand YAML opnemen als onderdeel van de jar-bestand Hallo of kunt u een extern YAML-bestand.

Zie voor meer informatie over lichtstroom [lichtstroom framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

> [!WARNING]
> Vervaldatum tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) met Storm 1.0.1, moet u mogelijk tooinstall een [Storm-ontwikkelomgeving](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun lichtstroom topologieën lokaal.

1. Hallo verplaatsen `WordCountTopology.java` bestand buiten het Hallo-project. Voorheen dit bestand Hallo topologie gedefinieerd, maar met lichtstroom is niet nodig.

2. In Hallo `resources` directory, maakt u een bestand met de naam `topology.yaml`. Gebruik hello tekst als Hallo inhoud van dit bestand te volgen.

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. Zorg Hallo na wijzigingen toohello `pom.xml` bestand.
   
   * Toevoegen van de volgende nieuwe afhankelijkheid in Hallo Hallo `<dependencies>` sectie:
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * Hallo invoegtoepassing toohello na toevoegen `<plugins>` sectie. Deze invoegtoepassing Hallo maken van een pakket (jar-bestand) verwerkt voor Hallo-project en enkele specifieke tooFlux van transformaties is van toepassing bij het maken van Hallo-pakket.
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
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

   * In Hallo **exec-maven-invoegtoepassing** `<configuration>` sectie, wijzig de waarde Hallo voor `<mainClass>` te`org.apache.storm.flux.Flux`. Deze instelling kan lichtstroom toohandle Hallo topologie lokaal wordt uitgevoerd in ontwikkeling.

   * In Hallo `<resources>` sectie, het toevoegen van Hallo toohello na `<includes>`. Deze XML bevat Hallo YAML-bestand dat Hallo topologie als onderdeel van het Hallo-project definieert.

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a>Hallo lichtstroom topologie lokaal testen

1. Hallo toocompile na gebruik en Hallo lichtstroom topologie met behulp van Maven uitvoeren:

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    Als u met behulp van PowerShell, gebruikt u Hallo volgende opdracht:

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > Als uw Storm 1.0.1 bits wordt gebruikt, wordt deze opdracht mislukt. Deze fout wordt veroorzaakt door [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055). In plaats daarvan [Storm installeren in uw ontwikkelomgeving](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) en Hallo gebruik de volgende informatie.

    Als u hebt [Storm geïnstalleerd in uw ontwikkelomgeving](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), kunt u opdrachten in plaats daarvan na Hallo:

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    Hallo `--local` parameter wordt op uw ontwikkelomgeving Hallo-topologie in de lokale modus uitgevoerd. Hallo `-R /topology.yaml` parameter gebruikt Hallo `topology.yaml` resource van de Hallo jar-bestand toodefine Hallo topologie van het bestand.

    Als dit wordt uitgevoerd, geeft Hallo topologie starten van de informatie. na de tekst Hello is een voorbeeld van uitvoer Hallo:

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    Er is een vertraging van 10 seconden tussen batches van geregistreerde gegevens.

2. Maak een kopie van Hallo `topology.yaml` bestand uit Hallo-project. Nieuwe bestandsnaam Hallo `newtopology.yaml`. In Hallo `newtopology.yaml` bestand, zoek Hallo volgende sectie en wijzig de waarde Hallo van `10` te`5`. Deze wijziging wijzigingen hello-interval tussen het verzenden van batches van word telt van too5 10 seconden.

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    Of als u Storm op uw ontwikkelingsomgeving hebt:

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    Wijziging Hallo `/path/to/newtopology.yaml` toohello pad toohello newtopology.yaml bestand dat u in de vorige stap Hallo hebt gemaakt. Met deze opdracht maakt gebruik van Hallo newtopology.yaml als Hallo topologie definitie. Aangezien we Hallo niet opnemen `compile` parameter Maven gebruikt Hallo-versie van Hallo project is ingebouwd in de vorige stappen.

    Eenmaal Hallo topologie begint, moet u merkt dat Hallo tijd tussen verzonden batches tooreflect Hallo waarde in newtopology.yaml is gewijzigd. Zo kunt u zien dat u uw configuratie via een YAML-bestand wijzigen kunt zonder toorecompile Hallo topologie.

Zie voor meer informatie over deze en andere functies van Hallo lichtstroom framework [lichtstroom (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

## <a name="trident"></a>Trident

Trident is een abstractie op hoog niveau die wordt geleverd door Storm. Biedt ondersteuning voor stateful verwerking. Hallo het belangrijkste voordeel van Trident is dat garanderen kunnen dat elk bericht dat Hallo topologie opgeeft slechts één keer wordt verwerkt. Trident gebruikt, kan uw topologie alleen garanderen dat berichten ten minste één keer worden verwerkt. Er zijn ook andere verschillen, zoals de ingebouwde componenten die kunnen worden gebruikt in plaats van bolts maken. Bolts zijn in feite is vervangen door minder-algemene onderdelen, zoals filters, projecties en functies.

Trident toepassingen kunnen worden gemaakt met behulp van Maven-projecten. U hello gebruiken dezelfde basic stappen zoals eerder in dit artikel wordt beschreven, alleen Hallo code verschilt. Trident kan niet ook (momenteel) worden gebruikt met Hallo lichtstroom framework.

Zie voor meer informatie over Trident Hallo [Trident-API-overzicht](http://storm.apache.org/documentation/Trident-API-Overview.html).

Zie voor een voorbeeld van een toepassing Trident [Twitter trends onderwerpen met Apache Storm op HDInsight](hdinsight-storm-twitter-trending.md).

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe toocreate een Storm-topologie met behulp van Java. Nu informatie over hoe:

* [Implementeren en beheren van Apache Storm-topologieën op HDInsight](hdinsight-storm-deploy-monitor-topology.md)

* [C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

U vindt meer voorbeeld Storm-topologieën in via [voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md).

