---
title: aaaScript action - pakketten voor Python installeren met Jupyter op Azure HDInsight | Microsoft Docs
description: Stapsgewijze instructies over hoe toouse script actie tooconfigure Jupyter-notebooks beschikbaar met HDInsight Spark-clusters toouse externe python-pakketten.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Scriptactie tooinstall externe Python-pakketten gebruiken voor Jupyter-notebooks in Apache Spark-clusters in HDInsight
> [!div class="op_single_selector"]
> * [Met behulp van de cel verwerkt Magic-pakket](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Met behulp van de scriptactie](hdinsight-apache-spark-python-package-installation.md)
>
>

Meer informatie over hoe toouse scriptacties tooconfigure een Apache Spark-cluster in HDInsight (Linux) toouse externe, community-hebben bijgedragen **python** pakketten die niet zijn opgenomen out-of-the-box in Hallo-cluster.

> [!NOTE]
> U kunt ook een Jupyter-notebook configureren met behulp van `%%configure` magic toouse externe pakketten. Zie voor instructies [externe pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).
> 
> 

U kunt zoeken Hallo [package index](https://pypi.python.org/pypi) voor Hallo volledige lijst met pakketten die beschikbaar zijn. U kunt ook een lijst met beschikbare pakketten opvragen uit andere bronnen. Bijvoorbeeld, kunt u pakketten beschikbaar gesteld via installeren [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) of [conda smidse](https://conda-forge.github.io/feedstocks.html).

In dit artikel leert u hoe tooinstall hello [TensorFlow](https://www.tensorflow.org/) van het pakket met Script Actoin op het cluster en deze gebruiken via Jupyter-notebook Hallo.

## <a name="prerequisites"></a>Vereisten
U moet Hallo volgende hebben:

* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

   > [!NOTE]
   > Als u nog geen een Spark-cluster in HDInsight Linux, kunt u scriptacties uitvoeren tijdens het maken van het cluster. Ga naar Hallo-documentatie op [hoe toouse aangepaste acties script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a>Externe pakketten gebruiken met Jupyter-notebooks

1. Van Hallo [Azure Portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt). U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.   

2. Klik op Hallo blade Spark-cluster **scriptacties** onder **gebruik**. Hallo aangepaste actie uitvoeren installeert die TensorFlow in de hoofdknooppunten Hallo en Hallo worker-knooppunten. Hallo bash-script kan worden verwezen vanuit: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh bezoek Hallo documentatie op [hoe toouse aangepaste acties script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

   > [!NOTE]
   > Er zijn twee python-installaties in Hallo-cluster. Spark gebruikt Hallo Anaconda python installatie zich bevindt op `/usr/bin/anaconda/bin`. Met de installatie in uw aangepaste acties via verwijzen naar `/usr/bin/anaconda/bin/pip` en `/usr/bin/anaconda/bin/conda`.
   > 
   > 

3. Open een PySpark Jupyter-notebook

    ![Een nieuwe Jupyter-notebook maken](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Een nieuwe Jupyter-notebook maken")

4. Een nieuwe notebook gemaakt en geopend met de Hallo naam Untitled.pynb. Klik op Hallo notebook naam Hallo boven en een beschrijvende naam.

    ![Geef een naam voor de notebook Hallo](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Geef een naam voor de notebook Hallo")

5. U gaat nu `import tensorflow` en een Hallo wereld-voorbeeld uitvoeren. 

    Code toocopy:

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    Hallo resultaat ziet er als volgt:
    
    ![De uitvoering van code TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "code TensorFlow uitvoeren")



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
* [Externe pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)
