---
title: aaaApache Storm schrijven tooStorage/de Data Lake Store - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Apache Storm toowrite toohello HDFS-compatibele opslag Hallo voor HDInsight. Azure Storage of Azure Data Lake Store moet u Hallo HDFS comptabile opslag bieden voor HDInsight. In dit document en Hallo gekoppeld bijvoorbeeld laten zien hoe Hallo HdfsBolt component gebruikte toowrite toohello standaard opslag van een Storm op HDInsight-cluster is.
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a>Om tooHDFS van Apache Storm op HDInsight te schrijven

Meer informatie over hoe toouse Storm toowrite gegevens toohello HDFS-compatibele opslag wordt gebruikt door Apache Storm op HDInsight. HDInsight kunt gebruiken beide Azure Storage en Azure Data Lake opslaan als HDFS comptabile opslag. Storm biedt een [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) onderdeel dat gegevens tooHDFS schrijft. Dit document bevat informatie over het schrijven van tooeither type opslag van Hallo HdfsBolt. 

> [!IMPORTANT]
> Hallo-voorbeeld topologie in dit document gebruikt afhankelijk van de onderdelen die deel van Storm op HDInsight uitmaken. Deze wijziging toowork met Azure Data Lake Store gebruikt in combinatie met andere Apache Storm-clusters mogelijk.

## <a name="get-hello-code"></a>Hallo code ophalen

Hallo-project met deze topologie wordt beschikbaar als download van [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).

toocompile dit project, moet u na de configuratie voor uw ontwikkelomgeving Hallo:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) of hoger. HDInsight 3.5 of hoger vereisen Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

Hallo kunnen volgende omgevingsvariabelen worden ingesteld wanneer u Java en Hallo JDK op uw ontwikkelwerkstation installeert. Echter, moet u controleren of ze bestaan en dat ze de juiste waarden voor uw systeem Hallo bevatten.

* `JAVA_HOME`-moet verwijzen toohello directory waarin hello JDK is geïnstalleerd.
* `PATH`-moet bevatten Hallo paden te volgen:
  
    * `JAVA_HOME`(of gelijkwaardige Hallo-pad).
    * `JAVA_HOME\bin`(of gelijkwaardige Hallo-pad).
    * Hallo-map is waarin Maven is geïnstalleerd.

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a>Hoe toouse Hallo HdfsBolt met HDInsight

