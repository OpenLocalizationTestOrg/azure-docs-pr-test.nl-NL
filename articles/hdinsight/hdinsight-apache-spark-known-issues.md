---
title: aaaTroubleshoot problemen met Apache Spark-cluster in Azure HDInsight | Microsoft Docs
description: Meer informatie over problemen met gerelateerde tooApache Spark-clusters in Azure HDInsight en hoe toowork rond de.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>Bekende problemen van Apache Spark-cluster in HDInsight

Dit document houdt van alle Hallo bekende problemen bij het Hallo HDInsight Spark openbare preview.  

## <a name="livy-leaks-interactive-session"></a>Livy lekt interactieve sessies
Wanneer Livy opnieuw wordt gestart (van Ambari of vervaldatum tooheadnode 0 virtuele machine opnieuw opstarten) met een interactieve sessie nog steeds actief is, wordt er een sessie interactieve taak gelekt. Als gevolg hiervan nieuwe taken kan blijven steken bij Hallo geaccepteerde status en kan niet worden gestart.

**Risicobeperking:**

Hallo te volgen procedure tooworkaround Hallo probleem gebruiken:

1. SSH in headnode. Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

2. Voer Hallo na opdracht toofind Hallo toepassing-id's van Hallo interactieve taken gestart via Livy. 
   
        yarn application –list
   
    Hallo taak standaardnamen worden Livy als Hallo taken zijn gestart met een interactieve sessie Livy met geen expliciete namen voor Hallo opgegeven Livy-sessie gestart door de Jupyter-notebook Hallo taaknaam begint met remotesparkmagics_ *. 
3. Hallo opdracht tookill volgende taken uitvoeren. 
   
        yarn application –kill <Application ID>

Nieuwe taken worden gestart met. 

## <a name="spark-history-server-not-started"></a>Spark geschiedenis Server is niet gestart
Spark geschiedenis Server is niet automatisch gestart nadat een cluster is gemaakt.  

**Risicobeperking:** 

Handmatig Hallo geschiedenis server starten vanaf Ambari.

## <a name="permission-issue-in-spark-log-directory"></a>Machtiging probleem in de logboekmap Spark
Wanneer hdiuser een taak met spark-submit verzendt, er is een fout java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (toestemming geweigerd) en Hallo Stuurprogrammalogboek is niet geschreven. 

**Risicobeperking:**

1. Hdiuser toohello Hadoop groep toevoegen. 
2. Geef een 777 machtigingen op /var/log/spark na het maken van het cluster. 
3. Hallo spark-Logboeklocatie met Ambari toobe een map met 777 machtigingen bijwerken.  
4. Voer spark-indienen als sudo.  

## <a name="spark-phoenix-connector-is-not-supported"></a>Spark Phoenix connector wordt niet ondersteund

Hallo Spark Phoenix connector wordt momenteel niet ondersteund met een HDInsight Spark-cluster.

**Risicobeperking:**

In plaats daarvan moet u Hallo Spark-HBase-connector gebruiken. Zie voor instructies [hoe toouse Spark HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).

## <a name="issues-related-toojupyter-notebooks"></a>Problemen tooJupyter laptops
Hier volgen enkele bekende problemen gerelateerde tooJupyter laptops.

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>Laptops met niet-ASCII-tekens in bestandsnamen
Jupyter-notebooks die kunnen worden gebruikt in HDInsight Spark-clusters mag geen niet-ASCII-tekens in bestandsnamen. Als u een bestand via Hallo Jupyter UI een niet-ASCII-bestandsnaam heeft tooupload probeert, zal mislukken achtergrond (dat wil zeggen, Jupyter kunt u Hallo-bestand uploaden, maar deze won't ofwel een zichtbaar fout genereert). 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>Fout tijdens het laden van notitieblokken van grotere
U ziet mogelijk een fout  **`Error loading notebook`**  wanneer het laden van laptops die groter zijn.  

**Risicobeperking:**

Als u deze fout krijgt, betekent niet dat uw gegevens is beschadigd of verloren.  Uw laptops zich nog steeds op schijf in `/var/lib/jupyter`, en u kunt SSH in Hallo cluster tooaccess ze. Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

Zodra u toohello-cluster via SSH hebt gekoppeld, kunt u uw notitieblokken van uw cluster tooyour lokale computer (via SCP of WinSCP) als een back-tooprevent Hallo verlies van alle belangrijke gegevens in de notebook Hallo kopiëren. U kunt vervolgens SSH-tunnel in uw headnode op poort 8001 tooaccess Jupyter zonder tussenkomst van Hallo-gateway.  Daar kunt u wist Hallo-uitvoer van uw laptop en sla opnieuw op toominimize Hallo notebook grootte.

tooprevent deze fout voorkomen in Hallo toekomstige, moet u enkele aanbevolen procedures volgen:

* Het is belangrijk tookeep Hallo notebook grootte klein. Elke uitvoer van uw Spark-taken die wordt teruggestuurd tooJupyter wordt bewaard in de notebook Hallo.  Het is een best practice met Jupyter in algemene tooavoid met `.collect()` op grote RDD of dataframes; als u toopeek op een RDD inhoud wilt, overweeg in plaats daarvan uitgevoerd `.take()` of `.sample()` zodat de uitvoer te groot niet ophalen.
* Ook als u een laptop opslaat, uitvoer Wis alle cellen tooreduce Hallo grootte.

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>Laptop opstarten duurt langer dan verwacht
Eerste code-instructie in Jupyter-notebook met behulp van Spark magic kan meer dan een minuut duren.  

**Uitleg:**

Dit gebeurt omdat wanneer de eerste codecel hello wordt uitgevoerd. Op de achtergrond Hallo Hiermee initieert u sessieconfiguratie en Spark, SQL en Hive-contexten worden ingesteld. Nadat deze contexten zijn ingesteld, de eerste instructie hello wordt uitgevoerd en daarmee Hallo indruk dat Hallo-instructie een toocomplete lang duurde.

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a>De time-out voor de Jupyter-notebook in Hallo-sessie maken
Wanneer het Spark-cluster heeft onvoldoende resources, wordt Hallo Spark en Pyspark kernels in Hallo Jupyter-notebook time-out bij het toocreate Hallo-sessie. 

**Oplossingen:** 

1. Sommige resources in uw Spark-cluster door vrijmaken:
   
   * Stoppen van andere laptops Spark toohello gaat sluiten en stoppen menu of afsluiten in Hallo notebook explorer te klikken.
   * Andere toepassingen Spark YARN wordt gestopt.
2. Hallo-notebook die u toostart van probeerde opnieuw opstarten Onvoldoende bronnen moeten beschikbaar zijn voor u toocreate nu een sessie.

## <a name="see-also"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Toepassingen maken en uitvoeren
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [De invoegtoepassing HDInsight Tools voor toocreate IntelliJ IDEA gebruiken en het verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)

