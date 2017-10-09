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
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="ecb4b-105">Om tooHDFS van Apache Storm op HDInsight te schrijven</span><span class="sxs-lookup"><span data-stu-id="ecb4b-105">Write tooHDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="ecb4b-106">Meer informatie over hoe toouse Storm toowrite gegevens toohello HDFS-compatibele opslag wordt gebruikt door Apache Storm op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-106">Learn how toouse Storm toowrite data toohello HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="ecb4b-107">HDInsight kunt gebruiken beide Azure Storage en Azure Data Lake opslaan als HDFS comptabile opslag.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="ecb4b-108">Storm biedt een [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) onderdeel dat gegevens tooHDFS schrijft.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data tooHDFS.</span></span> <span data-ttu-id="ecb4b-109">Dit document bevat informatie over het schrijven van tooeither type opslag van Hallo HdfsBolt.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-109">This document provides information on writing tooeither type of storage from hello HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ecb4b-110">Hallo-voorbeeld topologie in dit document gebruikt afhankelijk van de onderdelen die deel van Storm op HDInsight uitmaken.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-110">hello example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="ecb4b-111">Deze wijziging toowork met Azure Data Lake Store gebruikt in combinatie met andere Apache Storm-clusters mogelijk.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-111">It may require modification toowork with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="ecb4b-112">Hallo code ophalen</span><span class="sxs-lookup"><span data-stu-id="ecb4b-112">Get hello code</span></span>

