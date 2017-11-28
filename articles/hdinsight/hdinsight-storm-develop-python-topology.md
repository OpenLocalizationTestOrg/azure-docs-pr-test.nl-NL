---
title: aaaApache Storm met Python comopnents - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toocreate een Apache Storm-topologie die gebruikmaakt van Python-onderdelen.
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
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="2f3be-104">Apache Storm-topologieën op HDInsight met behulp van Python ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="2f3be-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="2f3be-105">Meer informatie over hoe toocreate een Apache Storm-topologie die gebruikmaakt van Python-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="2f3be-105">Learn how toocreate an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="2f3be-106">Apache Storm ondersteunt meerdere talen zelfs zodat u toocombine onderdelen van verschillende talen in een topologie.</span><span class="sxs-lookup"><span data-stu-id="2f3be-106">Apache Storm supports multiple languages, even allowing you toocombine components from several languages in one topology.</span></span> <span data-ttu-id="2f3be-107">Hallo lichtstroom framework (geïntroduceerd met Storm 0.10.0) kunt u tooeasily oplossingen die werken met Python-onderdelen maken.</span><span class="sxs-lookup"><span data-stu-id="2f3be-107">hello Flux framework (introduced with Storm 0.10.0) allows you tooeasily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f3be-108">Hallo-informatie in dit document is getest met Storm op HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="2f3be-108">hello information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="2f3be-109">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="2f3be-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2f3be-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2f3be-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="2f3be-111">Hallo-code voor dit project is beschikbaar op [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="2f3be-111">hello code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f3be-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2f3be-112">Prerequisites</span></span>

* <span data-ttu-id="2f3be-113">Python 2.7 of hoger</span><span class="sxs-lookup"><span data-stu-id="2f3be-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="2f3be-114">Java JDK 1.8 of hoger</span><span class="sxs-lookup"><span data-stu-id="2f3be-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="2f3be-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="2f3be-115">Maven 3</span></span>

* <span data-ttu-id="2f3be-116">(Optioneel) Een lokale Storm-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="2f3be-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="2f3be-117">Een lokale Storm-omgeving is alleen nodig als u wilt dat lokaal toorun Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="2f3be-117">A local Storm environment is only needed if you want toorun hello topology locally.</span></span> <span data-ttu-id="2f3be-118">Zie voor meer informatie [een ontwikkelomgeving instellen](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="2f3be-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="2f3be-119">Storm-ondersteuning voor meerdere talen</span><span class="sxs-lookup"><span data-stu-id="2f3be-119">Storm multi-language support</span></span>