> [!IMPORTANT]
> Voordat u Hallo HdfsBolt met Storm op HDInsight, moet u eerst een script actie toocopy vereist jar-bestanden gebruiken in Hallo `extpath` voor Storm. Zie voor meer informatie, Hallo [Hallo-cluster configureren](#configure) sectie.

Hallo HdfsBolt gebruikt Hallo bestand schema dat u toounderstand hoe bieden toowrite tooHDFS. Met HDInsight, gebruikt u een Hallo schema's te volgen:

* `wasb://`: Met een Azure Storage-account gebruikt.
* `adl://`: Gebruikt met Azure Data Lake Store.

Hallo bevat volgende tabel voorbeelden van het gebruik van Hallo bestand schema voor verschillende scenario's:

| Schema | Opmerkingen |
| ----- | ----- |
| `wasb:///` | Hallo standaard storage-account is een blobcontainer in Azure Storage-account |
| `adl:///` | Hallo standaardopslagaccount is een map in Azure Data Lake Store. Tijdens het maken geeft u Hallo directory in Data Lake Store die Hallo hoofdmap van de HDFS Hallo-cluster. Bijvoorbeeld, Hallo `/clusters/myclustername/` directory. |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | Een niet-standaard (Extra) Azure-opslagaccount gekoppeld Hallo-cluster. |
| `adl://STORENAME/` | Hallo root Hallo Data Lake Store door Hallo cluster gebruikt. Dit schema kunt u tooaccess gegevens die zich buiten het Hallo-map met de Hallo cluster bestandssysteem bevindt. |

Zie voor meer informatie, Hallo [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) verwijzing op Apache.org.

### <a name="example-configuration"></a>Voorbeeldconfiguratie

Hallo volgende YAML is een fragment uit Hallo `resources/writetohdfs.yaml` op Hallo voorbeeld bestand. Dit bestand definieert Hallo Storm-topologie met Hallo [lichtstroom](https://storm.apache.org/releases/1.1.0/flux.html) framework voor Apache Storm.

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

Deze YAML definieert Hallo volgende items:

* `syncPolicy`: Hiermee wordt gedefinieerd wanneer bestanden gesynchroniseerd/leeggemaakte toohello-bestandssysteem zijn. In dit voorbeeld elke 1000 tuples.
* `fileNameFormat`: Hiermee definieert u Hallo pad en naam patroon toouse bij het schrijven van bestanden. In dit voorbeeld Hallo pad is opgegeven tijdens runtime met een filter, en de bestandsextensie Hallo `.txt`.
* `recordFormat`: Definieert Hallo interne indeling van Hallo-bestanden die zijn geschreven. In dit voorbeeld velden worden gescheiden door Hallo `|` teken.
* `rotationPolicy`: Hiermee wordt gedefinieerd of toorotate bestanden. In dit voorbeeld wordt geen draaiing uitgevoerd.
* `hdfs-bolt`: Gebruik voorliggende onderdelen als configuratieparameters voor Hallo Hallo `HdfsBolt` klasse.

Zie voor meer informatie over Hallo lichtstroom framework [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="configure-hello-cluster"></a>Hallo-cluster configureren

Storm op HDInsight omvat standaard geen Hallo onderdelen HdfsBolt toocommunicate gebruikt met Azure Storage of de Data Lake Store in klassenpad van Storm. Gebruik Hallo volgende script actie tooadd deze onderdelen toohello `extlib` map voor Storm op het cluster:

| Script URI | Knooppunten tooapply naar | Parameters || `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | Geen |

Zie voor informatie over het gebruik van dit script met uw cluster Hallo [aanpassen HDInsight-clusters met behulp van scriptacties](./hdinsight-hadoop-customize-cluster-linux.md) document.

## <a name="build-and-package-hello-topology"></a>Bouw en het Hallo-topologie van het pakket

1. Hallo-voorbeeldproject van downloaden [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour ontwikkelomgeving.

2. Terminal of shell-sessie wijzigen mappen toohello hoofdmap Hallo gedownload vanaf een opdrachtprompt project. toobuild en pakket Hallo topologie, Hallo volgende opdracht gebruiken:
   
        mvn compile package
   
    Zodra Hallo build en verpakking is voltooid, er is een nieuwe map met de naam `target`, die een bestand met de naam bevat `StormToHdfs-1.0-SNAPSHOT.jar`. Dit bestand bevat Hallo gecompileerd topologie.

## <a name="deploy-and-run-hello-topology"></a>Implementeren en uitvoeren van Hallo-topologie

1. Gebruik Hallo opdracht toocopy Hallo topologie toohello HDInsight-cluster te volgen. Vervang **gebruiker** met Hallo SSH-gebruikersnaam die u hebt gebruikt bij het maken van Hallo-cluster. Vervang **CLUSTERNAME** met de naam van de cluster Hallo Hallo.
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    Voer desgevraagd Hallo wachtwoord dat wordt gebruikt bij het maken van SSH-gebruiker Hallo voor Hallo-cluster. Als u een openbare sleutel in plaats van een wachtwoord gebruikt, moet u mogelijk toouse hello `-i` parameter toospecify Hallo pad toohello die overeenkomt met de persoonlijke sleutel.
   
   > [!NOTE]
   > Voor meer informatie over het gebruik van `scp` met HDInsight, raadpleegt u [SSH gebruiken met HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).

2. Zodra het Hallo uploaden is voltooid, gebruikt u Hallo tooconnect toohello HDInsight-cluster via SSH te volgen. Vervang **gebruiker** met Hallo SSH-gebruikersnaam die u hebt gebruikt bij het maken van Hallo-cluster. Vervang **CLUSTERNAME** met de naam van de cluster Hallo Hallo.
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    Voer desgevraagd Hallo wachtwoord dat wordt gebruikt bij het maken van SSH-gebruiker Hallo voor Hallo-cluster. Als u een openbare sleutel in plaats van een wachtwoord gebruikt, moet u mogelijk toouse hello `-i` parameter toospecify Hallo pad toohello die overeenkomt met de persoonlijke sleutel.
   
   Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

3. Eenmaal zijn verbonden, gebruik Hallo volgende opdracht toocreate een bestand met de naam `dev.properties`:

        nano dev.properties

4. Gebruik Hallo na de tekst hello inhoud Hallo `dev.properties` bestand:

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > In dit voorbeeld wordt ervan uitgegaan dat uw cluster maakt gebruik van een Azure Storage-account als Hallo standaard opslag. Als uw cluster gebruikmaakt van Azure Data Lake Store, gebruikt u `hdfs.url: adl:///` in plaats daarvan.
    
    Gebruik-bestand Hallo toosave __Ctrl + X__, klikt u vervolgens __Y__, en tot slot __Enter__. Hallo-waarden in dit bestand ingesteld Hallo Data Lake store-URL en Hallo mapnaam die gegevens naar worden geschreven.

3. Gebruik Hallo opdracht toostart Hallo topologie te volgen:
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    Deze opdracht start Hallo-topologie met Hallo lichtstroom framework door het indienen van toohello Nimbus-knooppunt van Hallo-cluster. Hallo-topologie wordt gedefinieerd door Hallo `writetohdfs.yaml` op Hallo jar bestand. Hallo `dev.properties` bestand wordt doorgegeven als een filter en Hallo waarden in Hallo-bestand worden gelezen door Hallo-topologie.

## <a name="view-output-data"></a>Gegevens van de uitvoer weergeven

tooview hello gegevens, gebruikt u Hallo volgende opdracht:

    hdfs dfs -ls /stormdata/

Een lijst met Hallo-bestanden die zijn gemaakt door deze topologie wordt weergegeven.

Hallo volgt hieronder een voorbeeld van Hallo gegevens retuned door vorige Hallo-opdrachten:

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a>Hallo-topologie stoppen

Storm-topologieën uitgevoerd totdat deze wordt gestopt of Hallo-cluster is verwijderd. toostop Hallo topologie, Hallo volgende opdracht gebruiken:

    storm kill hdfswriter

## <a name="delete-your-cluster"></a>Uw cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe toouse Storm toowrite tooAzure Storage en Azure Data Lake Store detecteren andere [Storm-voorbeelden voor HDInsight](hdinsight-storm-example-topology.md).

