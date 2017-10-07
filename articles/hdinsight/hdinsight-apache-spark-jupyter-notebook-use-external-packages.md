---
title: aangepaste Maven-pakketten aaaUse met Jupyter in Spark op Azure HDInsight | Microsoft Docs
description: Stapsgewijze instructies over hoe tooconfigure Jupyter-notebooks beschikbaar met HDInsight Spark-clusters toouse aangepaste Maven-pakketten.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Externe pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight
> [!div class="op_single_selector"]
> * [Met behulp van de cel verwerkt Magic-pakket](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Met behulp van de scriptactie](hdinsight-apache-spark-python-package-installation.md)
>
>

Meer informatie over hoe tooconfigure een Jupyter-notebook in Apache Spark-cluster in HDInsight toouse externe, community-hebben bijgedragen **maven** pakketten die niet zijn opgenomen out-of-the-box in Hallo-cluster. 

U kunt zoeken Hallo [Maven opslagplaats](http://search.maven.org/) voor Hallo volledige lijst met pakketten die beschikbaar zijn. U kunt ook een lijst met beschikbare pakketten opvragen uit andere bronnen. Bijvoorbeeld, een volledige lijst met pakketten community bijgedragen is beschikbaar op [Spark pakketten](http://spark-packages.org/).

In dit artikel leert u hoe toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakket met de Jupyter-notebook Hallo.



## <a name="prerequisites"></a>Vereisten
U moet Hallo volgende hebben:

* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="use-external-packages-with-jupyter-notebooks"></a>Externe pakketten gebruiken met Jupyter-notebooks
1. Van Hallo [Azure Portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt). U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.   
2. Klik vanuit Hallo blade Spark-cluster op **snelkoppelingen**, en klik vervolgens vanuit Hallo **Cluster-Dashboard** blade klikt u op **Jupyter-Notebook**. Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.

    > [!NOTE]
    > U mogelijk ook Hallo Jupyter-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken. Vervang **CLUSTERNAME** met Hallo-naam van het cluster:
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. Maak een nieuwe notebook. Klik op **nieuw**, en klik vervolgens op **Spark**.
   
    ![Een nieuwe Jupyter-notebook maken](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Een nieuwe Jupyter-notebook maken")

4. Een nieuwe notebook gemaakt en geopend met de Hallo naam Untitled.pynb. Klik op Hallo notebook naam Hallo boven en een beschrijvende naam.
   
    ![Geef een naam voor de notebook Hallo](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Geef een naam voor de notebook Hallo")

5. U gebruikt Hallo `%%configure` magische tooconfigure Hallo notebook toouse een externe-pakket. Zorg ervoor dat u Hallo aanroepen in notitieblokken die gebruikmaken van externe pakketten, `%%configure` magische in de eerste codecel Hallo. Dit zorgt ervoor dat kernel Hallo geconfigureerde toouse Hallo pakket voordat het Hallo-sessie gestart.

    >[!IMPORTANT] 
    >Als u tooconfigure Hallo kernel in de eerste cel Hallo vergeet, kunt u Hallo `%%configure` Hello `-f` parameter, maar die wordt opnieuw opgestart Hallo-sessie en voortgang van alle gaan verloren.

    | HDInsight-versie | Opdracht |
    |-------------------|---------|
    |Voor HDInsight 3.3 en HDInsight 3.4 | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | Voor HDInsight 3.5 | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. Hallo codefragment hierboven verwacht Hallo maven-coördinaten voor een externe Hallo-pakket in de centrale opslagplaats Maven. In dit fragment `com.databricks:spark-csv_2.10:1.4.0` hello maven-coördinaat voor **spark-csv** pakket. Hier ziet u hoe u Hallo-coördinaten voor een pakket maken.
   
    a. Hallo-pakket niet vinden in Hallo Maven-opslagplaats. Voor deze zelfstudie gebruiken we [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Verzamel uit de opslagplaats hello, Hallo waarden voor **GroupId**, **artefact-id**, en **versie**. Zorg ervoor dat u verzamelen Hallo-waarden overeenkomen met uw cluster. In dit geval gebruiken we een Scala 2.10 en Spark 1.4.0 pakket, maar mogelijk moet u verschillende versies van tooselect voor de juiste Scala of Spark versie Hallo in uw cluster. U vindt hier Hallo Scala versie op het cluster door het uitvoeren van `scala.util.Properties.versionString` op Hallo Spark Jupyter kernel of Spark verzenden. U vindt hier Hallo Spark versie op het cluster door het uitvoeren van `sc.version` op Jupyter-notebooks.
   
    ![Externe pakketten gebruiken met Jupyter-notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "externe pakketten gebruiken met Jupyter-notebook")
   
    c. Samenvoegen van Hallo drie waarden, gescheiden door een dubbele punt (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

7. Hallo codecel uitvoeren met Hallo `%%configure` verwerkt Magic-pakket. Dit configureert Hallo onderliggende Livy sessie toouse Hallo pakket die u hebt opgegeven. U kunt nu Hallo-pakket gebruiken in de volgende cellen Hallo in Hallo laptop, zoals hieronder wordt weergegeven.
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. Vervolgens kunt u Hallo codefragmenten uitvoeren, zoals hieronder weergegeven tooview hello gegevens van Hallo dataframe u hebt gemaakt in de vorige stap Hallo.
   
        df.show()
   
        df.select("Time").count()

## <a name="seealso"></a>Zie ook
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

* [Externe python-pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight Linux](hdinsight-apache-spark-python-package-installation.md)
* [De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)