<span data-ttu-id="ecb4b-113">Hallo-project met deze topologie wordt beschikbaar als download van [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="ecb4b-113">hello project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="ecb4b-114">toocompile dit project, moet u na de configuratie voor uw ontwikkelomgeving Hallo:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-114">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="ecb4b-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) of hoger.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="ecb4b-116">HDInsight 3.5 of hoger vereisen Java 8.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="ecb4b-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="ecb4b-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="ecb4b-118">Hallo kunnen volgende omgevingsvariabelen worden ingesteld wanneer u Java en Hallo JDK op uw ontwikkelwerkstation installeert.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-118">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="ecb4b-119">Echter, moet u controleren of ze bestaan en dat ze de juiste waarden voor uw systeem Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="ecb4b-120">`JAVA_HOME`-moet verwijzen toohello directory waarin hello JDK is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-120">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="ecb4b-121">`PATH`-moet bevatten Hallo paden te volgen:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-121">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="ecb4b-122">`JAVA_HOME`(of gelijkwaardige Hallo-pad).</span><span class="sxs-lookup"><span data-stu-id="ecb4b-122">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="ecb4b-123">`JAVA_HOME\bin`(of gelijkwaardige Hallo-pad).</span><span class="sxs-lookup"><span data-stu-id="ecb4b-123">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="ecb4b-124">Hallo-map is waarin Maven is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-124">hello directory where Maven is installed.</span></span>

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a><span data-ttu-id="ecb4b-125">Hoe toouse Hallo HdfsBolt met HDInsight</span><span class="sxs-lookup"><span data-stu-id="ecb4b-125">How toouse hello HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecb4b-126">Voordat u Hallo HdfsBolt met Storm op HDInsight, moet u eerst een script actie toocopy vereist jar-bestanden gebruiken in Hallo `extpath` voor Storm.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-126">Before using hello HdfsBolt with Storm on HDInsight, you must first use a script action toocopy required jar files into hello `extpath` for Storm.</span></span> <span data-ttu-id="ecb4b-127">Zie voor meer informatie, Hallo [Hallo-cluster configureren](#configure) sectie.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-127">For more information, see hello [Configure hello cluster](#configure) section.</span></span>

<span data-ttu-id="ecb4b-128">Hallo HdfsBolt gebruikt Hallo bestand schema dat u toounderstand hoe bieden toowrite tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-128">hello HdfsBolt uses hello file scheme that you provide toounderstand how toowrite tooHDFS.</span></span> <span data-ttu-id="ecb4b-129">Met HDInsight, gebruikt u een Hallo schema's te volgen:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-129">With HDInsight, use one of hello following schemes:</span></span>

* <span data-ttu-id="ecb4b-130">`wasb://`: Met een Azure Storage-account gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="ecb4b-131">`adl://`: Gebruikt met Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="ecb4b-132">Hallo bevat volgende tabel voorbeelden van het gebruik van Hallo bestand schema voor verschillende scenario's:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-132">hello following table provides examples of using hello file scheme for different scenarios:</span></span>

| <span data-ttu-id="ecb4b-133">Schema</span><span class="sxs-lookup"><span data-stu-id="ecb4b-133">Scheme</span></span> | <span data-ttu-id="ecb4b-134">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="ecb4b-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="ecb4b-135">Hallo standaard storage-account is een blobcontainer in Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="ecb4b-135">hello default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="ecb4b-136">Hallo standaardopslagaccount is een map in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-136">hello default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="ecb4b-137">Tijdens het maken geeft u Hallo directory in Data Lake Store die Hallo hoofdmap van de HDFS Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-137">During cluster creation, you specify hello directory in Data Lake Store that is hello root of hello cluster's HDFS.</span></span> <span data-ttu-id="ecb4b-138">Bijvoorbeeld, Hallo `/clusters/myclustername/` directory.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-138">For example, hello `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="ecb4b-139">Een niet-standaard (Extra) Azure-opslagaccount gekoppeld Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-139">A non-default (additional) Azure storage account associated with hello cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="ecb4b-140">Hallo root Hallo Data Lake Store door Hallo cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-140">hello root of hello Data Lake Store used by hello cluster.</span></span> <span data-ttu-id="ecb4b-141">Dit schema kunt u tooaccess gegevens die zich buiten het Hallo-map met de Hallo cluster bestandssysteem bevindt.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-141">This scheme allows you tooaccess data that is located outside hello directory that contains hello cluster file system.</span></span> |

<span data-ttu-id="ecb4b-142">Zie voor meer informatie, Hallo [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) verwijzing op Apache.org.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-142">For more information, see hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="ecb4b-143">Voorbeeldconfiguratie</span><span class="sxs-lookup"><span data-stu-id="ecb4b-143">Example configuration</span></span>

<span data-ttu-id="ecb4b-144">Hallo volgende YAML is een fragment uit Hallo `resources/writetohdfs.yaml` op Hallo voorbeeld bestand.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-144">hello following YAML is an excerpt from hello `resources/writetohdfs.yaml` file included in hello example.</span></span> <span data-ttu-id="ecb4b-145">Dit bestand definieert Hallo Storm-topologie met Hallo [lichtstroom](https://storm.apache.org/releases/1.1.0/flux.html) framework voor Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-145">This file defines hello Storm topology using hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

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

<span data-ttu-id="ecb4b-146">Deze YAML definieert Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-146">This YAML defines hello following items:</span></span>

* <span data-ttu-id="ecb4b-147">`syncPolicy`: Hiermee wordt gedefinieerd wanneer bestanden gesynchroniseerd/leeggemaakte toohello-bestandssysteem zijn.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-147">`syncPolicy`: Defines when files are synched/flushed toohello file system.</span></span> <span data-ttu-id="ecb4b-148">In dit voorbeeld elke 1000 tuples.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="ecb4b-149">`fileNameFormat`: Hiermee definieert u Hallo pad en naam patroon toouse bij het schrijven van bestanden.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-149">`fileNameFormat`: Defines hello path and file name pattern toouse when writing files.</span></span> <span data-ttu-id="ecb4b-150">In dit voorbeeld Hallo pad is opgegeven tijdens runtime met een filter, en de bestandsextensie Hallo `.txt`.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-150">In this example, hello path is provided at runtime using a filter, and hello file extension is `.txt`.</span></span>
* <span data-ttu-id="ecb4b-151">`recordFormat`: Definieert Hallo interne indeling van Hallo-bestanden die zijn geschreven.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-151">`recordFormat`: Defines hello internal format of hello files written.</span></span> <span data-ttu-id="ecb4b-152">In dit voorbeeld velden worden gescheiden door Hallo `|` teken.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-152">In this example, fields are delimited by hello `|` character.</span></span>
* <span data-ttu-id="ecb4b-153">`rotationPolicy`: Hiermee wordt gedefinieerd of toorotate bestanden.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-153">`rotationPolicy`: Defines when toorotate files.</span></span> <span data-ttu-id="ecb4b-154">In dit voorbeeld wordt geen draaiing uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="ecb4b-155">`hdfs-bolt`: Gebruik voorliggende onderdelen als configuratieparameters voor Hallo Hallo `HdfsBolt` klasse.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-155">`hdfs-bolt`: Uses hello previous components as configuration parameters for hello `HdfsBolt` class.</span></span>

<span data-ttu-id="ecb4b-156">Zie voor meer informatie over Hallo lichtstroom framework [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="ecb4b-156">For more information on hello Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-hello-cluster"></a><span data-ttu-id="ecb4b-157">Hallo-cluster configureren</span><span class="sxs-lookup"><span data-stu-id="ecb4b-157">Configure hello cluster</span></span>

<span data-ttu-id="ecb4b-158">Storm op HDInsight omvat standaard geen Hallo onderdelen HdfsBolt toocommunicate gebruikt met Azure Storage of de Data Lake Store in klassenpad van Storm.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-158">By default, Storm on HDInsight does not include hello components that HdfsBolt uses toocommunicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="ecb4b-159">Gebruik Hallo volgende script actie tooadd deze onderdelen toohello `extlib` map voor Storm op het cluster:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-159">Use hello following script action tooadd these components toohello `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="ecb4b-160">| Script URI | Knooppunten tooapply naar | Parameters || `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | Geen |</span><span class="sxs-lookup"><span data-stu-id="ecb4b-160">| Script URI | Nodes tooapply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="ecb4b-161">Zie voor informatie over het gebruik van dit script met uw cluster Hallo [aanpassen HDInsight-clusters met behulp van scriptacties](./hdinsight-hadoop-customize-cluster-linux.md) document.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-161">For information on using this script with your cluster, see hello [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-hello-topology"></a><span data-ttu-id="ecb4b-162">Bouw en het Hallo-topologie van het pakket</span><span class="sxs-lookup"><span data-stu-id="ecb4b-162">Build and package hello topology</span></span>

1. <span data-ttu-id="ecb4b-163">Hallo-voorbeeldproject van downloaden [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-163">Download hello example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour development environment.</span></span>

2. <span data-ttu-id="ecb4b-164">Terminal of shell-sessie wijzigen mappen toohello hoofdmap Hallo gedownload vanaf een opdrachtprompt project.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-164">From a command prompt, terminal, or shell session, change directories toohello root of hello downloaded project.</span></span> <span data-ttu-id="ecb4b-165">toobuild en pakket Hallo topologie, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-165">toobuild and package hello topology, use hello following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="ecb4b-166">Zodra Hallo build en verpakking is voltooid, er is een nieuwe map met de naam `target`, die een bestand met de naam bevat `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-166">Once hello build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="ecb4b-167">Dit bestand bevat Hallo gecompileerd topologie.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-167">This file contains hello compiled topology.</span></span>

## <a name="deploy-and-run-hello-topology"></a><span data-ttu-id="ecb4b-168">Implementeren en uitvoeren van Hallo-topologie</span><span class="sxs-lookup"><span data-stu-id="ecb4b-168">Deploy and run hello topology</span></span>

1. <span data-ttu-id="ecb4b-169">Gebruik Hallo opdracht toocopy Hallo topologie toohello HDInsight-cluster te volgen.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-169">Use hello following command toocopy hello topology toohello HDInsight cluster.</span></span> <span data-ttu-id="ecb4b-170">Vervang **gebruiker** met Hallo SSH-gebruikersnaam die u hebt gebruikt bij het maken van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-170">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="ecb4b-171">Vervang **CLUSTERNAME** met de naam van de cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-171">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="ecb4b-172">Voer desgevraagd Hallo wachtwoord dat wordt gebruikt bij het maken van SSH-gebruiker Hallo voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-172">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="ecb4b-173">Als u een openbare sleutel in plaats van een wachtwoord gebruikt, moet u mogelijk toouse hello `-i` parameter toospecify Hallo pad toohello die overeenkomt met de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-173">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ecb4b-174">Voor meer informatie over het gebruik van `scp` met HDInsight, raadpleegt u [SSH gebruiken met HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ecb4b-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ecb4b-175">Zodra het Hallo uploaden is voltooid, gebruikt u Hallo tooconnect toohello HDInsight-cluster via SSH te volgen.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-175">Once hello upload completes, use hello following tooconnect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="ecb4b-176">Vervang **gebruiker** met Hallo SSH-gebruikersnaam die u hebt gebruikt bij het maken van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-176">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="ecb4b-177">Vervang **CLUSTERNAME** met de naam van de cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-177">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="ecb4b-178">Voer desgevraagd Hallo wachtwoord dat wordt gebruikt bij het maken van SSH-gebruiker Hallo voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-178">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="ecb4b-179">Als u een openbare sleutel in plaats van een wachtwoord gebruikt, moet u mogelijk toouse hello `-i` parameter toospecify Hallo pad toohello die overeenkomt met de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-179">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   <span data-ttu-id="ecb4b-180">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="ecb4b-181">Eenmaal zijn verbonden, gebruik Hallo volgende opdracht toocreate een bestand met de naam `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-181">Once connected, use hello following command toocreate a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="ecb4b-182">Gebruik Hallo na de tekst hello inhoud Hallo `dev.properties` bestand:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-182">Use hello following text as hello contents of hello `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="ecb4b-183">In dit voorbeeld wordt ervan uitgegaan dat uw cluster maakt gebruik van een Azure Storage-account als Hallo standaard opslag.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-183">This example assumes that your cluster uses an Azure Storage account as hello default storage.</span></span> <span data-ttu-id="ecb4b-184">Als uw cluster gebruikmaakt van Azure Data Lake Store, gebruikt u `hdfs.url: adl:///` in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="ecb4b-185">Gebruik-bestand Hallo toosave __Ctrl + X__, klikt u vervolgens __Y__, en tot slot __Enter__.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-185">toosave hello file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="ecb4b-186">Hallo-waarden in dit bestand ingesteld Hallo Data Lake store-URL en Hallo mapnaam die gegevens naar worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-186">hello values in this file set hello Data Lake store URL and hello directory name that data is written to.</span></span>

3. <span data-ttu-id="ecb4b-187">Gebruik Hallo opdracht toostart Hallo topologie te volgen:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-187">Use hello following command toostart hello topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="ecb4b-188">Deze opdracht start Hallo-topologie met Hallo lichtstroom framework door het indienen van toohello Nimbus-knooppunt van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-188">This command starts hello topology using hello Flux framework by submitting it toohello Nimbus node of hello cluster.</span></span> <span data-ttu-id="ecb4b-189">Hallo-topologie wordt gedefinieerd door Hallo `writetohdfs.yaml` op Hallo jar bestand.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-189">hello topology is defined by hello `writetohdfs.yaml` file included in hello jar.</span></span> <span data-ttu-id="ecb4b-190">Hallo `dev.properties` bestand wordt doorgegeven als een filter en Hallo waarden in Hallo-bestand worden gelezen door Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-190">hello `dev.properties` file is passed as a filter, and hello values contained in hello file are read by hello topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="ecb4b-191">Gegevens van de uitvoer weergeven</span><span class="sxs-lookup"><span data-stu-id="ecb4b-191">View output data</span></span>

<span data-ttu-id="ecb4b-192">tooview hello gegevens, gebruikt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-192">tooview hello data, use hello following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="ecb4b-193">Een lijst met Hallo-bestanden die zijn gemaakt door deze topologie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-193">A list of hello files created by this topology is displayed.</span></span>

<span data-ttu-id="ecb4b-194">Hallo volgt hieronder een voorbeeld van Hallo gegevens retuned door vorige Hallo-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-194">hello following list is an example of hello data retuned by hello previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a><span data-ttu-id="ecb4b-195">Hallo-topologie stoppen</span><span class="sxs-lookup"><span data-stu-id="ecb4b-195">Stop hello topology</span></span>

<span data-ttu-id="ecb4b-196">Storm-topologieën uitgevoerd totdat deze wordt gestopt of Hallo-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-196">Storm topologies run until stopped, or hello cluster is deleted.</span></span> <span data-ttu-id="ecb4b-197">toostop Hallo topologie, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ecb4b-197">toostop hello topology, use hello following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="ecb4b-198">Uw cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="ecb4b-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="ecb4b-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ecb4b-199">Next steps</span></span>

<span data-ttu-id="ecb4b-200">U hebt geleerd hoe toouse Storm toowrite tooAzure Storage en Azure Data Lake Store detecteren andere [Storm-voorbeelden voor HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ecb4b-200">Now that you have learned how toouse Storm toowrite tooAzure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