<span data-ttu-id="2f3be-120">Apache Storm is ontworpen toowork met onderdelen die zijn geschreven met behulp van elke programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="2f3be-120">Apache Storm was designed toowork with components written using any programming language.</span></span> <span data-ttu-id="2f3be-121">Hallo-onderdelen moeten begrijpen hoe toowork Hello [Thrift-definitie voor Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="2f3be-121">hello components must understand how toowork with hello [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="2f3be-122">Voor Python, wordt een module geleverd als onderdeel van Hallo Apache Storm-project waarmee u tooeasily interface met Storm.</span><span class="sxs-lookup"><span data-stu-id="2f3be-122">For Python, a module is provided as part of hello Apache Storm project that allows you tooeasily interface with Storm.</span></span> <span data-ttu-id="2f3be-123">U vindt deze module op [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="2f3be-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="2f3be-124">Storm is een Java-proces dat wordt uitgevoerd op Hallo Java Virtual Machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="2f3be-124">Storm is a Java process that runs on hello Java Virtual Machine (JVM).</span></span> <span data-ttu-id="2f3be-125">Onderdelen die zijn geschreven in andere talen worden uitgevoerd als subprocessen.</span><span class="sxs-lookup"><span data-stu-id="2f3be-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="2f3be-126">Hallo Storm communiceert met deze subprocessen met behulp van JSON-berichten via stdin/stdout verzonden.</span><span class="sxs-lookup"><span data-stu-id="2f3be-126">hello Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="2f3be-127">Meer informatie over de communicatie tussen onderdelen vindt u in Hallo [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentatie.</span><span class="sxs-lookup"><span data-stu-id="2f3be-127">More details on communication between components can be found in hello [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-hello-flux-framework"></a><span data-ttu-id="2f3be-128">Python met Hallo lichtstroom framework</span><span class="sxs-lookup"><span data-stu-id="2f3be-128">Python with hello Flux framework</span></span>

<span data-ttu-id="2f3be-129">Hallo lichtstroom framework kunt u Storm-topologieën toodefine afzonderlijk van Hallo-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="2f3be-129">hello Flux framework allows you toodefine Storm topologies separately from hello components.</span></span> <span data-ttu-id="2f3be-130">Hallo lichtstroom framework gebruikt YAML toodefine Hallo Storm-topologie.</span><span class="sxs-lookup"><span data-stu-id="2f3be-130">hello Flux framework uses YAML toodefine hello Storm topology.</span></span> <span data-ttu-id="2f3be-131">Hallo volgende tekst is een voorbeeld van hoe tooreference een Python-component in Hallo YAML document:</span><span class="sxs-lookup"><span data-stu-id="2f3be-131">hello following text is an example of how tooreference a Python component in hello YAML document:</span></span>

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

<span data-ttu-id="2f3be-132">Hallo klasse `FluxShellSpout` is gebruikte toostart hello `sentencespout.py` script dat Hallo spout implementeert.</span><span class="sxs-lookup"><span data-stu-id="2f3be-132">hello class `FluxShellSpout` is used toostart hello `sentencespout.py` script that implements hello spout.</span></span>

<span data-ttu-id="2f3be-133">Lichtstroom Hallo Python-scripts toobe verwacht in Hallo `/resources` map binnen Hallo jar-bestand dat Hallo topologie bevat.</span><span class="sxs-lookup"><span data-stu-id="2f3be-133">Flux expects hello Python scripts toobe in hello `/resources` directory inside hello jar file that contains hello topology.</span></span> <span data-ttu-id="2f3be-134">Dus in dit voorbeeld Hallo Python-scripts in Hallo slaat `/multilang/resources` directory.</span><span class="sxs-lookup"><span data-stu-id="2f3be-134">So this example stores hello Python scripts in hello `/multilang/resources` directory.</span></span> <span data-ttu-id="2f3be-135">Hallo `pom.xml` bevat dit bestand met behulp van Hallo XML te volgen:</span><span class="sxs-lookup"><span data-stu-id="2f3be-135">hello `pom.xml` includes this file using hello following XML:</span></span>

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="2f3be-136">Zoals eerder vermeld, wordt er een `storm.py` bestand dat Hallo Thrift-definitie voor Storm implementeert.</span><span class="sxs-lookup"><span data-stu-id="2f3be-136">As mentioned earlier, there is a `storm.py` file that implements hello Thrift definition for Storm.</span></span> <span data-ttu-id="2f3be-137">Hallo lichtstroom framework bevat `storm.py` automatisch wanneer Hallo project is gebouwd, dus u geen tooworry hebt over te nemen.</span><span class="sxs-lookup"><span data-stu-id="2f3be-137">hello Flux framework includes `storm.py` automatically when hello project is built, so you don't have tooworry about including it.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="2f3be-138">Hallo-project maken</span><span class="sxs-lookup"><span data-stu-id="2f3be-138">Build hello project</span></span>

<span data-ttu-id="2f3be-139">Gebruik van Hallo hoofdmap van Hallo-project, Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2f3be-139">From hello root of hello project, use hello following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="2f3be-140">Deze opdracht maakt u een `target/WordCount-1.0-SNAPSHOT.jar` -bestand met de Hallo gecompileerd topologie.</span><span class="sxs-lookup"><span data-stu-id="2f3be-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains hello compiled topology.</span></span>

## <a name="run-hello-topology-locally"></a><span data-ttu-id="2f3be-141">Hallo-topologie lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2f3be-141">Run hello topology locally</span></span>

<span data-ttu-id="2f3be-142">lokaal toorun Hallo-topologie Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2f3be-142">toorun hello topology locally, use hello following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="2f3be-143">Deze opdracht moet een lokale Storm-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="2f3be-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="2f3be-144">Zie voor meer informatie [een ontwikkelomgeving instellen](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span><span class="sxs-lookup"><span data-stu-id="2f3be-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="2f3be-145">Eenmaal Hallo-topologie wordt gestart, het verzendt informatie toohello lokale console vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="2f3be-145">Once hello topology starts, it emits information toohello local console similar toohello following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="2f3be-146">Gebruik-topologie Hallo toostop __Ctrl + c drukken__.</span><span class="sxs-lookup"><span data-stu-id="2f3be-146">toostop hello topology, use __Ctrl + C__.</span></span>

## <a name="run-hello-storm-topology-on-hdinsight"></a><span data-ttu-id="2f3be-147">Hallo Storm-topologie op HDInsight uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2f3be-147">Run hello Storm topology on HDInsight</span></span>

1. <span data-ttu-id="2f3be-148">Gebruik Hallo volgende opdracht toocopy hello `WordCount-1.0-SNAPSHOT.jar` bestand tooyour Storm op HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="2f3be-148">Use hello following command toocopy hello `WordCount-1.0-SNAPSHOT.jar` file tooyour Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="2f3be-149">Vervang `sshuser` met Hallo SSH-gebruiker voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="2f3be-149">Replace `sshuser` with hello SSH user for your cluster.</span></span> <span data-ttu-id="2f3be-150">Vervang `mycluster` met de naam van de cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="2f3be-150">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="2f3be-151">Hebt u mogelijk na vragen aan gebruiker tooenter Hallo wachtwoord voor Hallo SSH-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2f3be-151">You may be prompted tooenter hello password for hello SSH user.</span></span>

    <span data-ttu-id="2f3be-152">Zie voor meer informatie over het gebruik van SSH en SCP [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2f3be-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="2f3be-153">Zodra het Hallo-bestand zijn geüpload, sluit u toohello-cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="2f3be-153">Once hello file has been uploaded, connect toohello cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="2f3be-154">Gebruik vanaf Hallo SSH-sessie, Hallo opdracht toostart Hallo topologie op Hallo-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="2f3be-154">From hello SSH session, use hello following command toostart hello topology on hello cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="2f3be-155">U kunt Hallo Storm-gebruikersinterface tooview Hallo topologie op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2f3be-155">You can use hello Storm UI tooview hello topology on hello cluster.</span></span> <span data-ttu-id="2f3be-156">Hallo Storm-gebruikersinterface bevindt zich op https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="2f3be-156">hello Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="2f3be-157">Vervang `mycluster` met de clusternaam van uw.</span><span class="sxs-lookup"><span data-stu-id="2f3be-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="2f3be-158">Eenmaal gestart, wordt een Storm-topologie uitgevoerd totdat deze wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="2f3be-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="2f3be-159">toostop Hallo topologie, gebruikt u een van de volgende methoden Hallo:</span><span class="sxs-lookup"><span data-stu-id="2f3be-159">toostop hello topology, use one of hello following methods:</span></span>
>
> * <span data-ttu-id="2f3be-160">Hallo `storm kill TOPOLOGYNAME` opdracht vanaf de opdrachtregel Hallo</span><span class="sxs-lookup"><span data-stu-id="2f3be-160">hello `storm kill TOPOLOGYNAME` command from hello command line</span></span>
> * <span data-ttu-id="2f3be-161">Hallo **Kill** knop in Hallo Storm-gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="2f3be-161">hello **Kill** button in hello Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2f3be-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f3be-162">Next steps</span></span>

<span data-ttu-id="2f3be-163">Zie de volgende documenten voor andere manieren toouse Python met HDInsight Hallo:</span><span class="sxs-lookup"><span data-stu-id="2f3be-163">See hello following documents for other ways toouse Python with HDInsight:</span></span>

* [<span data-ttu-id="2f3be-164">Hoe toouse Python voor streaming MapReduce-taken</span><span class="sxs-lookup"><span data-stu-id="2f3be-164">How toouse Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="2f3be-165">Hoe toouse Python gebruiker gedefinieerde functies (UDF) in Pig en Hive</span><span class="sxs-lookup"><span data-stu-id="2f3be-165">How toouse Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
