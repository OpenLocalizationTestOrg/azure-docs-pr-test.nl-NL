---
title: aaaMicrosoft cognitieve Toolkit met Azure HDInsight Spark voor grondige learning | Microsoft Docs
description: Meer informatie over hoe een getraind Microsoft cognitieve Toolkit grondige learning-model kan worden toegepast tooa gegevensset met Hallo Spark Python API in een Azure HDInsight Spark-cluster.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a>Gebruik Microsoft cognitieve Toolkit grondige learning-model met Azure HDInsight Spark-cluster

In dit artikel, u Hallo volgende stappen.

1. Een aangepast script tooinstall Microsoft cognitieve Toolkit uitvoeren op een Azure HDInsight Spark-cluster.

2. Het uploaden van een Jupyter-notebook toohello Spark-cluster toosee tooapply een getraind Microsoft cognitieve Toolkit grondige learning-model toofiles in een Azure Blob Storage-Account met behulp van Hallo [Spark Python-API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)

## <a name="prerequisites"></a>Vereisten

* **Een Azure-abonnement**. Voordat u met deze zelfstudie begint, moet u een Azure-abonnement hebben. Zie [Maak vandaag nog uw gratis Azure-account](https://azure.microsoft.com/free).

* **Azure HDInsight Spark-cluster**. Voor dit artikel, een 2.0 Spark-cluster te maken. Zie voor instructies [maken Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-does-this-solution-flow"></a>Hoe deze oplossing stromen

Deze oplossing wordt verdeeld over dit artikel en een Jupyter-notebook die u als onderdeel van deze zelfstudie uploadt. In dit artikel kunt u Hallo stappen uitvoeren:

* Een scriptactie uitvoeren op een HDInsight Spark-cluster tooinstall Microsoft cognitieve Toolkit en Python-pakketten.
* Upload Hallo Jupyter-notebook die Hallo oplossing toohello HDInsight Spark-cluster wordt uitgevoerd.

Hallo worden volgende resterende stappen behandeld in Hallo Jupyter-notebook.

- Installatiekopieën van het voorbeeld in een Spark Resiliant gedistribueerd gegevensset of RDD geladen
   - Laden van modules en standaardinstellingen definiëren
   - Hallo gegevensset lokaal op Hallo Spark-cluster downloaden
   - Hallo gegevensset converteren naar een RDD
- Hallo afbeeldingen met een getraind cognitieve Toolkit model beoordelen
   - Hallo getraind cognitieve Toolkit model toohello Spark-cluster downloaden
   - Functies toobe die wordt gebruikt door de worker-knooppunten definiëren
   - Score Hallo afbeeldingen op de worker-knooppunten
   - De nauwkeurigheid model evalueren


## <a name="install-microsoft-cognitive-toolkit"></a>Microsoft cognitieve Toolkit installeren

U kunt Microsoft cognitieve Toolkit installeren op een Spark-cluster met behulp van de scriptactie. Scriptactie gebruikmaakt van aangepaste scripts tooinstall onderdelen op Hallo cluster die niet standaard beschikbaar. Kunt u aangepast script Hallo van hello Azure-Portal met behulp van HDInsight .NET SDK of met behulp van Azure PowerShell. U kunt ook als onderdeel van het maken van het cluster, of nadat Hallo-cluster is actief en werkend Hallo script tooinstall Hallo toolkit gebruiken. 

In dit artikel gebruiken we Hallo portal tooinstall Hallo toolkit nadat Hallo-cluster is gemaakt. Zie voor andere manieren toorun Hallo aangepast script, [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).

### <a name="using-hello-azure-portal"></a>Met behulp van hello Azure Portal

Zie voor instructies over hoe toouse hello Azure Portal toorun actie script, [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation). Zorg ervoor dat u na invoer tooinstall Microsoft cognitieve Toolkit Hallo opgeven.

* Geef een waarde voor actienaam Hallo-script.

* Voor **Bash script URI**, voer `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.

* Controleer of u Hallo script alleen uitvoeren op Hallo hoofd- en werkrollen knooppunten en wis alle andere selectievakjes Hallo.

* Klik op **Create**.

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a>Hallo Jupyter-notebook tooAzure HDInsight Spark-cluster uploaden

toouse hello Microsoft cognitieve Toolkit met hello Azure HDInsight Spark-cluster, moet u de Jupyter-notebook Hallo laden **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark-cluster. Deze laptop is beschikbaar op GitHub op [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).

1. Kloon Hallo GitHub-opslagplaats [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration). Zie voor instructies tooclone, [een opslagplaats klonen](https://help.github.com/articles/cloning-a-repository/).

2. Open in hello Azure Portal, Hallo blade Spark-cluster dat u al ingericht, klikt u op **Cluster-Dashboard**, en klik vervolgens op **Jupyter-notebook**.

    U kunt ook Hallo Jupyter-notebook starten door te gaan toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`. Vervang \<clustername > Hallo-naam van uw HDInsight-cluster.

3. Hallo Jupyter-notebook, klik op **uploaden** in Hallo rechterbovenhoek en navigeer vervolgens toohello locatie waar u de GitHub-opslagplaats Hallo gekloond.

    ![Uploaden van Jupyter-notebook tooAzure HDInsight Spark-cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "uploaden Jupyter-notebook tooAzure HDInsight Spark-cluster")

4. Klik op **uploaden** opnieuw.

5. Nadat de notebook Hallo is geüpload, klikt u op de naam Hallo van Hallo laptop en volg Hallo-instructies in het Hallo-notebook zelf op hoe tooload Hallo gegevensset en Hallo zelfstudie uit te voeren.

## <a name="see-also"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Analyse van Application Insights-telemetriegegevens met behulp van Spark in HDInsight](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a>Toepassingen maken en uitvoeren
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
