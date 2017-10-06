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
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a>Apache Storm-topologieën op HDInsight met behulp van Python ontwikkelen

Meer informatie over hoe toocreate een Apache Storm-topologie die gebruikmaakt van Python-onderdelen. Apache Storm ondersteunt meerdere talen zelfs zodat u toocombine onderdelen van verschillende talen in een topologie. Hallo lichtstroom framework (geïntroduceerd met Storm 0.10.0) kunt u tooeasily oplossingen die werken met Python-onderdelen maken.

> [!IMPORTANT]
> Hallo-informatie in dit document is getest met Storm op HDInsight 3.6. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

Hallo-code voor dit project is beschikbaar op [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).

## <a name="prerequisites"></a>Vereisten

* Python 2.7 of hoger

* Java JDK 1.8 of hoger

* Maven 3

* (Optioneel) Een lokale Storm-ontwikkelomgeving. Een lokale Storm-omgeving is alleen nodig als u wilt dat lokaal toorun Hallo-topologie. Zie voor meer informatie [een ontwikkelomgeving instellen](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).

## <a name="storm-multi-language-support"></a>Storm-ondersteuning voor meerdere talen

Apache Storm is ontworpen toowork met onderdelen die zijn geschreven met behulp van elke programmeertaal. Hallo-onderdelen moeten begrijpen hoe toowork Hello [Thrift-definitie voor Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift). Voor Python, wordt een module geleverd als onderdeel van Hallo Apache Storm-project waarmee u tooeasily interface met Storm. U vindt deze module op [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).

Storm is een Java-proces dat wordt uitgevoerd op Hallo Java Virtual Machine (JVM). Onderdelen die zijn geschreven in andere talen worden uitgevoerd als subprocessen. Hallo Storm communiceert met deze subprocessen met behulp van JSON-berichten via stdin/stdout verzonden. Meer informatie over de communicatie tussen onderdelen vindt u in Hallo [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentatie.

## <a name="python-with-hello-flux-framework"></a>Python met Hallo lichtstroom framework

Hallo lichtstroom framework kunt u Storm-topologieën toodefine afzonderlijk van Hallo-onderdelen. Hallo lichtstroom framework gebruikt YAML toodefine Hallo Storm-topologie. Hallo volgende tekst is een voorbeeld van hoe tooreference een Python-component in Hallo YAML document:

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

Hallo klasse `FluxShellSpout` is gebruikte toostart hello `sentencespout.py` script dat Hallo spout implementeert.

Lichtstroom Hallo Python-scripts toobe verwacht in Hallo `/resources` map binnen Hallo jar-bestand dat Hallo topologie bevat. Dus in dit voorbeeld Hallo Python-scripts in Hallo slaat `/multilang/resources` directory. Hallo `pom.xml` bevat dit bestand met behulp van Hallo XML te volgen:

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

Zoals eerder vermeld, wordt er een `storm.py` bestand dat Hallo Thrift-definitie voor Storm implementeert. Hallo lichtstroom framework bevat `storm.py` automatisch wanneer Hallo project is gebouwd, dus u geen tooworry hebt over te nemen.

## <a name="build-hello-project"></a>Hallo-project maken

Gebruik van Hallo hoofdmap van Hallo-project, Hallo volgende opdracht:

```bash
mvn clean compile package
```

Deze opdracht maakt u een `target/WordCount-1.0-SNAPSHOT.jar` -bestand met de Hallo gecompileerd topologie.

## <a name="run-hello-topology-locally"></a>Hallo-topologie lokaal uitvoeren

lokaal toorun Hallo-topologie Hallo volgende opdracht gebruiken:

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> Deze opdracht moet een lokale Storm-ontwikkelomgeving. Zie voor meer informatie [een ontwikkelomgeving instellen](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)

Eenmaal Hallo-topologie wordt gestart, het verzendt informatie toohello lokale console vergelijkbare toohello volgende tekst:


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


Gebruik-topologie Hallo toostop __Ctrl + c drukken__.

## <a name="run-hello-storm-topology-on-hdinsight"></a>Hallo Storm-topologie op HDInsight uitvoeren

1. Gebruik Hallo volgende opdracht toocopy hello `WordCount-1.0-SNAPSHOT.jar` bestand tooyour Storm op HDInsight-cluster:

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    Vervang `sshuser` met Hallo SSH-gebruiker voor uw cluster. Vervang `mycluster` met de naam van de cluster Hallo. Hebt u mogelijk na vragen aan gebruiker tooenter Hallo wachtwoord voor Hallo SSH-gebruiker.

    Zie voor meer informatie over het gebruik van SSH en SCP [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Zodra het Hallo-bestand zijn geüpload, sluit u toohello-cluster via SSH:

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. Gebruik vanaf Hallo SSH-sessie, Hallo opdracht toostart Hallo topologie op Hallo-cluster te volgen:

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. U kunt Hallo Storm-gebruikersinterface tooview Hallo topologie op Hallo-cluster. Hallo Storm-gebruikersinterface bevindt zich op https://mycluster.azurehdinsight.net/stormui. Vervang `mycluster` met de clusternaam van uw.

> [!NOTE]
> Eenmaal gestart, wordt een Storm-topologie uitgevoerd totdat deze wordt gestopt. toostop Hallo topologie, gebruikt u een van de volgende methoden Hallo:
>
> * Hallo `storm kill TOPOLOGYNAME` opdracht vanaf de opdrachtregel Hallo
> * Hallo **Kill** knop in Hallo Storm-gebruikersinterface.


## <a name="next-steps"></a>Volgende stappen

Zie de volgende documenten voor andere manieren toouse Python met HDInsight Hallo:

* [Hoe toouse Python voor streaming MapReduce-taken](hdinsight-hadoop-streaming-python.md)
* [Hoe toouse Python gebruiker gedefinieerde functies (UDF) in Pig en Hive](hdinsight-python.md)
