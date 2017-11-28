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
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="cd7b5-103">Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="cd7b5-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="cd7b5-104">Meer informatie over hoe toouse Azure Event Hubs met Storm op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-104">Learn how toouse Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="cd7b5-105">In dit voorbeeld maakt gebruik van Java-onderdelen tooread en write-gegevens in Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-105">This example uses Java-based components tooread and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="cd7b5-106">Azure Event Hubs kunt u tooprocess enorme hoeveelheden gegevens van websites, apps en apparaten.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-106">Azure Event Hubs allows you tooprocess massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="cd7b5-107">Hallo Event Hub spout maakt het eenvoudig toouse Apache Storm op HDInsight tooanalyze deze gegevens in realtime.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-107">hello Event Hub spout makes it easy toouse Apache Storm on HDInsight tooanalyze this data in real time.</span></span> <span data-ttu-id="cd7b5-108">U kunt ook gegevens tooEvent Hubs van Storm schrijven met behulp van Hallo Event Hubs Bolts.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-108">You can also write data tooEvent Hubs from Storm by using hello Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd7b5-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cd7b5-109">Prerequisites</span></span>

* <span data-ttu-id="cd7b5-110">Een Apache Storm op HDInsight-cluster versie 3.6.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="cd7b5-111">Zie voor meer informatie [aan de slag met Storm op HDInsight-cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cd7b5-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="cd7b5-112">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-112">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cd7b5-113">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="cd7b5-114">Een [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="cd7b5-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="cd7b5-115">[Oracle Java Developer Kit (JDK) versie 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) of gelijkwaardig, zoals [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="cd7b5-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="cd7b5-116">[Maven](https://maven.apache.org/download.cgi): Maven is een project build-systeem voor Java-projecten.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="cd7b5-117">Een teksteditor of geïntegreerde ontwikkelomgeving (IDE).</span><span class="sxs-lookup"><span data-stu-id="cd7b5-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="cd7b5-118">Uw editor of IDE mogelijk specifieke functionaliteit voor het werken met Maven die niet in dit document wordt besproken.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="cd7b5-119">Zie voor informatie over het Hallo-mogelijkheden van uw omgeving voor het bewerken, Hallo-documentatie voor Hallo product dat u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-119">For information about hello capabilities of your editing environment, see hello documentation for hello product you are using.</span></span>

    * <span data-ttu-id="cd7b5-120">Een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-120">An SSH client.</span></span> <span data-ttu-id="cd7b5-121">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="cd7b5-122">Hallo `ssh` en `scp` opdrachten.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-122">hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="cd7b5-123">Dit zijn de gebruikte toocopy bestanden toohello HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-123">These are used toocopy files toohello HDInsight cluster.</span></span> <span data-ttu-id="cd7b5-124">Op Windows, kunt u deze via Bash op Windows 10 krijgen.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-hello-example"></a><span data-ttu-id="cd7b5-125">Understanding Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cd7b5-125">Understanding hello example</span></span>

<span data-ttu-id="cd7b5-126">Hallo [hdinsight, java, storm, eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) voorbeeld bevat twee topologieën:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-126">hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="cd7b5-127">Hallo `resources/writer.yaml` topologie schrijft willekeurige gegevens tooan Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-127">hello `resources/writer.yaml` topology writes random data tooan Azure Event Hub.</span></span> <span data-ttu-id="cd7b5-128">Hallo-gegevens worden gegenereerd door Hallo `DeviceSpout` onderdeel, en is een willekeurige apparaat-ID en de waarde van apparaat.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-128">hello data is generated by hello `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="cd7b5-129">Het wordt dus bepaalde hardware die een tekenreeks-ID en een numerieke waarde verzendt simuleren.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="cd7b5-130">Thee `resources/reader.yaml` topologie leest gegevens uit Event Hub (Hallo gegevens geschreven door EventHubWriter,) parseert Hallo JSON-gegevens en meldt zich dan Hallo `deviceId` en `deviceValue` gegevens.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-130">Thee `resources/reader.yaml` topology reads data from Event Hub (hello data written by EventHubWriter,) parses hello JSON data, and then logs hello `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="cd7b5-131">Hallo-gegevens zijn opgemaakt als een JSON-document voordat deze wordt tooEvent Hub geschreven en door Hallo reader gelezen dit wordt geparseerd uit JSON en in tuples.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-131">hello data is formatted as a JSON document before it is written tooEvent Hub, and when read by hello reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="cd7b5-132">Hallo JSON-indeling is als volgt:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-132">hello JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="cd7b5-133">Project-configuratie</span><span class="sxs-lookup"><span data-stu-id="cd7b5-133">Project configuration</span></span>

<span data-ttu-id="cd7b5-134">Hallo `POM.xml` bestand bevat configuratiegegevens voor dit Maven-project.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-134">hello `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="cd7b5-135">Hallo interessante stukken zijn:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-135">hello interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="cd7b5-136">Event Hub-onderdelen</span><span class="sxs-lookup"><span data-stu-id="cd7b5-136">Event Hub components</span></span>

<span data-ttu-id="cd7b5-137">Hallo-component die leest en schrijft tooAzure Event Hubs bevindt zich in Hallo [HDInsight opslagplaats](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="cd7b5-137">hello component that reads and writes tooAzure Event Hubs is located in hello [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="cd7b5-138">Hallo volgende secties in Hallo `POM.xml` bestand laden Hallo onderdelen uit deze opslagplaats</span><span class="sxs-lookup"><span data-stu-id="cd7b5-138">hello following sections in hello `POM.xml` file load hello components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a><span data-ttu-id="cd7b5-139">Hallo EventHubs Storm Spout afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="cd7b5-139">hello EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="cd7b5-140">Deze xml definieert een afhankelijkheid voor Hallo eventhubs, dit pakket bevat een spout om te lezen uit Event Hubs en een bolt voor het schrijven van tooit.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-140">This xml defines a dependency for hello eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing tooit.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="cd7b5-141">Deze xml configureert Hallo project toogenerate uitvoer voor Java 8, die wordt gebruikt door HDInsight 3.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-141">This xml configures hello project toogenerate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="hello-maven-shade-plugin"></a><span data-ttu-id="cd7b5-142">Hallo maven-schaduw-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="cd7b5-142">hello maven-shade-plugin</span></span>

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

<span data-ttu-id="cd7b5-143">Deze xml configureert Hallo oplossing toopackage Hallo uitvoer in een jar uber.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-143">This xml configures hello solution toopackage hello output into an uber jar.</span></span> <span data-ttu-id="cd7b5-144">Hallo jar bevat Hallo projectcode en vereiste afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-144">hello jar contains both hello project code and required dependencies.</span></span> <span data-ttu-id="cd7b5-145">Dit wordt ook gebruikt voor:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-145">It is also used to:</span></span>

* <span data-ttu-id="cd7b5-146">Wijzig de naam licentiebestanden voor Hallo afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-146">Rename license files for hello dependencies.</span></span>
* <span data-ttu-id="cd7b5-147">Uitsluiten van beveiliging/handtekeningen.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="cd7b5-148">Zorg ervoor dat meerdere implementaties van dezelfde Hallo interface worden samengevoegd tot één post.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-148">Ensure that multiple implementations of hello same interface are merged into one entry.</span></span>

<span data-ttu-id="cd7b5-149">Deze configuratie-instellingen voorkomen dat er fouten tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="cd7b5-150">Topologie definities</span><span class="sxs-lookup"><span data-stu-id="cd7b5-150">Topology definitions</span></span>

<span data-ttu-id="cd7b5-151">In dit voorbeeld wordt Hallo [lichtstroom](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-151">This example uses hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="cd7b5-152">Dit framework gebruikt YAML toodefine Hallo topologieën.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-152">This framework uses YAML toodefine hello topologies.</span></span> <span data-ttu-id="cd7b5-153">Hallo belangrijkste voordeel is dat u niet harde coderen Hallo-topologie in Java-code.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-153">hello primary benefit is that you aren't hard coding hello topology in Java code.</span></span> <span data-ttu-id="cd7b5-154">Omdat de definitie van Hallo YAML is, kunt u deze vóór het verzenden van Hallo-topologie, zonder toorecompile Alles wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-154">Since hello definition is YAML, you can change it before submitting hello topology, without having toorecompile everything.</span></span>

<span data-ttu-id="cd7b5-155">__Writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-155">__writer.yaml__:</span></span>

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

<span data-ttu-id="cd7b5-156">__Reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-156">__reader.yaml__:</span></span>

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

#### <a name="tell-hello-topology-about-event-hub"></a><span data-ttu-id="cd7b5-157">Hallo-topologie vertellen over Event Hub</span><span class="sxs-lookup"><span data-stu-id="cd7b5-157">Tell hello topology about Event Hub</span></span>

<span data-ttu-id="cd7b5-158">Tijdens runtime, Hallo `dev.properties` bestand gebruikte toopass Hallo Event Hub configuratie toohello topologie is.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-158">At run time, hello `dev.properties` file is used toopass hello Event Hub configuration toohello topology.</span></span> <span data-ttu-id="cd7b5-159">Hallo is volgende voorbeeld de Standaardinhoud Hallo van Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-159">hello following example is hello default contents of hello file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="cd7b5-160">Omgevingsvariabelen configureren</span><span class="sxs-lookup"><span data-stu-id="cd7b5-160">Configure environment variables</span></span>

<span data-ttu-id="cd7b5-161">Hallo kunnen volgende omgevingsvariabelen worden ingesteld wanneer u Java en Hallo JDK op uw ontwikkelwerkstation installeert.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-161">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="cd7b5-162">Echter, moet u controleren of ze bestaan en dat ze de juiste waarden voor uw systeem Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-162">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="cd7b5-163">**JAVA_HOME** -toohello directory waar Hallo Java runtime environment (JRE) is geïnstalleerd moet verwijzen.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-163">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="cd7b5-164">Bijvoorbeeld in een Unix- of Linux-distributie, heeft een waarde gelijkaardig te`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-164">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="cd7b5-165">In Windows, zou er een waarde gelijkaardig te`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="cd7b5-165">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="cd7b5-166">**PAD** -moet bevatten Hallo paden te volgen:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-166">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="cd7b5-167">**JAVA_HOME** (of equivalente paden Hallo)</span><span class="sxs-lookup"><span data-stu-id="cd7b5-167">**JAVA_HOME** (or hello equivalent path)</span></span>
  * <span data-ttu-id="cd7b5-168">**JAVA_HOME\bin** (of equivalente paden Hallo)</span><span class="sxs-lookup"><span data-stu-id="cd7b5-168">**JAVA_HOME\bin** (or hello equivalent path)</span></span>
  * <span data-ttu-id="cd7b5-169">Hallo-directory waar Maven is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="cd7b5-169">hello directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="cd7b5-170">Event Hub configureren</span><span class="sxs-lookup"><span data-stu-id="cd7b5-170">Configure Event Hub</span></span>

<span data-ttu-id="cd7b5-171">Event Hubs is Hallo gegevensbron voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-171">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="cd7b5-172">Volgende stappen toocreate een Event Hub hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-172">Use hello following steps toocreate a Event Hub.</span></span>

1. <span data-ttu-id="cd7b5-173">Van Hallo [klassieke Azure-Portal](https://manage.windowsazure.com), selecteer **nieuw** > **Service Bus** > **Event Hub**  >  **Aangepast maken**.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-173">From hello [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="cd7b5-174">Op Hallo **toevoegen van nieuwe Event Hub** scherm, voert u een **naam Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-174">On hello **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="cd7b5-175">Selecteer Hallo **regio** toocreate Hallo-hub in, en vervolgens een naamruimte maken of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-175">Select hello **Region** toocreate hello hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="cd7b5-176">Tot slot op Hallo **pijl** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-176">Finally, click hello **Arrow** toocontinue.</span></span>

    ![wizardpagina 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="cd7b5-178">Selecteer dezelfde Hallo **locatie** als uw Storm op HDInsight-server tooreduce latentie en kosten.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-178">Select hello same **Location** as your Storm on HDInsight server tooreduce latency and costs.</span></span>

3. <span data-ttu-id="cd7b5-179">Op Hallo **configureren Event Hub** scherm, voert u Hallo **aantal partitie** en **bericht bewaren** waarden.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-179">On hello **Configure Event Hub** screen, enter hello **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="cd7b5-180">Gebruik voor dit voorbeeld wordt een aantal partities van 10 en de retentie van een bericht van 1.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="cd7b5-181">Houd er rekening mee Hallo partitie aantal omdat u deze waarde later nodig.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-181">Note hello partition count because you need this value later.</span></span>

    ![wizardpagina 2 van de](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="cd7b5-183">Nadat u Hallo event hub hebt gemaakt, selecteer Hallo naamruimte, selecteer **Event Hubs**, en selecteer vervolgens Hallo event hub die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-183">After hello event hub has been created, select hello namespace, select **Event Hubs**, and then select hello event hub that you created earlier.</span></span>
5. <span data-ttu-id="cd7b5-184">Selecteer **configureren**, maakt u twee nieuwe beleidsregels voor toegang met behulp van Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-184">Select **Configure**, then create two new access policies by using hello following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="cd7b5-185">Naam</span><span class="sxs-lookup"><span data-stu-id="cd7b5-185">Name</span></span></th><th><span data-ttu-id="cd7b5-186">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="cd7b5-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="cd7b5-187">schrijver</span><span class="sxs-lookup"><span data-stu-id="cd7b5-187">Writer</span></span></td><td><span data-ttu-id="cd7b5-188">Verzenden</span><span class="sxs-lookup"><span data-stu-id="cd7b5-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="cd7b5-189">Lezer</span><span class="sxs-lookup"><span data-stu-id="cd7b5-189">Reader</span></span></td><td><span data-ttu-id="cd7b5-190">Luisteren</span><span class="sxs-lookup"><span data-stu-id="cd7b5-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="cd7b5-191">Nadat u Hallo machtigingen hebt gemaakt, selecteert u Hallo **opslaan** pictogram Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-191">After You create hello permissions, select hello **Save** icon at hello bottom of hello page.</span></span> <span data-ttu-id="cd7b5-192">Deze beleidsregels voor gedeelde toegang zijn gebruikte tooread en tooEvent Hub schrijven.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-192">These shared access policies are used tooread and write tooEvent Hub.</span></span>

    ![beleid](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="cd7b5-194">Nadat u Hallo beleid opslaat, gebruikt u Hallo **codegenerator voor gedeelde toegang** onderin Hallo van Hallo pagina tooretrieve Hallo sleutel voor Hallo **writer** en **lezer** beleid.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-194">After you save hello policies, use hello **Shared access key generator** at hello bottom of hello page tooretrieve hello key for hello **writer** and **reader** policies.</span></span> <span data-ttu-id="cd7b5-195">Sla deze sleutels.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-195">Save these keys.</span></span>

## <a name="download-and-build-hello-project"></a><span data-ttu-id="cd7b5-196">Download en bouw Hallo-project</span><span class="sxs-lookup"><span data-stu-id="cd7b5-196">Download and build hello project</span></span>

1. <span data-ttu-id="cd7b5-197">Hallo-project hebt gedownload van GitHub: [hdinsight, java, storm, eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="cd7b5-197">Download hello project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="cd7b5-198">U kunt het downloadpakket Hallo als een zip-archief of gebruik [git](https://git-scm.com/) tooclone Hallo-project lokaal.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-198">You can either download hello package as a zip archive, or use [git](https://git-scm.com/) tooclone hello project locally.</span></span>

2. <span data-ttu-id="cd7b5-199">Hallo wijzigen `dev.properties` bestand met de Hallo-configuratie voor uw Event Hub.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-199">Modify hello `dev.properties` file with hello configuration for your Event Hub.</span></span>

3. <span data-ttu-id="cd7b5-200">Gebruik Hallo toobuild en pakket Hallo-project te volgen:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-200">Use hello following toobuild and package hello project:</span></span>

        mvn package

    <span data-ttu-id="cd7b5-201">Met deze opdracht vereiste afhankelijkheden, builds gedownload en vervolgens de pakketten project Hallo.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-201">This command downloads required dependencies, builds, and then packages hello project.</span></span> <span data-ttu-id="cd7b5-202">Hallo-uitvoer wordt opgeslagen in Hallo **/target** map als **EventHubExample-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-202">hello output is stored in hello **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="cd7b5-203">Lokaal testen</span><span class="sxs-lookup"><span data-stu-id="cd7b5-203">Test locally</span></span>

<span data-ttu-id="cd7b5-204">Aangezien deze topologieën alleen lezen en tooEvent Hubs schrijven, kunt u deze testen lokaal hebt u een [Storm-ontwikkelomgeving](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="cd7b5-204">Since these topologies just read and write tooEvent Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="cd7b5-205">Gebruik Hallo toorun lokaal in Hallo dev omgeving stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-205">Use hello following steps toorun locally in hello dev environment:</span></span>

1. <span data-ttu-id="cd7b5-206">Hallo writer uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-206">Run hello writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="cd7b5-207">Hallo lezer uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-207">Run hello reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="cd7b5-208">`--local`: Voer Hallo-topologie in de lokale modus (niet-gedistribueerd).</span><span class="sxs-lookup"><span data-stu-id="cd7b5-208">`--local`: Run hello topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="cd7b5-209">`-R /writer.yaml`: Definitie van de topologie Hallo laden uit Hallo `resources` verpakt in Hallo jar.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-209">`-R /writer.yaml`: Load hello topology definition from hello `resources` packaged in hello jar.</span></span> <span data-ttu-id="cd7b5-210">Als een bestand op het lokale bestandssysteem Hallo Hallo topologie is Hallo pad tooit opgeven als de laatste parameter Hallo.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-210">If hello topology is a file on hello local file system, specify hello path tooit as hello last parameter instead.</span></span>
> * <span data-ttu-id="cd7b5-211">`--filter dev.properties`: Gebruik Hallo inhoud van `dev.properties` toofill Hallo-waarden in Hallo topologie definities.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-211">`--filter dev.properties`: Use hello contents of `dev.properties` toofill in hello values in hello topology definitions.</span></span> <span data-ttu-id="cd7b5-212">Bijvoorbeeld `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="cd7b5-213">Uitvoer is vastgelegd toohello console bij lokale uitvoering.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-213">Output is logged toohello console when running locally.</span></span> <span data-ttu-id="cd7b5-214">Gebruik __Ctrl + C__ toostop Hallo topologie.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-214">Use __Ctrl+C__ toostop hello topology.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="cd7b5-215">Hallo-topologieën implementeren</span><span class="sxs-lookup"><span data-stu-id="cd7b5-215">Deploy hello topologies</span></span>

1. <span data-ttu-id="cd7b5-216">SCP toocopy Hallo jar pakket tooyour HDInsight-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-216">Use SCP toocopy hello jar package tooyour HDInsight cluster.</span></span> <span data-ttu-id="cd7b5-217">GEBRUIKERSNAAM vervangen door Hallo SSH-gebruiker voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-217">Replace USERNAME with hello SSH user for your cluster.</span></span> <span data-ttu-id="cd7b5-218">Vervang CLUSTERNAME door Hallo-naam van uw HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-218">Replace CLUSTERNAME with hello name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="cd7b5-219">Als u een wachtwoord voor uw SSH-account gebruikt, zijn na vragen aan gebruiker tooenter Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-219">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="cd7b5-220">Als u een SSH-sleutel met Hallo account gebruikt, moet u mogelijk toouse hello `-i` parameter toospecify Hallo pad toohello sleutelbestand.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-220">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="cd7b5-221">Bijvoorbeeld: `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="cd7b5-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="cd7b5-222">Deze opdracht kopieert Hallo bestand toohello basismap van uw SSH-gebruiker op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-222">This command copies hello file toohello home directory of your SSH user on hello cluster.</span></span>

2. <span data-ttu-id="cd7b5-223">Zodra het Hallo-bestand is klaar met uploaden, gebruikt u SSH tooconnect toohello HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-223">Once hello file has finished uploading, use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="cd7b5-224">Vervang **gebruikersnaam** Hallo-naam van uw SSH-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-224">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="cd7b5-225">Vervang **CLUSTERNAME** met de naam van uw HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="cd7b5-226">Als u een wachtwoord voor uw SSH-account gebruikt, zijn na vragen aan gebruiker tooenter Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-226">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="cd7b5-227">Als u een SSH-sleutel met Hallo account gebruikt, moet u mogelijk toouse hello `-i` parameter toospecify Hallo pad toohello sleutelbestand.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-227">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="cd7b5-228">Hallo volgende voorbeeld wordt geladen Hallo persoonlijke sleutel uit `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-228">hello following example loads hello private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="cd7b5-229">Gebruik Hallo opdracht toostart Hallo topologieën te volgen:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-229">Use hello following command toostart hello topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="cd7b5-230">`--remote`: Hallo topologie toohello Nimbus-service op Hallo worker-knooppunten in cluster Hallo gestart verzendt.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-230">`--remote`: Submits hello topology toohello Nimbus service, which starts it on hello worker nodes in hello cluster.</span></span>

4. <span data-ttu-id="cd7b5-231">gegevens van tooview Hallo geregistreerd, gaat u toohttps://CLUSTERNAME.azurehdinsight.net/stormui, waar __CLUSTERNAME__ Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-231">tooview hello logged data, go toohttps://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="cd7b5-232">Selecteer Hallo topologieën en inzoomen toohello onderdelen.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-232">Select hello topologies and drill down toohello components.</span></span> <span data-ttu-id="cd7b5-233">Selecteer Hallo __poort__ vermelding voor een exemplaar van een onderdeel tooview informatie in het logboek geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="cd7b5-233">Select hello __port__ entry for an instance of a component tooview logged information.</span></span>

5. <span data-ttu-id="cd7b5-234">Gebruik Hallo opdrachten toostop Hallo topologieën te volgen:</span><span class="sxs-lookup"><span data-stu-id="cd7b5-234">Use hello following commands toostop hello topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="cd7b5-235">Uw cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="cd7b5-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="cd7b5-236">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cd7b5-236">Next steps</span></span>

* [<span data-ttu-id="cd7b5-237">Voorbeeldtopologieën van Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd7b5-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
