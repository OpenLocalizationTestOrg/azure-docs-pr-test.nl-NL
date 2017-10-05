---
title: Apache Storm met Python comopnents - Azure HDInsight | Microsoft Docs
description: Informatie over het maken van een Apache Storm-topologie die gebruikmaakt van Python-onderdelen.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: Apache storm python
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 305c4060ad81458b254e66a4bad6dfd7bf69b28d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="a91e3-104">Apache Storm-topologieën op HDInsight met behulp van Python ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="a91e3-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="a91e3-105">Informatie over het maken van een Apache Storm-topologie die gebruikmaakt van Python-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="a91e3-105">Learn how to create an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="a91e3-106">Apache Storm ondersteunt meerdere talen zelfs zodat u onderdelen uit verschillende talen in een topologie combineren.</span><span class="sxs-lookup"><span data-stu-id="a91e3-106">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span></span> <span data-ttu-id="a91e3-107">Het lichtstroom framework (geïntroduceerd met Storm 0.10.0) kunt u eenvoudig om oplossingen te maken die gebruikmaken van Python-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="a91e3-107">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a91e3-108">De informatie in dit document is getest met Storm op HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="a91e3-108">The information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="a91e3-109">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a91e3-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a91e3-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a91e3-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="a91e3-111">De code voor dit project is beschikbaar op [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="a91e3-111">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a91e3-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a91e3-112">Prerequisites</span></span>

* <span data-ttu-id="a91e3-113">Python 2.7 of hoger</span><span class="sxs-lookup"><span data-stu-id="a91e3-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="a91e3-114">Java JDK 1.8 of hoger</span><span class="sxs-lookup"><span data-stu-id="a91e3-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="a91e3-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="a91e3-115">Maven 3</span></span>

* <span data-ttu-id="a91e3-116">(Optioneel) Een lokale Storm-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="a91e3-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="a91e3-117">Een lokale Storm-omgeving is alleen nodig als u wilt de topologie lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a91e3-117">A local Storm environment is only needed if you want to run the topology locally.</span></span> <span data-ttu-id="a91e3-118">Zie voor meer informatie [een ontwikkelomgeving instellen](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="a91e3-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="a91e3-119">Storm-ondersteuning voor meerdere talen</span><span class="sxs-lookup"><span data-stu-id="a91e3-119">Storm multi-language support</span></span>

<span data-ttu-id="a91e3-120">Apache Storm is ontworpen om te werken met onderdelen die zijn geschreven met behulp van elke programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="a91e3-120">Apache Storm was designed to work with components written using any programming language.</span></span> <span data-ttu-id="a91e3-121">De onderdelen moeten begrijpen hoe u werkt met de [Thrift-definitie voor Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="a91e3-121">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="a91e3-122">Voor Python, wordt een module geleverd als onderdeel van de Apache Storm-project waarmee u eenvoudig een interface met Storm.</span><span class="sxs-lookup"><span data-stu-id="a91e3-122">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span></span> <span data-ttu-id="a91e3-123">U vindt deze module op [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="a91e3-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="a91e3-124">Storm is een Java-proces dat wordt uitgevoerd op de Java-virtuele Machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="a91e3-124">Storm is a Java process that runs on the Java Virtual Machine (JVM).</span></span> <span data-ttu-id="a91e3-125">Onderdelen die zijn geschreven in andere talen worden uitgevoerd als subprocessen.</span><span class="sxs-lookup"><span data-stu-id="a91e3-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="a91e3-126">De Storm communiceert met deze subprocessen met behulp van JSON-berichten via stdin/stdout verzonden.</span><span class="sxs-lookup"><span data-stu-id="a91e3-126">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="a91e3-127">Meer informatie over de communicatie tussen onderdelen vindt u in de [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentatie.</span><span class="sxs-lookup"><span data-stu-id="a91e3-127">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-the-flux-framework"></a><span data-ttu-id="a91e3-128">Python met lichtstroom framework</span><span class="sxs-lookup"><span data-stu-id="a91e3-128">Python with the Flux framework</span></span>

<span data-ttu-id="a91e3-129">Het framework lichtstroom kunt u Storm-topologieën afzonderlijk van de onderdelen te definiëren.</span><span class="sxs-lookup"><span data-stu-id="a91e3-129">The Flux framework allows you to define Storm topologies separately from the components.</span></span> <span data-ttu-id="a91e3-130">Het framework lichtstroom gebruikt YAML voor het definiëren van de Storm-topologie.</span><span class="sxs-lookup"><span data-stu-id="a91e3-130">The Flux framework uses YAML to define the Storm topology.</span></span> <span data-ttu-id="a91e3-131">De volgende tekst is een voorbeeld van een Python-component in het document YAML verwijzen naar:</span><span class="sxs-lookup"><span data-stu-id="a91e3-131">The following text is an example of how to reference a Python component in the YAML document:</span></span>

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

<span data-ttu-id="a91e3-132">De klasse `FluxShellSpout` wordt gebruikt om te beginnen de `sentencespout.py` script dat de spout implementeert.</span><span class="sxs-lookup"><span data-stu-id="a91e3-132">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span></span>

<span data-ttu-id="a91e3-133">Lichtstroom verwacht de Python-scripts in de `/resources` map binnen het jar-bestand dat de topologie bevat.</span><span class="sxs-lookup"><span data-stu-id="a91e3-133">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span></span> <span data-ttu-id="a91e3-134">Dus in dit voorbeeld Slaat het Python-scripts in de `/multilang/resources` directory.</span><span class="sxs-lookup"><span data-stu-id="a91e3-134">So this example stores the Python scripts in the `/multilang/resources` directory.</span></span> <span data-ttu-id="a91e3-135">De `pom.xml` deze met behulp van de volgende XML-bestand bevat:</span><span class="sxs-lookup"><span data-stu-id="a91e3-135">The `pom.xml` includes this file using the following XML:</span></span>

```xml
<!-- include the Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="a91e3-136">Zoals eerder vermeld, wordt er een `storm.py` bestand dat de Thrift-definitie voor Storm implementeert.</span><span class="sxs-lookup"><span data-stu-id="a91e3-136">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span></span> <span data-ttu-id="a91e3-137">Het framework lichtstroom bevat `storm.py` automatisch wanneer het project is gebouwd, zodat u niet hoeft te hoeven maken over te nemen.</span><span class="sxs-lookup"><span data-stu-id="a91e3-137">The Flux framework includes `storm.py` automatically when the project is built, so you don't have to worry about including it.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="a91e3-138">Het project bouwen</span><span class="sxs-lookup"><span data-stu-id="a91e3-138">Build the project</span></span>

<span data-ttu-id="a91e3-139">Gebruik de volgende opdracht in de hoofdmap van het project:</span><span class="sxs-lookup"><span data-stu-id="a91e3-139">From the root of the project, use the following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="a91e3-140">Deze opdracht maakt u een `target/WordCount-1.0-SNAPSHOT.jar` -bestand met de gecompileerde topologie.</span><span class="sxs-lookup"><span data-stu-id="a91e3-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span></span>

## <a name="run-the-topology-locally"></a><span data-ttu-id="a91e3-141">De topologie lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a91e3-141">Run the topology locally</span></span>

<span data-ttu-id="a91e3-142">Als u wilt de topologie lokaal uitvoeren, moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a91e3-142">To run the topology locally, use the following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="a91e3-143">Deze opdracht moet een lokale Storm-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="a91e3-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="a91e3-144">Zie voor meer informatie [een ontwikkelomgeving instellen](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span><span class="sxs-lookup"><span data-stu-id="a91e3-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="a91e3-145">Eenmaal de topologie wordt gestart, het verzendt gegevens naar de lokale console vergelijkbaar met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="a91e3-145">Once the topology starts, it emits information to the local console similar to the following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="a91e3-146">Voor het beëindigen van de topologie gebruikt __Ctrl + c drukken__.</span><span class="sxs-lookup"><span data-stu-id="a91e3-146">To stop the topology, use __Ctrl + C__.</span></span>

## <a name="run-the-storm-topology-on-hdinsight"></a><span data-ttu-id="a91e3-147">De topologie Storm op HDInsight uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a91e3-147">Run the Storm topology on HDInsight</span></span>

1. <span data-ttu-id="a91e3-148">Gebruik de volgende opdracht om te kopiëren de `WordCount-1.0-SNAPSHOT.jar` -bestand naar uw Storm op HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="a91e3-148">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="a91e3-149">Vervang `sshuser` met de SSH-gebruiker voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="a91e3-149">Replace `sshuser` with the SSH user for your cluster.</span></span> <span data-ttu-id="a91e3-150">Vervang `mycluster` met de naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="a91e3-150">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="a91e3-151">U wordt mogelijk gevraagd het wachtwoord invoeren voor de SSH-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a91e3-151">You may be prompted to enter the password for the SSH user.</span></span>

    <span data-ttu-id="a91e3-152">Zie voor meer informatie over het gebruik van SSH en SCP [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a91e3-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="a91e3-153">Zodra het bestand zijn geüpload, verbinding maken met het cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="a91e3-153">Once the file has been uploaded, connect to the cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="a91e3-154">Gebruik de volgende opdracht voor het starten van de topologie op het cluster van de SSH-sessie:</span><span class="sxs-lookup"><span data-stu-id="a91e3-154">From the SSH session, use the following command to start the topology on the cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="a91e3-155">U kunt de Storm-gebruikersinterface gebruiken om de topologie op het cluster weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a91e3-155">You can use the Storm UI to view the topology on the cluster.</span></span> <span data-ttu-id="a91e3-156">De Storm-gebruikersinterface bevindt zich op https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="a91e3-156">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="a91e3-157">Vervang `mycluster` met de clusternaam van uw.</span><span class="sxs-lookup"><span data-stu-id="a91e3-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="a91e3-158">Eenmaal gestart, wordt een Storm-topologie uitgevoerd totdat deze wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="a91e3-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="a91e3-159">Als u wilt de topologie stoppen, moet u een van de volgende methoden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a91e3-159">To stop the topology, use one of the following methods:</span></span>
>
> * <span data-ttu-id="a91e3-160">De `storm kill TOPOLOGYNAME` opdracht vanaf de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="a91e3-160">The `storm kill TOPOLOGYNAME` command from the command line</span></span>
> * <span data-ttu-id="a91e3-161">De **Kill** knop in de Storm-gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="a91e3-161">The **Kill** button in the Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a91e3-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a91e3-162">Next steps</span></span>

<span data-ttu-id="a91e3-163">Zie de volgende documenten voor andere manieren om te Python gebruiken met HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a91e3-163">See the following documents for other ways to use Python with HDInsight:</span></span>

* [<span data-ttu-id="a91e3-164">Het gebruik van Python voor streaming MapReduce-taken</span><span class="sxs-lookup"><span data-stu-id="a91e3-164">How to use Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="a91e3-165">Het gebruik van Python gebruiker gedefinieerde functies (UDF) in Pig en Hive</span><span class="sxs-lookup"><span data-stu-id="a91e3-165">How to use Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
